---
author: alkohli
ms.service: databox
ms.topic: include
ms.date: 03/12/2021
ms.author: alkohli
ms.openlocfilehash: cf67ea58c4c13756fdc6e437883f12124ca47eb9
ms.sourcegitcommit: ed7376d919a66edcba3566efdee4bc3351c57eda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105103998"
---
1. [Azure Portal](https://portal.azure.com/)에서 Azure Stack Edge 리소스를 선택한 다음, **개요** 로 이동합니다. 디바이스는 온라인 상태여야 합니다. **클라우드 저장소 게이트웨이 > 스토리지 계정** 으로 차례로 이동합니다.

2. 디바이스 명령 모음에서 **+ 스토리지 계정 추가** 를 선택합니다. 

   ![스토리지 계정 추가](media/azure-stack-edge-gateway-add-storage-account/add-storage-account-1.png)

3. **Edge 스토리지 계정 추가** 창에서 다음 설정을 지정합니다.

    1. 디바이스의 Edge 스토리지 계정에 대한 고유한 이름을 제공합니다. 스토리지 계정 이름에는 소문자와 숫자만 포함할 수 있습니다. 특수 문자는 허용되지 않습니다. 스토리지 계정 이름은 디바이스 내에서 고유해야 합니다(디바이스 간에는 아님).

    2. 스토리지 계정이 보유하고 있는 데이터에 대한 정보의 선택적 설명을 제공합니다.  
    
    3. 기본적으로 Edge 스토리지 계정은 클라우드의 Azure Storage 계정에 매핑되고 스토리지 계정의 데이터는 자동으로 클라우드로 푸시됩니다. Edge 스토리지 계정이 매핑되는 Azure 스토리지 계정을 지정합니다.

    4. 새 컨테이너를 만들거나 Azure 스토리지 계정의 기존 컨테이너에서 선택합니다. Edge 스토리지 계정에 기록된 디바이스의 데이터가 있으면 매핑된 Azure Storage 계정에서 선택한 스토리지 컨테이너에 자동으로 업로드됩니다.

    5. 모든 스토리지 계정 옵션을 지정한 후 **추가** 를 선택하여 Edge 스토리지 계정을 만듭니다. Edge 스토리지 계정이 성공적으로 만들어지면 알림이 표시됩니다. 그러면, 새 Edge 스토리지 계정이 Azure Portal의 스토리지 계정 목록에 표시됩니다.

    <!--[Add a storage account](media/azure-stack-edge-gateway-add-storage-account/add-storage-account-2.png)-->
    
4. 새 스토리지 계정을 선택하고 **액세스 키** 로 이동하면 Blob service 엔드포인트 및 해당하는 스토리지 계정 이름을 찾을 수 있습니다. 이 정보를 복사합니다. 이러한 값은 액세스 키와 함께 Edge 스토리지 계정에 연결하는 데 도움이 됩니다.

    ![스토리지 계정 2 추가](media/azure-stack-edge-gateway-add-storage-account/add-storage-account-4.png)

    [Azure Resource Manager를 사용하여 디바이스 로컬 API에 연결](../articles/databox-online/azure-stack-edge-gpu-connect-resource-manager.md)하여 액세스 키를 가져옵니다.