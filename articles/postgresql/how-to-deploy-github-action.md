---
title: '빠른 시작: GitHub Actions를 통해 Azure PostgreSQL에 연결'
description: GitHub Actions 워크플로에서 Azure PostgreSQL 사용
author: mksuni
ms.service: postgresql
ms.topic: quickstart
ms.author: sumuth
ms.date: 10/12/2020
ms.custom: github-actions-azure
ms.openlocfilehash: 2e546801f95d9d884bdfb3f09a18b3fa6e2d78a1
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97364989"
---
# <a name="quickstart-use-github-actions-to-connect-to-azure-postgresql"></a>빠른 시작: GitHub Actions를 사용하여 Azure PostgreSQL에 연결

<Token>**적용 대상:** :::image type="icon" source="./media/applies-to/yes.png" border="false":::Azure Database for PostgreSQL - 단일 서버 :::image type="icon" source="./media/applies-to/yes.png" border="false":::Azure Database for PostgreSQL - 유연한 서버</Token>

워크플로를 사용하여 [Azure Database for PostgreSQL](https://azure.microsoft.com/services/postgresql/)에 데이터베이스 업데이트를 배포하는 [GitHub Actions](https://docs.github.com/en/actions)를 시작합니다.

## <a name="prerequisites"></a>사전 요구 사항

필요한 항목은 다음과 같습니다.
- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- 샘플 데이터(`data.sql`)가 들어 있는 GitHub 리포지토리. GitHub 계정이 없는 경우 [평가판에 가입](https://github.com/join)하세요.
- Azure Database for PostgreSQL 서버.
    - [빠른 시작: Azure Portal에서 PostgreSQL 서버용 Azure Database 만들기](quickstart-create-server-database-portal.md)

## <a name="workflow-file-overview"></a>워크플로 파일 개요

GitHub Actions 워크플로는 리포지토리의 `/.github/workflows/` 경로에 있는 YAML(.yml) 파일에서 정의됩니다. 이 정의는 워크플로를 구성하는 다양한 단계와 매개 변수를 포함합니다.

이 파일에는 다음 두 가지 섹션이 있습니다.

|섹션  |작업  |
|---------|---------|
|**인증** | 1. 서비스 주체를 정의합니다. <br /> 2. GitHub 비밀을 만듭니다. |
|**배포** | 1. 데이터베이스를 배포합니다. |

## <a name="generate-deployment-credentials"></a>배포 자격 증명 생성

[Azure CLI](/cli/azure/)에서 [az ad sp create-for-rbac](/cli/azure/ad/sp#az-ad-sp-create-for-rbac&preserve-view=true) 명령을 사용하여 [서비스 주체](../active-directory/develop/app-objects-and-service-principals.md)를 만들 수 있습니다. 이 명령은 Azure Portal에서 [Azure Cloud Shell](https://shell.azure.com/)을 사용하거나 **사용해 보세요** 단추를 선택하여 실행합니다.

`server-name` 자리 표시자를 Azure에서 호스팅되는 PostgreSQL 서버의 이름으로 바꿉니다. `subscription-id` 및 `resource-group`을 PostgreSQL 서버에 연결된 구독 ID 및 리소스 그룹으로 바꿉니다.

```azurecli-interactive
   az ad sp create-for-rbac --name {server-name} --role contributor \
                            --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                            --sdk-auth
```

출력은 아래와 비슷한 데이터베이스에 대한 액세스 권한을 제공하는 역할 할당 자격 증명이 포함된 JSON 개체입니다. 나중에 사용할 수 있도록 이 출력 JSON 개체를 복사합니다.

```output
  {
    "clientId": "<GUID>",
    "clientSecret": "<GUID>",
    "subscriptionId": "<GUID>",
    "tenantId": "<GUID>",
    (...)
  }
```

> [!IMPORTANT]
> 항상 최소한의 액세스 권한을 부여하는 것이 좋습니다. 이전 예제의 범위가 전체 리소스 그룹이 아닌 특정 서버로 제한됩니다.

## <a name="copy-the-postgresql-connection-string"></a>PostgreSQL 연결 문자열 복사

Azure Portal에서 Azure Database for PostgreSQL 서버로 이동하여 **설정** > **연결 문자열** 을 엽니다. **ADO.NET** 연결 문자열을 복사합니다. `your_database` 및 `your_password`의 자리 표시자 값을 바꿉니다. 연결 문자열은 다음과 비슷합니다.

> [!IMPORTANT]
> - 단일 서버의 경우 ```user=adminusername@servername```을 사용합니다. ```@servername```은 필수입니다.
> - 유연한 서버의 경우 ```@servername```없이 ```user= adminusername```을 사용합니다.

```output
psql host={servername.postgres.database.azure.com} port=5432 dbname={your_database} user={adminusername} password={your_database_password} sslmode=require
```

연결 문자열을 GitHub 비밀로 사용합니다.

## <a name="configure-the-github-secrets"></a>GitHub 비밀 구성

1. [GitHub](https://github.com/)에서 리포지토리를 찾습니다.

1. **설정 > 비밀 > 새 비밀** 을 차례로 선택합니다.

1. Azure CLI 명령의 전체 JSON 출력을 비밀의 값 필드에 붙여넣습니다. 비밀 이름을 `AZURE_CREDENTIALS`로 지정합니다.

    나중에 워크플로 파일을 구성할 때 이 비밀을 Azure 로그인 작업의 `creds` 입력에 사용합니다. 예를 들면 다음과 같습니다.

    ```yaml
    - uses: azure/login@v1
    with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
   ```

1. **새 비밀** 을 다시 선택합니다.

1. 연결 문자열 값을 비밀의 값 필드에 붙여넣습니다. 비밀 이름을 `AZURE_POSTGRESQL_CONNECTION_STRING`으로 지정합니다.


## <a name="add-your-workflow"></a>워크플로 추가

1. GitHub 리포지토리에 대한 **작업** 으로 이동합니다.

2. **워크플로 직접 설정** 을 선택합니다.

2. 워크플로 파일의 `on:` 섹션 뒤에 있는 모든 항목을 삭제합니다. 예를 들어 나머지 워크플로는 다음과 같습니다.

    ```yaml
    name: CI

    on:
    push:
        branches: [ master ]
    pull_request:
        branches: [ master ]
    ```

1. 워크플로 이름을 `PostgreSQL for GitHub Actions`로 바꾸고, 체크 아웃 및 로그인 작업을 추가합니다. 이러한 작업은 사이트 코드를 체크 아웃하고 이전에 만든 `AZURE_CREDENTIALS` GitHub 비밀을 사용하여 Azure에서 인증합니다.

    ```yaml
    name: PostgreSQL for GitHub Actions

    on:
    push:
        branches: [ master ]
    pull_request:
        branches: [ master ]

    jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v1
        - uses: azure/login@v1
        with:
            creds: ${{ secrets.AZURE_CREDENTIALS }}
    ```

2. Azure PostgreSQL 배포 작업을 사용하여 PostgreSQL 인스턴스에 연결합니다. `POSTGRESQL_SERVER_NAME`을 사용자의 서버 이름으로 바꿉니다. 리포지토리의 루트 수준에 `data.sql`이라는 PostgreSQL 데이터 파일이 있어야 합니다.

    ```yaml
     - uses: azure/postgresql@v1
       with:
        connection-string: ${{ secrets.AZURE_POSTGRESQL_CONNECTION_STRING }}
        server-name: POSTGRESQL_SERVER_NAME
        sql-file: './data.sql'
    ```

3. Azure에서 로그아웃하는 작업을 추가하여 워크플로를 완성합니다. 완성된 워크플로는 다음과 같습니다. 파일이 리포지토리의 `.github/workflows` 폴더에 표시됩니다.

    ```yaml
   name: PostgreSQL for GitHub Actions

    on:
    push:
        branches: [ master ]
    pull_request:
        branches: [ master ]


    jobs:
    build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v1
        - uses: azure/login@v1
        with:
            creds: ${{ secrets.AZURE_CREDENTIALS }}

    - uses: azure/postgresql@v1
      with:
        server-name: POSTGRESQL_SERVER_NAME
        connection-string: ${{ secrets.AZURE_POSTGRESQL_CONNECTION_STRING }}
        sql-file: './data.sql'

        # Azure logout
    - name: logout
      run: |
         az logout
    ```

## <a name="review-your-deployment"></a>배포 검토

1. GitHub 리포지토리에 대한 **작업** 으로 이동합니다.

1. 첫 번째 결과를 열어 워크플로 실행에 대한 자세한 로그를 확인합니다.

    :::image type="content" source="media/how-to-deploy-github-action/gitbub-action-postgres-success.png" alt-text="GitHub 작업 실행 로그":::

## <a name="clean-up-resources"></a>리소스 정리

Azure PostgreSQL 데이터베이스 및 리포지토리가 더 이상 필요하지 않은 경우 리소스 그룹과 GitHub 리포지토리를 삭제하여 배포한 리소스를 정리합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Azure 및 GitHub 통합에 대해 알아보기](/azure/developer/github/)
<br/>
> [!div class="nextstepaction"]
> [서버에 연결하는 방법 알아보기](how-to-connect-query-guide.md)
