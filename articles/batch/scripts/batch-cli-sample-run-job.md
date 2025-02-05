---
title: Azure CLI 스크립트 예제 - Batch 작업 실행
description: 이 스크립트는 Batch 작업을 만들고 일련의 태스크를 작업에 추가합니다. 또한 작업 및 태스크를 모니터링하는 방법도 보여 줍니다.
ms.topic: sample
ms.date: 12/12/2019
ms.custom: devx-track-azurecli
ms.openlocfilehash: b67925f48a9d2dbe0b4559d46d783b500e7a0773
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "93100918"
---
# <a name="cli-example-run-a-job-and-tasks-with-azure-batch"></a>CLI 예제: Azure Batch로 작업 및 태스크 실행

이 스크립트는 Batch 작업을 만들고 일련의 태스크를 작업에 추가합니다. 또한 작업 및 태스크를 모니터링하는 방법도 보여 줍니다. 

[!INCLUDE [azure-cli-prepare-your-environment.md](../../../includes/azure-cli-prepare-your-environment.md)]

- 이 자습서에는 Azure CLI 버전 2.0.20 이상이 필요합니다. Azure Cloud Shell을 사용하는 경우 최신 버전이 이미 설치되어 있습니다. 

## <a name="example-script"></a>예제 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-deployment"></a>배포 정리

다음 명령을 실행하여 리소스 그룹 및 모든 관련 리소스를 제거합니다.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group#az-group-create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az batch account create](/cli/azure/batch/account#az-batch-account-create) | Batch 계정을 만듭니다. |
| [az batch account login](/cli/azure/batch/account#az-batch-account-login) | 추가 CLI 상호 작용을 위해 지정된 Batch 계정에 대해 인증합니다.  |
| [az batch pool create](/cli/azure/batch/pool#az-batch-pool-create) | 컴퓨팅 노드 풀을 만듭니다.  |
| [az batch job create](/cli/azure/batch/job#az-batch-job-create) | Batch 작업을 만듭니다.  |
| [az batch task create](/cli/azure/batch/task#az-batch-task-create) | 지정된 Batch 작업에 태스크를 추가합니다.  |
| [az batch job set](/cli/azure/batch/job#az-batch-job-set) | Batch 작업의 속성을 업데이트합니다.  |
| [az batch job show](/cli/azure/batch/job#az-batch-job-show) | 지정된 Batch 작업의 세부 정보를 검색합니다.  |
| [az batch task show](/cli/azure/batch/task#az-batch-task-show) | 지정된 Batch 작업에서 태스크의 세부 정보를 검색합니다.  |
| [az group delete](/cli/azure/group#az-group-delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.
