---
title: 서버리스 Python 함수 앱 만들기 - Azure CLI
description: Azure CLI를 사용하여 서버리스 Python 함수 앱 만들기
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.topic: sample
ms.date: 11/23/2019
ms.custom: devx-track-python, devx-track-azurecli
ms.openlocfilehash: 65ea6513046cd0372720e5a9438941dda2a74877
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97934359"
---
# <a name="create-a-serverless-python-function-app-using-azure-cli"></a>Azure CLI를 사용하여 서버리스 Python 함수 앱 만들기

이 Azure Functions 샘플 스크립트는 함수의 컨테이너인 함수 앱을 만듭니다. 

>[!NOTE]
>생성된 함수 앱은 Python 버전 3.6에서 실행됩니다. Python 버전 3.7은 Azure Functions 에서도 지원됩니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](../../../includes/azure-cli-prepare-your-environment.md)]

 - 이 자습서에는 Azure CLI 버전 2.0 이상이 필요합니다. Azure Cloud Shell을 사용하는 경우 최신 버전이 이미 설치되어 있습니다. 

## <a name="sample-script"></a>샘플 스크립트

이 스크립트는 [소비 계획](../consumption-plan.md)을 사용하는 Azure 함수 앱을 만듭니다.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption-python/create-function-app-consumption-python.sh "Create an Azure Function on a Consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다. 이 스크립트는 다음 명령을 사용합니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az storage account create](/cli/azure/storage/account#az-storage-account-create) | Azure Storage 계정을 만듭니다. |
| [az functionapp create](/cli/azure/functionapp#az-functionapp-create) | 함수 앱을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.

추가 Azure Functions CLI 스크립트 샘플은 [Azure Functions 설명서](../functions-cli-samples.md)에서 확인할 수 있습니다.
