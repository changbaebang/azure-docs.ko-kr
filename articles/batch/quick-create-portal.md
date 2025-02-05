---
title: Azure 빠른 시작 - Azure Portal에서 첫 번째 Batch 작업 실행
description: 이 빠른 시작에서는 Azure Portal을 사용하여 Batch 계정, 컴퓨팅 노드의 풀 및 풀에서 기본 태스크를 실행하는 작업을 만드는 방법을 보여줍니다.
ms.topic: quickstart
ms.date: 08/17/2020
ms.custom: mvc
ms.openlocfilehash: 1234a932a732cdb6fda1c412a423ae0b1ea089e9
ms.sourcegitcommit: 24a12d4692c4a4c97f6e31a5fbda971695c4cd68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102184018"
---
# <a name="quickstart-run-your-first-batch-job-in-the-azure-portal"></a>빠른 시작: Azure Portal에서 첫 번째 Batch 작업 실행

Azure Portal을 사용하여 Batch 계정, 컴퓨팅 노드 풀(가상 머신) 및 풀에서 태스크를 실행하는 작업을 만들어 Azure Batch를 시작합니다. 이 빠른 시작을 완료하면, Batch 서비스의 주요 개념을 이해하고 더 큰 규모의 더 실제적인 작업으로 Batch를 시도할 준비가 됩니다.

## <a name="prerequisites"></a>사전 요구 사항

- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

## <a name="create-a-batch-account"></a>Batch 계정 만들기

다음 단계에 따라 테스트용 배치 계정 샘플을 만듭니다. 풀 및 작업을 만들려면 배치 계정이 필요합니다. 여기서 보여 주듯이 Azure Storage 계정과 배치 계정을 연결할 수 있습니다. 스토리지 계정은 이 빠른 시작에서 필요하지 않지만, 애플리케이션을 배포하고 대부분의 실제 작업에 대한 입력 및 출력 데이터를 저장하는 데 유용합니다.

1. [Azure Portal](https://portal.azure.com)에서 **리소스 만들기** > **Compute** > **Batch Service** 를 선택합니다. 

   :::image type="content" source="media/quick-create-portal/marketplace-batch.png" alt-text="Azure Marketplace의 Batch Service 스크린샷.":::

1. **리소스 그룹** 필드에서 **새로 만들기** 를 선택하고 리소스 그룹의 이름을 입력합니다.

1. **계정 이름** 에 대한 값을 입력합니다. 이 이름은 선택한 Azure **위치** 내에서 고유해야 합니다. 소문자와 숫자만 포함할 수 있으며, 3-24자 사이여야 합니다.

1. **스토리지 계정** 에서 기존 스토리지 계정을 선택하거나 새 스토리지 계정을 만듭니다.

1. 다른 설정은 변경하지 마세요. **검토 + 만들기** 를 선택한 다음, **만들기** 를 선택하여 Batch 계정을 만듭니다.

**배포 성공** 메시지가 표시되면 생성한 Batch 계정으로 이동합니다.

## <a name="create-a-pool-of-compute-nodes"></a>컴퓨팅 노드 풀 만들기

이제 배치 계정이 있으므로 테스트를 위해 Windows 컴퓨팅 노드의 샘플 풀을 만듭니다. 이 빠른 예제의 풀은 Azure Marketplace에서 Windows Server 2019 이미지를 실행하는 두 개의 노드로 구성되어 있습니다.

1. 배치 계정에서 **풀** > **추가** 를 차례로 선택합니다.

1. *mypool* 이라는 **풀 ID** 를 입력합니다.

1. **운영 체제** 에서 다음 설정을 선택합니다(다른 옵션을 탐색할 수 있음).
  
   |설정  |값  |
   |---------|---------|
   |**이미지 형식**|Marketplace|
   |**게시자**     |microsoftwindowsserver|
   |**제품**     |windowsserver|
   |**Sku**     |2019-datacenter-core-smalldisk|

1. 아래로 스크롤하여 **노드 크기** 및 **배율** 설정을 입력합니다. 제안된 노드 크기는 이 빠른 예제의 성능과 비용에 대한 적절한 균형을 제공합니다.
  
   |설정  |값  |
   |---------|---------|
   |**노드 가격 책정 계층**     |표준 A1|
   |**대상 전용 노드**     |2|

1. 나머지 설정은 기본값으로 유지하고 **확인** 을 선택하여 풀을 만듭니다.

Batch는 풀을 즉시 만들지만, 컴퓨팅 노드를 할당하고 시작하는 데 몇 분이 걸립니다. 이 시간 동안 풀의 **할당 상태** 는 **Resizing**(크기 조정 중)입니다. 풀 크기를 조정하는 동안 작업과 태스크를 계속 만들 수 있습니다.

몇 분 후에 풀의 상태가 **Steady** 로 변경되고 노드가 시작됩니다. 노드의 상태를 확인하려면 풀을 선택한 다음, **노드** 를 선택합니다. 노드의 상태가 **Idle**(유휴)이면 태스크를 실행할 준비가 되었습니다.

## <a name="create-a-job"></a>작업 만들기

이제 풀이 있으므로 여기에서 실행할 작업을 만들 수 있습니다. Batch 작업은 하나 이상의 태스크로 구성된 논리적 그룹입니다. 작업에는 우선 순위 및 태스크를 실행할 풀과 같은 태스크에 공통적으로 적용되는 설정이 포함됩니다. 처음에는 작업에 태스크가 없습니다.

1. 배치 계정 보기에서 **작업** > **추가** 를 선택합니다.

1. *myjob* 이라는 **작업 ID** 를 입력합니다. **풀** 에서 *mypool* 을 선택합니다. 나머지 설정은 기본값으로 유지하고 **확인** 을 선택합니다.

## <a name="create-tasks"></a>작업 만들기

이제 작업을 선택하여 **태스크** 페이지를 엽니다. 여기서 작업에서 실행할 샘플 태스크를 만듭니다. 일반적으로 컴퓨팅 노드에서 실행하기 위해 Batch에서 큐에 넣고 배포하는 여러 태스크를 만듭니다. 이 예제에서는 두 개의 동일한 태스크를 만듭니다. 각 태스크는 명령줄을 실행하여 컴퓨팅 노드에 Batch 환경 변수를 표시한 다음, 90초 동안 기다립니다.

Batch를 사용하면 명령줄에서 앱 또는 스크립트를 지정합니다. Batch는 컴퓨팅 노드에 앱과 스크립트를 배포하는 여러 가지 방법을 제공합니다.

첫 번째 태스크를 만들려면 다음을 수행합니다.

1. **추가** 를 선택합니다.

1. *mytask* 라는 **태스크 ID** 를 입력합니다.

1. **명령줄** 에 `cmd /c "set AZ_BATCH & timeout /t 90 > NUL"`을 입력합니다. 나머지 설정은 기본값으로 유지하고 **제출** 을 선택합니다.

태스크가 만들어지면 Batch는 풀에서 실행되도록 해당 태스크를 큐에 넣습니다. 노드에서 실행할 수 있게 되면 태스크가 실행됩니다.

두 번째 작업을 만들려면 위의 단계를 반복합니다. 다른 **태스크 ID** 를 입력하고 동일한 명령줄을 지정합니다. 첫 번째 태스크가 아직 실행 중이면 Batch는 풀의 다른 노드에서 두 번째 태스크를 시작합니다.

## <a name="view-task-output"></a>태스크 출력 보기

만든 예제 작업은 몇 분 안에 완료됩니다. 완료된 작업의 출력을 보려면 작업을 선택한 다음, **노드의 파일** 을 선택합니다. 작업의 표준 출력을 보려면 `stdout.txt` 파일을 선택합니다. 내용은 다음과 비슷합니다.

:::image type="content" source="media/quick-create-portal/task-output.png" alt-text="완료된 작업의 출력 스크린샷.":::

내용에는 노드에 설정된 Azure Batch 환경 변수가 표시됩니다. 사용자 고유의 Batch 작업 및 태스크를 만들 때, 태스크 명령줄과 이 명령줄에서 실행되는 앱 및 스크립트에서 이러한 환경 변수를 참조할 수 있습니다.

## <a name="clean-up-resources"></a>리소스 정리

Batch 자습서 및 샘플을 계속 사용하려면 이 빠른 시작에서 만든 배치 계정 및 연결된 스토리지 계정을 사용합니다. 배치 계정 자체에는 요금이 부과되지 않습니다.

작업이 예약되지 않은 경우에도 노드가 실행되는 동안은 풀에 대한 요금이 부과됩니다. 풀이 더 이상 필요하지 않으면 삭제합니다. 계정 보기에서 **풀** 과 해당 풀의 이름을 선택합니다. 그런 다음, **삭제** 를 선택합니다.  풀을 삭제하면 노드의 모든 태스크 출력이 삭제됩니다.

더 이상 필요하지 않으면 리소스 그룹, 배치 계정 및 관련된 모든 리소스를 삭제합니다. 이렇게 하려면 배치 계정에 대한 리소스 그룹을 선택하고 **리소스 그룹 삭제** 를 선택합니다.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 배치 계정, Batch 풀 및 Batch 작업을 만들었습니다. 작업에서 샘플 태스크를 실행했고, 노드 중 하나에서 만들어진 출력을 보았습니다. 이제 Batch 서비스의 핵심 개념을 이해 했으므로 더 큰 규모의 더 실제적인 작업 부하로 Batch를 시도할 준비가 되었습니다. Azure Batch에 대한 자세한 내용은 Azure Batch 자습서로 계속 진행하세요.

> [!div class="nextstepaction"]
> [Azure Batch 자습서](./tutorial-parallel-dotnet.md)
