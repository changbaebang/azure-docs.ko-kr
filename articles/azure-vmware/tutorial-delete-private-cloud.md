---
title: 자습서 - Azure VMware Solution 프라이빗 클라우드 삭제
description: 더 이상 필요하지 않은 Azure VMware Solution 프라이빗 클라우드를 삭제하는 방법을 알아봅니다.
ms.topic: tutorial
ms.date: 03/13/2021
ms.openlocfilehash: 453e7a3316c342cd724a951eafea0ae9fa045506
ms.sourcegitcommit: afb9e9d0b0c7e37166b9d1de6b71cd0e2fb9abf5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2021
ms.locfileid: "103462102"
---
# <a name="tutorial-delete-an-azure-vmware-solution-private-cloud"></a>자습서: Azure VMware Solution 프라이빗 클라우드 삭제

더 이상 필요하지 않은 Azure VMware Solution 프라이빗 클라우드가 있으면 이를 삭제할 수 있습니다. 프라이빗 클라우드에는 격리된 네트워크 도메인, 전용 서버 호스트에 프로비저닝된 하나 이상의 vSphere 클러스터 및 여러 가지 VM(가상 머신)이 포함되어 있습니다. 프라이빗 클라우드를 삭제하면 모든 VM, 해당 데이터 및 클러스터가 삭제됩니다. 전용 Azure VMware Solution 호스트는 안전하게 초기화되어 무료 풀로 반환됩니다. 프로비저닝된 네트워크 주소 공간도 삭제됩니다.  

> [!CAUTION]
> 프라이빗 클라우드 삭제는 되돌릴 수 없는 작업입니다. 프라이빗 클라우드를 삭제하면 실행 중인 모든 워크로드 및 구성 요소가 종료되고 공용 IP 주소를 포함한 모든 프라이빗 클라우드 데이터 및 구성 설정이 삭제되므로 데이터를 복구할 수 없습니다.

## <a name="prerequisites"></a>사전 요구 사항

나중에 VM과 해당 데이터가 필요한 경우 프라이빗 클라우드를 삭제하기 전에 데이터를 백업해야 합니다.  VM과 해당 데이터를 복구할 수 있는 방법은 없습니다.


## <a name="delete-the-private-cloud"></a>프라이빗 클라우드 삭제

1. [Azure Portal](https://portal.azure.com)에서 Azure VMware Solution 콘솔에 액세스합니다.

2. 삭제할 프라이빗 클라우드를 선택합니다.
 
3. 프라이빗 클라우드의 이름을 입력하고 **예** 를 선택합니다. 

>[!NOTE]
>삭제 프로세스를 완료하는 데 몇 시간이 걸립니다.  
