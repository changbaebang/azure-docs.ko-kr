---
title: '자습서: Azure Static Web Apps에서 서버에 렌더링된 Nuxt.js 웹 사이트 배포'
description: Azure Static Web Apps를 사용하여 Nuxt.js 동적 사이트를 생성하고 배포합니다.
services: static-web-apps
author: christiannwamba
ms.service: static-web-apps
ms.topic: tutorial
ms.date: 05/08/2020
ms.author: chnwamba
ms.custom: devx-track-js
ms.openlocfilehash: 8f21f5fa8ee9035fe594cecff37a63b1ef2115cc
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97563469"
---
# <a name="deploy-server-rendered-nuxtjs-websites-on-azure-static-web-apps-preview"></a>Azure Static Web Apps 미리 보기에서 서버에 렌더링된 Nuxt.js 웹 사이트 배포

이 자습서에서는 [Azure Static Web Apps](overview.md)에 [Nuxt.js](https://nuxtjs.org) 생성 정적 웹 사이트를 배포하는 방법을 알아봅니다. 시작하려면 Nuxt.js 앱을 설정, 구성 및 배포하는 방법을 알아봅니다. 이 프로세스 동안 Nuxt.js를 사용하여 정적 페이지를 생성할 때 자주 발생하는 일반적인 문제를 처리하는 방법에 대해서도 알아봅니다.

## <a name="prerequisites"></a>사전 요구 사항

- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/).
- GitHub 계정. [체험 계정을 만듭니다](https://github.com/join).
- 설치된 [Node.js](https://nodejs.org).

## <a name="set-up-a-nuxtjs-app"></a>Nuxt.js 앱 설정

`create-nuxt-app`을 사용하여 새 Nuxt.js 프로젝트를 설정할 수 있습니다. 이 자습서에서는 새 프로젝트 대신 기존 리포지토리를 복제하는 것으로 시작합니다. 이 리포지토리는 동적 Nuxt.js 앱을 정적 사이트로 배포하는 방법을 보여 주기 위해 설정되었습니다.

1. 템플릿 리포지토리에서 GitHub 계정 아래에 새 리포지토리를 만듭니다.
1. [http://github.com/staticwebdev/nuxtjs-starter/generate](https://github.com/login?return_to=/staticwebdev/nuxtjs-starter/generate)로 이동합니다.
1. 리포지토리 이름을 **nuxtjs-starter** 로 지정합니다.
1. 그런 다음, 새 리포지토리를 머신에 복제합니다. <YOUR_GITHUB_ACCOUNT_NAME>을 계정 이름으로 바꾸어야 합니다.

    ```bash
    git clone http://github.com/<YOUR_GITHUB_ACCOUNT_NAME>/nuxtjs-starter
    ```

1. 새로 복제된 Nuxt.js 앱으로 이동합니다.

   ```bash
   cd nuxtjs-starter
   ```

1. 종속성을 설치합니다.

    ```bash
    npm install
    ```

1. 개발 중인 Nuxt.js 앱을 시작합니다.

    ```bash
    npm run dev
    ```

`http://localhost:3000`으로 이동하여 앱을 엽니다. 이 경우 기본 설정 브라우저에서 다음 웹 사이트를 열어 볼 수 있습니다.

:::image type="content" source="media/deploy-nuxtjs/start-nuxtjs-app.png" alt-text="Nuxt.js 앱 시작":::

프레임워크/라이브러리를 클릭하면 선택한 항목에 대한 세부 정보 페이지가 표시됩니다.

:::image type="content" source="media/deploy-nuxtjs/start-nuxtjs-details.png" alt-text="자세히 페이지":::

## <a name="generate-a-static-website-from-nuxtjs-build"></a>Nuxt.js 빌드에서 정적 웹 사이트 생성

`npm run build`를 사용하여 Nuxt.js를 빌드하면 앱은 정적 사이트가 아닌 기존 웹앱으로 빌드됩니다. 정적 사이트를 생성하려면 다음 애플리케이션 구성을 사용합니다.

1. `nuxt generate` 명령을 사용하여 정적 사이트만 생성하도록 _package.json_ 의 빌드 스크립트를 업데이트합니다.

    ```json
    "scripts": {
      "dev": "nuxt dev",
      "build": "nuxt generate",
    },
    ```

    이제 이 명령을 사용하면 Static Web Apps는 커밋을 푸시할 때마다 `build` 스크립트를 실행합니다.

1. 정적 사이트를 생성합니다.

    ```bash
    npm run build
    ```

    Nuxt.js는 정적 사이트를 생성하고 작업 디렉터리의 루트에 있는 _dist_ 폴더에 복사합니다.

    > [!NOTE]
    > 이 폴더는 배포할 때 CI/CD에 의해 생성되어야 하므로 _.gitignore_ 파일에 나열됩니다.

## <a name="push-your-static-website-to-github"></a>정적 웹 사이트를 GitHub로 푸시

Azure Static Web Apps는 GitHub 리포지토리에서 앱을 배포하고 지정된 분기에 푸시된 모든 커밋에 대해 이 작업을 계속합니다. 다음 명령을 사용하여 변경 내용을 GitHub에 동기화합니다.

1. 변경된 모든 파일 스테이징:

    ```bash
    git add .
    ```

1. 모든 변경 내용을 커밋합니다.

    ```bash
    git commit -m "Update build config"
    ```

1. GitHub에 변경 내용을 푸시합니다.

    ```bash
    git push origin main
    ```

## <a name="deploy-your-static-website"></a>정적 웹 사이트 배포

다음 단계에서는 GitHub에 방금 푸시한 앱을 Azure Static Web Apps로 연결하는 방법을 보여줍니다. Azure에 있으면 애플리케이션을 프로덕션 환경에 배포할 수 있습니다.

### <a name="create-an-azure-static-web-apps-preview-resource"></a>Azure Static Web Apps 미리 보기 리소스 만들기

1. [Azure Portal](https://portal.azure.com)로 이동합니다.
1. **리소스 만들기** 를 클릭합니다.
1. **Static Web Apps** 를 검색합니다.
1. **Static Web Apps(미리 보기)** 를 클릭합니다.
1. **만들기**

1. *구독* 드롭다운 목록에서 구독을 선택하거나 기본값을 사용합니다.
1. *리소스 그룹* 드롭다운 아래의 **새로 만들기** 링크를 클릭합니다. *새 리소스 그룹 이름* 에 **mystaticsite** 를 입력하고 **확인** 을 클릭합니다.
1. **이름** 텍스트 상자에 앱의 전역적으로 고유한 이름을 입력합니다. 유효한 문자에는 `a-z`, `A-Z`, `0-9` 및 `-`가 포함됩니다. 이 값은 `https://<APP_NAME>.azurestaticapps.net` 형식의 정적 앱에 대한 URL 접두사로 사용됩니다.
1. *지역* 드롭다운에서 가장 가까운 지역을 선택합니다.
1. SKU 드롭다운에서 **무료** 를 선택합니다.

   :::image type="content" source="media/deploy-nuxtjs/create-static-web-app.png" alt-text="Static Web App 만들기":::

### <a name="add-a-github-repository"></a>GitHub 리포지토리 추가

새 Static Web Apps 계정은 Nuxt.js 앱으로 리포지토리에 액세스해야 커밋을 자동으로 배포할 수 있습니다.

1. **GitHub로 로그인 단추** 를 클릭합니다.
1. Nuxt.js 프로젝트의 리포지토리를 만든 **조직** 을 선택합니다. 이는 GitHub 사용자 이름일 수 있습니다.
1. 이전에 만든 리포지토리의 이름을 찾아서 선택합니다.
1. *분기* 드롭다운에서 분기로 **주** 를 선택합니다.

   :::image type="content" source="media/deploy-nuxtjs/connect-github.png" alt-text="GitHub 연결":::

### <a name="configure-the-build-process"></a>빌드 프로세스 구성

Azure Static Web Apps는 각 배포 중에 npm 모듈을 설치하고 `npm run build`를 실행하는 등의 일반적인 작업을 자동으로 수행하도록 빌드되었습니다. 그러나 수동으로 구성해야 하는 애플리케이션 원본 폴더 및 빌드 대상 폴더와 같은 몇 가지 설정이 있습니다.

1. **빌드** 탭을 클릭하여 정적 출력 폴더를 구성합니다.

      :::image type="content" source="media/deploy-nuxtjs/build-tab.png" alt-text="빌드 탭":::

1. *앱 아티팩트 위치* 텍스트 상자에 **dist** 를 입력합니다.

### <a name="review-and-create"></a>검토 및 만들기

1. **검토 + 만들기** 단추를 클릭하여 세부 정보가 모두 올바른지 확인합니다.
1. **만들기** 를 클릭하여 리소스 만들기를 시작하고 배포를 위한 GitHub Action을 프로비저닝합니다.
1. 배포가 완료되면 **리소스로 이동** 을 클릭합니다.
1. _개요_ 창에서 *URL* 링크를 클릭하여 배포된 애플리케이션을 엽니다. 

웹 사이트에서 즉시 로드를 기록하는 경우 백그라운드 GitHub Actions 워크플로가 계속 실행됩니다. 워크플로가 완료되면 브라우저 새로 고침을 클릭하여 웹앱을 볼 수 있습니다.

리포지토리의 작업으로 이동하여 작업 워크플로의 상태를 확인할 수 있습니다.

```url
https://github.com/<YOUR_GITHUB_USERNAME>/nuxtjs-starter/actions
```

### <a name="sync-changes"></a>변경 내용 동기화

앱을 만들 때 Azure Static Web Apps는 리포지토리에 GitHub Actions 워크플로 파일을 만들었습니다. git 기록이 동기화되도록 이 파일을 로컬 리포지토리로 가져와야 합니다.

터미널로 돌아가 다음 `git pull origin main` 명령을 실행합니다.

## <a name="configure-dynamic-routes"></a>동적 경로 구성

새로 배포된 사이트로 이동하여 프레임워크 또는 라이브러리 로고 중 하나를 클릭합니다. 세부 정보 페이지를 가져오는 대신 404 오류 페이지가 표시됩니다.

:::image type="content" source="media/deploy-nuxtjs/404-in-production.png" alt-text="동적 경로의 404 오류":::

그 이유는 Nuxt.js가 홈페이지를 위해서만 정적 사이트를 생성했기 때문입니다. Nuxt.js는 모든 `.vue` 페이지 파일에 대해 동일한 정적 `.html` 파일을 생성할 수 있지만 예외가 있습니다. 

페이지가 동적 페이지인 경우(예: `_id.vue`) 해당 동적 페이지에서 정적 HTML을 생성하는 데 충분한 정보가 없습니다. 동적 경로에 가능한 경로를 명시적으로 제공해야 합니다.

## <a name="generate-static-pages-from-dynamic-routes"></a>동적 경로에서 정적 페이지 생성

1. Nuxt.js가 사용 가능한 모든 데이터 목록을 사용하여 각 프레임워크/라이브러리용 정적 페이지를 생성하도록 _nuxt.config.js_ 파일을 업데이트합니다.

   ```javascript
     import { projects } from "./utils/projectsData";

     export default {
       mode: "universal",

       //...truncated

       generate: {
         async routes() {
           const paths = [];

           projects.forEach(project => {
             paths.push(`/project/${project.slug}`);
           });

           return paths;
         }
       }
     };
   ```

   > [!NOTE]
   > `routes`는 비동기 함수이므로 이 함수에서 API에 대한 요청을 수행하고 반환된 목록을 사용하여 경로를 생성할 수 있습니다.

2. GitHub 리포지토리에 새 변경 내용을 푸시하고 GitHub 작업에서 사이트를 다시 빌드하는 동안 몇 분 정도 기다립니다. 빌드가 완료되면 404 오류가 사라집니다.

   :::image type="content" source="media/deploy-nuxtjs/404-in-production-fixed.png" alt-text="동적 경로의 404 오류 수정":::

> [!div class="nextstepaction"]
> [사용자 지정 도메인 설정](custom-domain.md)
