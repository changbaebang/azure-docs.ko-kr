---
title: 자습서 - 지역 복제 레지스트리에서 배포
description: 지리적 복제 Azure Container Registry의 컨테이너 이미지를 사용하여 두 개의 다른 Azure 지역에 Linux 기반 웹앱을 배포합니다. 3부로 구성된 시리즈 중 제2부입니다.
ms.topic: tutorial
ms.date: 08/20/2018
ms.custom: seodec18, mvc
ms.openlocfilehash: 7a203bfc9b1317bc258e4a93ae4ac03ecbdc7a15
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92148431"
---
# <a name="tutorial-deploy-a-web-app-from-a-geo-replicated-azure-container-registry"></a>자습서: 지리적 복제 Azure Container Registry에서 웹앱 배포

세 부분으로 이루어진 자습서 시리즈의 두 번째 부분입니다. [1부](container-registry-tutorial-prepare-registry.md)에서 지리적 복제 프라이빗 컨테이너 레지스트리가 작성되었으며 컨테이너 이미지가 원본에서 빌드되어 레지스트리로 푸시되었습니다. 이 문서에서는 서로 다른 두 Azure 지역에 있는 두 웹앱 인스턴스에 컨테이너를 배포하여 지리적 복제 레지스트리의 네트워크-인접 측면을 활용합니다. 그러면 각 인스턴스는 가장 가까운 레지스트리에서 컨테이너 이미지를 가져옵니다.

이 자습서는 시리즈의 2부입니다.

> [!div class="checklist"]
> * 두 개의 *Web App for Containers* 인스턴스에 컨테이너 이미지 배포
> * 배포된 애플리케이션 확인

지리적 복제 레지스트리를 아직 만들지 않았고 컨테이너화된 샘플 애플리케이션의 이미지를 레지스트리에 푸시한 경우 시리즈의 이전 자습서인 [지리적 복제 Azure Container Registry 준비](container-registry-tutorial-prepare-registry.md)로 돌아갑니다.

이 시리즈의 그 다음 문서에서는 애플리케이션을 업데이트한 다음, 업데이트된 컨테이너 이미지를 레지스트리로 푸시합니다. 마지막으로, 실행 중인 각 웹앱 인스턴스를 탐색하여 변경 사항이 자동으로 적용되어 Azure Container Registry 지역에서 복제 및 webhook가 실제로 작동하고 있음을 보여 줍니다.

## <a name="automatic-deployment-to-web-apps-for-containers"></a>Web App for Containers에 자동 배포

Azure Container Registry는 컨테이너화된 애플리케이션을 [Web App for Containers](../app-service/index.yml)에 직접 배포할 수 있도록 지원합니다. 이 자습서에서는 Azure Portal을 사용하여 이전 자습서에서 만든 컨테이너 이미지를 다른 Azure 영역에 있는 두 개의 웹앱 계획에 배포합니다.

레지스트리의 컨테이너 이미지에서 웹앱을 배포하고 같은 영역에 지리적 복제 레지스트리가 있는 경우 Azure Container Registry는 이미지 배포 [webhook](container-registry-webhook.md)를 만듭니다. 새 이미지를 컨테이너 리포지토리로 푸시하면 webhook가 변경 사항을 선택하고 새 컨테이너 이미지를 웹앱에 자동으로 배포합니다.

## <a name="deploy-a-web-app-for-containers-instance"></a>Web App for Containers 인스턴스 배포

이 단계에서는 *미국 서부* 영역에 Web App for Containers를 만듭니다.

[Azure Portal](https://portal.azure.com)에 로그인하고 이전 자습서에서 만든 레지스트리로 이동합니다.

**리포지토리** > **acr-helloworld** 를 선택하고 **태그** 의 **v1** 태그를 마우스 오른쪽 단추로 클릭한 다음 **웹앱에 배포** 를 선택합니다.

![Azure Portal에서 App Service에 배포][deploy-app-portal-01]

"웹앱에 배포"를 사용하지 않도록 설정된 경우 첫 번째 자습서의 [컨테이너 레지스트리 만들기](container-registry-tutorial-prepare-registry.md#create-a-container-registry)에 설명된 대로 레지스트리 관리 사용자를 사용하도록 설정하지 않은 것일 수 있습니다. Azure Portal의 **설정** > **액세스 키** 에서 관리 사용자를 사용하도록 설정할 수 있습니다.

"웹앱에 배포"를 선택하면 표시되는 **컨테이너용 웹앱** 에서 각 설정에 대해 다음 값을 지정합니다.

| 설정 | 값 |
|---|---|
| **사이트 이름** | 웹앱에 대한 전역적으로 고유한 이름입니다. 이 예제에서는 `<acrName>-westus` 형식을 사용하여 웹앱이 배포된 레지스트리 및 영역을 쉽게 식별합니다. |
| **리소스 그룹** | **기존 항목 사용** > `myResourceGroup` |
| **App Service 계획/위치** | **미국 서부** 영역에 `plan-westus`라는 새 계획을 만듭니다. |
| **이미지** | `acr-helloworld:v1` |
| **운영 체제** | Linux |

> [!NOTE]
> 컨테이너형 앱을 배포하기 위한 새 앱 서비스 계획을 만들 때 애플리케이션을 호스팅하기 위한 기본 계획이 자동으로 선택됩니다. 기본 계획은 운영 체제 설정에 따라 달라집니다.

웹앱을 *미국 서부* 영역에 프로비저닝하려면 **만들기** 를 선택합니다.

![스크린샷은 만들기 단추가 강조 표시된 Web App for Containers를 보여줍니다.][deploy-app-portal-02]

## <a name="view-the-deployed-web-app"></a>배포된 웹앱 보기

배포가 완료되면 브라우저에서 해당 URL로 이동하여 실행 중인 애플리케이션을 볼 수 있습니다.

포털에서 **App Services** 를 선택한 다음 이전 단계에서 프로비저닝된 웹앱을 선택합니다. 이 예제에서 웹앱 이름은 *uniqueregistryname-westus* 입니다.

브라우저에서 실행 중인 애플리케이션을 보려면 **App Service** 개요의 오른쪽 위에 있는 웹앱의 하이퍼링크 URL을 선택합니다.

![스크린샷은 웹앱 URL이 강조 표시된 App Service 개요를 보여줍니다.][deploy-app-portal-04]

Docker 이미지가 지리적 복제 컨테이너 레지스트리에서 배포되면 사이트에서 컨테이너 레지스트리를 호스팅하는 Azure 영역을 나타내는 이미지를 표시합니다.

![스크린샷은 브라우저에 표시되는 배포된 웹 애플리케이션을 보여줍니다.][deployed-app-westus]

## <a name="deploy-second-web-app-for-containers-instance"></a>두 번째 Web App for Containers 인스턴스 배포

이전 섹션에서 설명한 절차를 사용하여 *미국 동부* 영역에 두 번째 웹앱을 배포합니다. **Web App for Containers** 에서 다음 값을 지정합니다.

| 설정 | 값 |
|---|---|
| **사이트 이름** | 웹앱에 대한 전역적으로 고유한 이름입니다. 이 예제에서는 `<acrName>-eastus` 형식을 사용하여 웹앱이 배포된 레지스트리 및 영역을 쉽게 식별합니다. |
| **리소스 그룹** | **기존 항목 사용** > `myResourceGroup` |
| **App Service 계획/위치** | **미국 동부** 영역에 `plan-eastus`라는 새 계획을 만듭니다. |
| **이미지** | `acr-helloworld:v1` |
| **운영 체제** | Linux |

웹앱을 *미국 동부* 영역에 프로비저닝하려면 **만들기** 를 선택합니다.

![스크린샷은 만들기 단추가 강조 표시된 Web App for Containers 만들기 창을 보여줍니다.][deploy-app-portal-06]

## <a name="view-the-second-deployed-web-app"></a>두 번째로 배포된 웹앱 보기

이전과 마찬가지로 브라우저에서 해당 URL로 이동하여 실행 중인 애플리케이션을 볼 수 있습니다.

포털에서 **App Services** 를 선택한 다음 이전 단계에서 프로비저닝된 웹앱을 선택합니다. 이 예제에서 웹앱 이름은 *uniqueregistryname-eastus* 입니다.

브라우저에서 실행 중인 애플리케이션을 보려면 **App Service 개요** 의 오른쪽 위에 있는 웹앱의 하이퍼링크 URL을 선택합니다.

![Azure Portal에서 Linux의 웹앱 구성][deploy-app-portal-07]

Docker 이미지가 지리적 복제 컨테이너 레지스트리에서 배포되면 사이트에서 컨테이너 레지스트리를 호스팅하는 Azure 영역을 나타내는 이미지를 표시합니다.

![브라우저에 표시된 배포된 웹 애플리케이션][deployed-app-eastus]

## <a name="next-steps"></a>다음 단계

이 자습서에서는 지리적 복제 Azure Container Registry에서 Web App for Containers 인스턴스 2개를 배포했습니다.

다음 자습서로 이동하여 새 컨테이너 이미지를 업데이트하고 컨테이너 레지스트리에 배포한 다음 두 영역에서 실행 중인 웹앱이 자동으로 업데이트되었는지 확인합니다.

> [!div class="nextstepaction"]
> [지리적 복제 컨테이너 이미지에 업데이트 배포](./container-registry-tutorial-deploy-update.md)

<!-- IMAGES -->
[deploy-app-portal-01]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-01.png
[deploy-app-portal-02]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-02.png
[deploy-app-portal-03]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-03.png
[deploy-app-portal-04]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-04.png
[deploy-app-portal-05]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-05.png
[deploy-app-portal-06]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-06.png
[deploy-app-portal-07]: ./media/container-registry-tutorial-deploy-app/deploy-app-portal-07.png
[deployed-app-westus]: ./media/container-registry-tutorial-deploy-app/deployed-app-westus.png
[deployed-app-eastus]: ./media/container-registry-tutorial-deploy-app/deployed-app-eastus.png