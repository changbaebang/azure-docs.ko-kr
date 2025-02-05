---
title: Azure Pipelines를 사용한 연속 통합
description: ARM 템플릿(Azure Resource Manager 템플릿)을 지속적으로 빌드, 테스트 및 배포하는 방법을 알아봅니다.
ms.date: 03/02/2021
ms.topic: tutorial
ms.author: jgao
ms.openlocfilehash: 3ff98c1c033c6da4b6bdf40c3b8ecb3347601741
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "101722819"
---
# <a name="tutorial-continuous-integration-of-arm-templates-with-azure-pipelines"></a>자습서: ARM 템플릿과 Azure Pipelines의 연속 통합

[이전 자습서](./deployment-tutorial-linked-template.md)에서 연결된 템플릿을 배포합니다.  이 자습서에서는 Azure Pipelines를 사용하여 ARM 템플릿(Azure Resource Manager 템플릿) 프로젝트를 지속적으로 빌드하고 배포하는 방법에 대해 알아봅니다.

Azure DevOps는 팀이 작업을 계획하고, 협업을 통해 코드를 개발하고, 애플리케이션을 빌드하여 배포할 수 있도록 지원하는 개발자 서비스를 제공합니다. 개발자는 Azure DevOps Services를 사용하여 클라우드에서 작업할 수 있습니다. Azure DevOps는 웹 브라우저 또는 IDE 클라이언트를 통해 액세스할 수 있는 통합 기능 세트를 제공합니다. Azure 파이프라인은 이러한 기능 중 하나입니다. Azure Pipelines는 모든 기능을 갖춘 CI(지속적인 통합) 및 CD(지속적인 업데이트) 서비스입니다. 선호하는 Git 공급자와 함께 작동하며 대부분의 주요 클라우드 서비스에 배포할 수 있습니다. 그런 다음, 코드를 빌드하고, 테스트하고, Microsoft Azure, Google Cloud Platform 또는 Amazon Web Services에 배포하는 프로세스를 자동화할 수 있습니다.

> [!NOTE]
> 프로젝트 이름을 선택합니다. 자습서를 진행할 때 **AzureRmPipeline** 을 프로젝트 이름으로 바꿔야 합니다.
> 이 프로젝트 이름은 리소스 이름을 생성하는 데 사용됩니다.  리소스 중 하나는 스토리지 계정입니다. Storage 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 사용해야 합니다. 이름은 고유해야 합니다. 템플릿에서 스토리지 계정 이름은 **store** 가 추가된 프로젝트 이름이며, 프로젝트 이름은 3-11자 사이여야 합니다. 따라서 프로젝트 이름은 스토리지 계정 이름 요구 사항을 충족해야 하며 11자 미만이어야 합니다.

이 자습서에서 다루는 작업은 다음과 같습니다.

> [!div class="checklist"]
> * GitHub 리포지토리 준비
> * Azure DevOps 프로젝트 만들기
> * Azure 파이프라인 만들기
> * 파이프라인 배포 확인
> * 템플릿을 업데이트하고 다시 배포
> * 리소스 정리

Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 구성 요소

이 문서를 완료하려면 다음이 필요합니다.

* 템플릿의 리포지토리를 만드는 데 사용할 **GitHub 계정**. 계정이 없는 경우 [체험 계정](https://github.com)을 만들 수 있습니다. GitHub 리포지토리 사용에 대한 자세한 내용은 [GitHub 리포지토리 빌드](/azure/devops/pipelines/repos/github)를 참조하세요.
* **Git를 설치** 합니다. 이 자습서의 지침에서는 *Git Bash* 또는 *Git Shell* 을 사용합니다. 지침은 [Git 설치](https://www.atlassian.com/git/tutorials/install-git)를 참조하세요.
* **Azure DevOps 조직**. 조직이 없는 경우 무료로 만들 수 있습니다. [조직 또는 프로젝트 컬렉션 만들기](/azure/devops/organizations/accounts/create-organization)를 참조하세요.
* (선택 사항)**Resource Manager 도구 확장이 포함된 Visual Studio Code**. [빠른 시작: Visual Studio Code를 사용하여 ARM 템플릿 만들기](quickstart-create-templates-use-visual-studio-code.md)를 참조하세요.

## <a name="prepare-a-github-repository"></a>GitHub 리포지토리 준비

GitHub는 Resource Manager 템플릿을 비롯한 프로젝트 소스 코드를 저장하는 데 사용됩니다. 지원되는 다른 리포지토리에 대한 내용은 [Azure DevOps에서 지원하는 리포지토리](/azure/devops/pipelines/repos/)를 참조하세요.

### <a name="create-a-github-repository"></a>GitHub 리포지토리 만들기

GitHub 계정이 없는 경우 [사전 요구 사항](#prerequisites)을 참조하세요.

1. [GitHub](https://github.com)에 로그인합니다.
1. 오른쪽 위 모서리에서 계정 이미지를 선택한 다음, **해당 리포지토리** 를 선택합니다.

    ![Azure Resource Manager Azure DevOps Azure Pipelines GitHub 리포지토리 만들기](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-github-repository.png)

1. 녹색 **새로 만들기** 단추를 선택합니다.
1. **리포지토리 이름** 에서 리포지토리 이름을 입력합니다.  예: **AzureRmPipeline-repo**. **AzureRmPipeline** 을 프로젝트 이름으로 바꿉니다. 이 자습서를 **공개** 로 진행할 것인지 아니면 **프라이빗** 으로 진행할 것인지 선택할 수 있습니다. 그런 다음, **리포지토리 만들기** 를 선택합니다.
1. URL을 적어 둡니다. 리포지토리 URL은 다음과 같은 형식입니다. - `https://github.com/[YourAccountName]/[YourRepositoryName]`

이 리포지토리를 *원격 리포지토리* 라고 합니다. 같은 프로젝트를 작업하는 각 개발자는 자신의 *로컬 리포지토리* 를 복제하고, 변경 내용을 원격 리포지토리에 병합할 수 있습니다.

### <a name="clone-the-remote-repository"></a>원격 리포지토리 복제

1. Git Shell 또는 Git Bash를 엽니다. [필수 조건](#prerequisites)을 참조하세요.
1. 현재 폴더가 **GitHub** 인지 확인합니다.
1. 다음 명령을 실행합니다.

    ```bash
    git clone https://github.com/[YourAccountName]/[YourGitHubRepositoryName]
    cd [YourGitHubRepositoryName]
    mkdir CreateWebApp
    cd CreateWebApp
    pwd
    ```

    `[YourAccountName]` 을 해당 GitHub 계정 이름으로 바꾸고, `[YourGitHubRepositoryName]` 을 이전 절차에서 만든 리포지토리 이름으로 바꿉니다.

_CreateWebApp_ 폴더는 템플릿이 저장되는 폴더입니다. `pwd` 명령은 폴더 경로를 보여줍니다. 경로는 다음 절차에 따라 템플릿을 저장하는 위치입니다.

### <a name="download-a-quickstart-template"></a>빠른 시작 템플릿 다운로드

템플릿을 만드는 대신 템플릿을 다운로드하여 _CreateWebApp_ 폴더에 저장할 수 있습니다.

* 기본 템플릿: https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/get-started-deployment/linked-template/azuredeploy.json
* 연결된 템플릿: https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/get-started-deployment/linked-template/linkedStorageAccount.json

폴더 이름과 파일 이름은 모두 파이프라인에 있는 그대로 사용됩니다. 이러한 이름을 변경할 경우 파이프라인에서 사용되는 이름을 업데이트해야 합니다.

### <a name="push-the-template-to-the-remote-repository"></a>원격 리포지토리에 템플릿 푸시

_azuredeploy.json_ 이 로컬 리포지토리에 추가되었습니다. 다음으로, 템플릿을 원격 리포지토리에 업로드합니다.

1. *Git Shell* 또는 *Git Bash* 가 열려 있지 않으면 지금 엽니다.
1. 디렉터리를 로컬 리포지토리의 _CreateWebApp_ 폴더로 변경합니다.
1. _azuredeploy.json_ 파일이 이 폴더에 있는지 확인합니다.
1. 다음 명령을 실행합니다.

    ```bash
    git add .
    git commit -m "Add web app templates."
    git push origin main
    ```

    LF에 대한 경고가 발생할 수 있습니다. 경고를 무시해도 됩니다. **main** 은 기본 분기입니다.  일반적으로 각 업데이트에 대한 분기를 만듭니다. 자습서를 간소화하려면 기본 분기를 직접 사용합니다.

1. 브라우저에서 GitHub 리포지토리를 찾습니다. URL은 `https://github.com/[YourAccountName]/[YourGitHubRepository]`입니다. _CreateWebApp_ 폴더와 이 폴더 내의 두 개의 파일이 표시됩니다.
1. _azuredeploy.json_ 을 선택하여 템플릿을 엽니다.
1. **원시** 단추를 선택합니다. URL은 `https://raw.githubusercontent.com`으로 시작합니다.
1. URL 복사본을 만듭니다. 이 값은 나중에 자습서에서 파이프라인을 구성할 때 제공해야 합니다.

지금까지 GitHub 리포지토리를 만들고, 템플릿을 리포지토리에 업로드했습니다.

## <a name="create-a-devops-project"></a>DevOps 프로젝트 만들기

다음 절차를 진행하려면 DevOps 조직이 필요합니다. 조직이 없는 경우 [사전 요구 사항](#prerequisites)을 참조하세요.

1. [Azure DevOps](https://dev.azure.com)에 로그인합니다.
1. 왼쪽에서 DevOps 조직을 선택합니다.

    ![Azure Resource Manager Azure DevOps Azure Pipelines Azure DevOps 프로젝트 만들기](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-create-devops-project.png)

1. **새 프로젝트** 를 선택합니다. 프로젝트가 하나도 없는 경우 [프로젝트 만들기] 페이지가 자동으로 열립니다.
1. 다음 값을 입력합니다.

    * **프로젝트 이름**: 프로젝트 이름을 입력합니다. 자습서를 시작할 때 선택한 프로젝트 이름을 사용해도 됩니다.
    * **버전 제어**: **Git** 를 선택합니다. **버전 제어** 를 보려면 **고급** 을 확장해야 할 수도 있습니다.

    그 외의 속성은 기본값을 사용합니다.
1. **만들기** 를 선택합니다.

Azure에 프로젝트를 배포하는 데 사용되는 서비스 연결을 만듭니다.

1. 왼쪽 메뉴의 맨 아래에서 **프로젝트 설정** 을 선택합니다.
1. **파이프라인** 아래에서 **서비스 연결** 을 선택합니다.
1. **서비스 연결 만들기**, **Azure Resource Manager**, **다음** 을 차례로 선택합니다.
1. **서비스 주체**, **다음** 을 차례로 선택합니다.
1. 다음 값을 입력합니다.

    * **범위 수준**: **Subscription** 을 선택합니다.
    * **구독**: 해당 구독을 선택합니다.
    * **리소스 그룹**: 비워 둠
    * **연결 이름**: 연결 이름을 입력합니다. 예: **AzureRmPipeline-conn**. 이 이름을 적어 둡니다. 파이프라인을 만들 때 이 이름이 필요합니다.
    * **모든 파이프라인에 액세스 권한 부여** (선택됨)
1. **저장** 을 선택합니다.

## <a name="create-a-pipeline"></a>파이프라인 만들기

지금까지 다음 작업을 완료했습니다.  GitHub 및 DevOps에 익숙해서 이전 섹션을 건너뛴 경우 다음 작업을 완료해야만 계속 진행할 수 있습니다.

* GitHub 리포지토리를 만들고, 템플릿을 리포지토리의 _CreateWebApp_ 폴더에 저장합니다.
* DevOps 프로젝트를 만들고, Azure Resource Manager 서비스 연결을 만듭니다.

템플릿을 배포하는 단계를 사용하여 파이프라인을 만들려면 다음을 수행합니다.

1. 왼쪽 메뉴에서 **파이프라인** 을 선택합니다.
1. **파이프라인 만들기** 를 선택합니다.
1. **연결** 탭에서 **GitHub** 를 선택합니다. GitHub 자격 증명을 입력하라는 메시지가 표시되면 입력하고 그 다음 지침을 따릅니다. 다음 화면이 표시되면 **리포지토리만 선택** 을 선택하고, 리포지토리가 목록에 있는지 확인한 다음, **승인 및 설치** 를 선택합니다.

    ![Azure Resource Manager Azure DevOps Azure Pipelines 리포지토리만 선택](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-only-select-repositories.png)

1. **선택** 탭에서 리포지토리를 선택합니다. 기본 이름은 `[YourAccountName]/[YourGitHubRepositoryName]`입니다.
1. **구성** 탭에서 **시작 파이프라인** 을 선택합니다. 두 스크립트 단계가 있는 _azure-pipelines.yml_ 파이프라인 파일이 표시됩니다.
1. _.yml_ 파일에서 두 스크립트 단계를 삭제합니다.
1. 커서를 **steps:** 뒤의 줄로 이동합니다.
1. 화면 오른쪽에서 **도우미 표시** 를 선택하여 **작업** 창을 엽니다.
1. **ARM 템플릿 배포** 를 선택합니다.
1. 다음 값을 입력합니다.

    * **deploymentScope**: **리소스 그룹** 을 선택합니다. 범위에 대해 자세히 알아보려면 [배포 범위](deploy-rest.md#deployment-scope)를 참조하세요.
    * **Azure Resource Manager 연결**: 이전에 만든 서비스 연결 이름을 선택합니다.
    * **구독**:  대상 구독 ID를 지정합니다.
    * **작업**: **리소스 그룹 만들기 또는 업데이트** 작업을 선택합니다. 이 경우 두 가지 작업을 수행합니다. 1. 새 리소스 그룹 이름이 제공되면 리소스 그룹을 만듭니다. 2. 지정된 템플릿을 배포합니다.
    * **리소스 그룹**: 새 리소스 그룹 이름을 입력합니다. 예: **AzureRmPipeline-rg**.
    * **위치**: 리소스 그룹의 위치를 선택합니다(예: **미국 중부**).
    * **템플릿 위치**: **파일의 URL** 을 선택합니다. 이는 작업이 URL을 사용하여 템플릿 파일을 찾는다는 것을 의미합니다. _relativePath_ 는 기본 템플릿에서 사용되고 _relativePath_ 는 URI 기반 배포에서만 지원되므로 여기에서 URL을 사용해야 합니다.
    * **템플릿 링크**: [GitHub 저장소 준비](#prepare-a-github-repository) 섹션의 끝에서 받은 URL을 입력합니다. `https://raw.githubusercontent.com` 로 시작합니다.
    * **템플릿 매개 변수 링크**: 이 필드는 비워 둡니다. 매개 변수 값을 **템플릿 매개 변수 재정의** 에 지정합니다.
    * **템플릿 매개 변수 재정의**: `-projectName [EnterAProjectName]` 을 입력합니다.
    * **배포 모드**: **증분** 을 선택합니다.
    * **배포 이름**: **DeployPipelineTemplate** 을 입력합니다. **배포 이름** 을 표시하려면 **고급** 을 선택합니다.

    ![스크린샷은 필수 값이 입력된 ARM 템플릿 배포 페이지를 보여줍니다.](./media/deployment-tutorial-pipeline/resource-manager-template-pipeline-configure.png)

1. **추가** 를 선택합니다.

    작업에 대한 자세한 내용은 [Azure Resource Group 배포 작업](/azure/devops/pipelines/tasks/deploy/azure-resource-group-deployment) 및 [Azure Resource Manager 템플릿 배포 작업](https://github.com/microsoft/azure-pipelines-tasks/blob/master/Tasks/AzureResourceManagerTemplateDeploymentV3/README.md)을 참조하세요.

    _.yml_ 파일은 다음과 비슷해야 합니다.

    ![스크린샷은 [파이프라인 YAML 검토]라는 제목의 새 파이프라인이 있는 검토 페이지를 보여줍니다.](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-yml.png)

1. **저장 및 실행** 을 선택합니다.
1. **저장 및 실행** 창에서 **저장 및 실행** 을 다시 선택합니다. 연결된 리포지토리에 YAML 파일의 복사본이 저장됩니다. 리포지토리로 이동하면 YAML 파일을 볼 수 있습니다.
1. 파이프라인이 성공적으로 실행되는지 확인합니다.

    ![Azure Resource Manager Azure DevOps Azure Pipelines yaml](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-status.png)

## <a name="verify-the-deployment"></a>배포 확인

1. [Azure Portal](https://portal.azure.com)에 로그인합니다.
1. 리소스 그룹을 엽니다. 이름은 파이프라인 YAML 파일에서 지정한 이름입니다. 스토리지 계정이 하나 만들어진 것이 보입니다. 스토리지 계정 이름은 **store** 로 시작합니다.
1. 스토리지 계정 이름을 선택하여 엽니다.
1. **속성** 을 선택합니다. **복제** 는 **LRS(로컬 중복 스토리지)** 입니다.

## <a name="update-and-redeploy"></a>업데이트 및 다시 배포

템플릿을 업데이트하고 변경 내용을 원격 리포지토리에 푸시하면 파이프라인이 자동으로 리소스(이 예에서는 스토리지 계정)를 업데이트합니다.

1. Visual Studio Code 또는 텍스트 편집기의 로컬 리포지토리에서 _linkedStorageAccount.json_ 을 엽니다.
1. **storageAccountType** 의 **defaultValue** 를 **Standard_GRS** 로 업데이트합니다. 다음 스크린샷을 참조하세요.

    ![Azure Resource Manager Azure DevOps Azure Pipelines yaml 업데이트](./media/deployment-tutorial-pipeline/azure-resource-manager-devops-pipelines-update-yml.png)

1. 변경 내용을 저장합니다.
1. Git Bash/Shell에서 다음 명령을 실행하여 원격 리포지토리에 변경 내용을 푸시합니다.

    ```bash
    git pull origin main
    git add .
    git commit -m "Update the storage account type."
    git push origin main
    ```

    첫 번째 명령(`pull`)은 로컬 리포지토리를 원격 리포지토리와 동기화합니다. 파이프라인 YAML 파일이 원격 리포지토리에만 추가되었습니다. `pull` 명령을 실행하면 YAML 파일의 복사본이 로컬 분기로 다운로드됩니다.

    네 번째 명령(`push`)은 수정된 _linkedStorageAccount.json_ 파일을 원격 리포지토리에 업로드합니다. 원격 리포지토리의 기본 분기가 업데이트되었으므로 파이프라인이 다시 실행됩니다.

변경 내용을 확인하려면 스토리지 계정의 복제 속성을 확인하면 됩니다. [배포 확인](#verify-the-deployment)을 참조하세요.

## <a name="clean-up-resources"></a>리소스 정리

Azure 리소스가 더 이상 필요하지 않은 경우 리소스 그룹을 삭제하여 배포한 리소스를 정리합니다.

1. Azure Portal의 왼쪽 메뉴에서 **리소스 그룹** 을 선택합니다.
2. **이름으로 필터링** 필드에서 리소스 그룹 이름을 입력합니다.
3. 해당 리소스 그룹 이름을 선택합니다.
4. 위쪽 메뉴에서 **리소스 그룹 삭제** 를 선택합니다.

GitHub 리포지토리 및 Azure DevOps 프로젝트를 삭제할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

축하합니다! 이 Resource Manager 템플릿 배포 자습서를 완료했습니다. 의견이나 제안 사항이 있으면 사용자 의견 섹션에서 알려주십시오. 감사합니다.
템플릿에 대한 고급 개념을 자세히 살펴볼 준비가 되었습니다. 다음 자습서에서는 배포할 리소스를 정의하는 데 유용한 템플릿 참조 설명서를 사용하는 방법에 대해 자세히 설명합니다.

> [!div class="nextstepaction"]
> [템플릿 참조 활용](./template-tutorial-use-template-reference.md)
