---
title: 명령줄에서 C# 함수 만들기 - Azure Functions
description: 명령줄에서 C# 함수를 만든 다음, 로컬 프로젝트를 Azure Functions의 서버리스 호스팅에 게시하는 방법을 알아봅니다.
ms.date: 10/03/2020
ms.topic: quickstart
ms.custom:
- devx-track-csharp
- devx-track-azurecli
adobe-target: true
adobe-target-activity: DocsExp–386541–A/B–Enhanced-Readability-Quickstarts–2.19.2021
adobe-target-experience: Experience B
adobe-target-content: ./create-first-function-cli-csharp-ieux
ms.openlocfilehash: 08b1f2b112542a4b4772744d122ce1260b0edffd
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "101704772"
---
# <a name="quickstart-create-a-c-function-in-azure-from-the-command-line"></a>빠른 시작: 명령줄에서 Azure에 C# 함수 만들기

[!INCLUDE [functions-language-selector-quickstart-cli](../../includes/functions-language-selector-quickstart-cli.md)]

이 문서에서는 명령줄 도구를 사용하여 HTTP 요청에 응답하는 C# 클래스 라이브러리 기반 함수를 만듭니다. 코드를 로컬로 테스트한 후 서버리스 Azure Functions 환경에 배포합니다.

이 빠른 시작을 완료하면 Azure 계정에서 약간의 비용(몇 USD 센트)이 발생합니다.

또한 이 문서의 [Visual Studio Code 기반 버전](create-first-function-vs-code-csharp.md)도 있습니다.

## <a name="configure-your-local-environment"></a>로컬 환경 구성

시작하기 전에 다음이 있어야 합니다.

+ 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).

+ [.NET Core SDK 3.1](https://www.microsoft.com/net/download)

+ [Azure Functions Core Tools](functions-run-local.md#v2) 버전 3.x.

+ 다음 도구 중 하나를 통해 Azure 리소스를 만듭니다.

    + [Azure CLI](/cli/azure/install-azure-cli) 버전 2.4 이상.

    + [Azure PowerShell](/powershell/azure/install-az-ps) 버전 5.0 이상.

### <a name="prerequisite-check"></a>필수 구성 요소 확인

Azure 리소스를 만드는 데 Azure CLI 또는 Azure PowerShell을 사용하는지 여부에 따라 필수 구성 요소를 확인합니다.

# <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)

+ 터미널 또는 명령 창에서 `func --version`을 실행하여 Azure Functions Core Tools가 3.x인지 확인합니다.

+ `az --version`을 실행하여 Azure CLI 버전이 2.4 이상인지 확인합니다.

+ `az login`을 실행하여 Azure에 로그인하고 활성 구독을 확인합니다.

+ `dotnet --list-sdks`를 실행하여 .NET Core SDK 버전 3.1.x가 설치되어 있는지 확인합니다.

# <a name="azure-powershell"></a>[Azure PowerShell](#tab/azure-powershell)

+ 터미널 또는 명령 창에서 `func --version`을 실행하여 Azure Functions Core Tools가 3.x인지 확인합니다.

+ `(Get-Module -ListAvailable Az).Version`을 실행하고 버전 5.0 이상을 확인합니다. 

+ `Connect-AzAccount`을 실행하여 Azure에 로그인하고 활성 구독을 확인합니다.

+ `dotnet --list-sdks`를 실행하여 .NET Core SDK 버전 3.1.x가 설치되어 있는지 확인합니다.

---

## <a name="create-a-local-function-project"></a>로컬 함수 프로젝트 만들기

Azure Functions에서 함수 프로젝트는 각각 특정 트리거에 응답하는 하나 이상의 개별 함수에 대한 컨테이너입니다. 프로젝트의 모든 함수는 동일한 로컬 및 호스팅 구성을 공유합니다. 이 섹션에서는 단일 함수가 포함된 함수 프로젝트를 만듭니다.

1. 다음과 같이 `func init` 명령을 실행하여 지정된 런타임에 *LocalFunctionProj* 폴더에 함수 프로젝트를 만듭니다.  

    ```csharp
    func init LocalFunctionProj --dotnet
    ```

1. 프로젝트 폴더로 이동합니다.

    ```console
    cd LocalFunctionProj
    ```

    이 폴더에는 [local.settings.json](functions-run-local.md#local-settings-file) 및 [host.json](functions-host-json.md)이라는 구성 파일을 포함하여 프로젝트의 다양한 파일이 있습니다. *local.settings.json* 은 Azure에서 다운로드한 비밀을 포함할 수 있으므로 이 파일은 기본적으로 *.gitignore* 파일의 원본 제어에서 제외됩니다.

1. 다음 명령을 사용하여 함수를 프로젝트에 추가합니다. 여기서 `--name` 인수는 함수(HttpExample)의 고유 이름이고, `--template` 인수는 함수의 트리거(HTTP)를 지정합니다.

    ```console
    func new --name HttpExample --template "HTTP trigger" --authlevel "anonymous"
    ``` 

    `func new`는 HttpExample.cs 코드 파일을 만듭니다.

### <a name="optional-examine-the-file-contents"></a>(선택 사항) 파일 내용 검사

원하는 경우 [로컬에서 함수 실행](#run-the-function-locally)으로 건너뛰고, 나중에 파일 내용을 검사할 수 있습니다.

#### <a name="httpexamplecs"></a>HttpExample.cs

*HttpExample.cs* 에는 `req` 변수에 요청 데이터를 수신하는 `Run` 메서드가 포함되며, 트리거 동작을 정의하는 **HttpTriggerAttribute** 로 데코레이트된 [HttpRequest](/dotnet/api/microsoft.aspnetcore.http.httprequest)입니다.

:::code language="csharp" source="~/functions-docs-csharp/http-trigger-template/HttpExample.cs":::

반환 개체는 [OkObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.okobjectresult)(200) 또는 [BadRequestObjectResult](/dotnet/api/microsoft.aspnetcore.mvc.badrequestobjectresult)(400)로 응답 메시지를 반환하는 [ActionResult](/dotnet/api/microsoft.aspnetcore.mvc.actionresult)입니다. 자세한 내용은 [Azure Functions HTTP 트리거 및 바인딩](./functions-bindings-http-webhook.md?tabs=csharp)을 참조하세요.

[!INCLUDE [functions-run-function-test-local-cli](../../includes/functions-run-function-test-local-cli.md)]

[!INCLUDE [functions-create-azure-resources-cli](../../includes/functions-create-azure-resources-cli.md)]

4. Azure에서 함수 앱을 만듭니다.

    # <a name="azure-cli"></a>[Azure CLI](#tab/azure-cli)
        
    ```azurecli
    az functionapp create --resource-group AzureFunctionsQuickstart-rg --consumption-plan-location westeurope --runtime dotnet --functions-version 3 --name <APP_NAME> --storage-account <STORAGE_NAME>
    ```
    
    [az functionapp create](/cli/azure/functionapp#az_functionapp_create) 명령은 Azure에서 함수 앱을 만듭니다. 
    
    # <a name="azure-powershell"></a>[Azure PowerShell](#tab/azure-powershell)
    
    ```azurepowershell
    New-AzFunctionApp -Name <APP_NAME> -ResourceGroupName AzureFunctionsQuickstart-rg -StorageAccount <STORAGE_NAME> -Runtime dotnet -FunctionsVersion 3 -Location 'West Europe'
    ```
    
    [New-AzFunctionApp](/powershell/module/az.functions/new-azfunctionapp) cmdlet은 Azure에서 함수 앱을 만듭니다. 
    
    ---
    
    이전 예제에서는 `<STORAGE_NAME>`을 이전 단계에서 사용한 계정의 이름으로 바꾸고, `<APP_NAME>`을 적절하고 전역적으로 고유한 이름으로 바꿉니다. `<APP_NAME>`은 함수 앱의 기본 DNS 도메인이기도 합니다. 
    
    이 명령은 [Azure Functions 소비 계획](consumption-plan.md)에 따라 지정된 언어 런타임을 실행하는 함수 앱을 만듭니다. 여기서 발생하는 사용량에 대한 비용은 무료입니다. 또한 이 명령은 동일한 리소스 그룹에 연결된 Azure Application Insights 인스턴스를 프로비저닝하여 함수 앱을 모니터링하고 로그를 볼 수 있습니다. 자세한 내용은 [Azure Functions 모니터링](functions-monitoring.md)을 참조하세요. 인스턴스를 활성화할 때까지 비용이 발생하지 않습니다.

[!INCLUDE [functions-publish-project-cli](../../includes/functions-publish-project-cli.md)]

[!INCLUDE [functions-run-remote-azure-cli](../../includes/functions-run-remote-azure-cli.md)]

[!INCLUDE [functions-streaming-logs-cli-qs](../../includes/functions-streaming-logs-cli-qs.md)]

[!INCLUDE [functions-cleanup-resources-cli](../../includes/functions-cleanup-resources-cli.md)]

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Azure Storage 큐에 연결]

[Azure Storage 큐에 연결]: functions-add-output-binding-storage-queue-cli.md?pivots=programming-language-csharp
