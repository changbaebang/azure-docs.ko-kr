---
title: '자습서: Azure Static Web Apps에 VuePress 사이트 게시'
description: 이 자습서에서는 Azure Static Web Apps에 VuePress 애플리케이션을 배포하는 방법을 보여줍니다.
services: static-web-apps
author: aaronpowell
ms.service: static-web-apps
ms.topic: tutorial
ms.date: 05/08/2020
ms.author: aapowell
ms.custom: devx-track-js
ms.openlocfilehash: 6f0616df885a7f8fcd76337c810bc368aa02f3c8
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "100650452"
---
# <a name="tutorial-publish-a-vuepress-site-to-azure-static-web-apps-preview"></a>자습서: Azure Static Web Apps 미리 보기에 VuePress 사이트 게시

이 문서에서는 [Azure Static Web Apps](overview.md)에 [VuePress](https://vuepress.vuejs.org/) 웹 애플리케이션을 만들고 배포하는 방법을 보여줍니다. 최종 결과는 앱이 빌드되고 게시되는 방식을 제어하는 관련 GitHub Actions를 포함하는 새로운 Azure Static Web Apps 애플리케이션입니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
>
> - VuePress 앱 만들기
> - Azure Static Web Apps 설정
> - VuePress 앱을 Azure에 배포

## <a name="prerequisites"></a>필수 구성 요소

- 활성 구독이 있는 Azure 계정. 계정이 없는 경우 [체험 계정을 만들](https://azure.microsoft.com/free/) 수 있습니다.
- GitHub 계정. 계정이 없는 경우 [체험 계정을 만들](https://github.com/join) 수 있습니다.
- 설치된 [Node.js](https://nodejs.org).

## <a name="create-a-vuepress-app"></a>VuePress 앱 만들기

CLI(명령줄 인터페이스)에서 VuePress 앱을 만듭니다.

1. VuePress 앱에 대한 새 폴더를 만듭니다.

   ```bash
   mkdir static-site
   ```

1. 폴더에 _README.md_ 파일을 추가합니다.

   ```bash
   echo '# Hello From VuePress' > README.md
   ```

1. _package.json_ 파일을 초기화합니다.

   ```bash
   npm init -y
   ```

1. VuePress를 `devDependency`로 추가합니다.

   ```bash
   npm install --save-dev vuepress
   ```

1. 텍스트 편집기에서 _package.json_ 파일을 열고 [`scripts`](https://docs.npmjs.com/cli-commands/run-script.html) 섹션에 빌드 명령을 추가합니다.

   ```json
   ...
   "scripts": {
       "build": "vuepress build"
   }
   ...
   ```

1. _.gitignore_ 파일을 만들어 _노드\_모듈_ 폴더를 제외합니다.

    ```bash
    echo 'node_modules' > .gitignore
    ```

1. Git 리포지토리를 초기화합니다.

   ```bash
    git init
    git add -A
    git commit -m "initial commit"
   ```

## <a name="push-your-application-to-github"></a>GitHub에 애플리케이션 푸시

Azure Static Web Apps에 연결하려면 GitHub의 리포지토리가 필요합니다. 다음 단계에서는 사이트용 리포지토리를 만드는 방법을 보여줍니다.

1. **vuepress-static-app** 이라는 [https://github.com/new](https://github.com/new)에서 빈 GitHub 리포지토리(추가 정보를 만들지 않음)를 만듭니다.

1. 로컬 리포지토리에 GitHub 리포지토리를 원격으로 추가합니다. 다음 명령에서 `<YOUR_USER_NAME>` 자리 표시자 대신 GitHub 사용자 이름을 추가해야 합니다.

   ```bash
   git remote add origin https://github.com/<YOUR_USER_NAME>/vuepress-static-app
   ```

1. 로컬 리포지토리를 GitHub로 푸시합니다.

   ```bash
   git push --set-upstream origin main
   ```

## <a name="deploy-your-web-app"></a>웹앱 배포

다음 단계에서는 새 Static Web Apps 애플리케이션을 만들어 프로덕션 환경에 배포하는 방법을 보여줍니다.

### <a name="create-the-application"></a>애플리케이션 만들기

1. [Azure Portal](https://portal.azure.com)로 이동합니다.
1. **리소스 만들기** 를 클릭합니다.
1. **Static Web Apps** 를 검색합니다.
1. **Static Web Apps(미리 보기)** 를 클릭합니다.
1. **만들기**

   :::image type="content" source="./media/publish-vuepress/create-in-portal.png" alt-text="포털에서 Static Web Apps(미리 보기) 만들기":::

1. **구독** 의 경우 나열된 구독을 수락하거나 드롭다운 목록에서 새 구독을 선택합니다.

1. _리소스 그룹_ 에서 **새로 만들기** 를 선택합니다. _새 리소스 그룹 이름_ 에서 **vuepress-static-app** 을 입력하고 **확인** 을 선택합니다.

1. 그런 다음, **이름** 상자에 있는 앱 이름을 선택합니다. 유효한 문자에는 `a-z`, `A-Z`, `0-9` 및 `-`가 포함됩니다.

1. _지역_ 에 대해 가까운 사용 가능한 지역을 선택합니다.

1. _SKU_ 에 대해 **무료** 를 선택합니다.

   :::image type="content" source="./media/publish-vuepress/basic-app-details.png" alt-text="세부 정보 입력":::

1. **GitHub로 로그인** 단추를 클릭합니다.

1. 리포지토리를 만든 **조직** 을 선택합니다.

1. **vuepress-static-app** 을 _리포지토리_ 로 선택합니다.

1. _분기_ 에 대해 **기본** 을 선택합니다.

   :::image type="content" source="./media/publish-vuepress/completed-github-info.png" alt-text="완료된 GitHub 정보":::

### <a name="build"></a>빌드

그런 다음, 빌드 프로세스에서 앱을 빌드하는 데 사용하는 구성 설정을 추가합니다. 다음 설정은 GitHub Action 워크플로 파일을 구성합니다.

1. **다음: 빌드 >** 단추를 클릭하여 빌드 구성을 편집합니다.

1. _앱 위치_ 를 **/** 로 설정합니다.

1. _앱 아티팩트 위치_ 를 **.vuepress/dist** 로 설정합니다.

현재 API를 배포하지 않으므로 _API 위치_ 에 대한 값이 필요하지 않습니다.

   :::image type="content" source="./media/publish-vuepress/build-details.png" alt-text="빌드 설정":::

### <a name="review-and-create"></a>검토 및 만들기

1. **검토 + 만들기** 단추를 클릭하여 세부 정보가 모두 올바른지 확인합니다.

1. **만들기** 를 클릭하여 Azure Static Web Apps 만들기를 시작하고 배포를 위한 GitHub Action을 프로비저닝합니다.

1. 배포가 완료되면 **리소스로 이동** 을 클릭합니다.

1. 리소스 화면에서 _URL_ 링크를 클릭하여 배포된 애플리케이션을 엽니다. GitHub Action이 완료되려면 1~2분 정도 기다려야 할 수 있습니다.

   :::image type="content" source="./media/publish-vuepress/deployed-app.png" alt-text="배포된 애플리케이션":::

### <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [사용자 지정 도메인 추가](custom-domain.md)
