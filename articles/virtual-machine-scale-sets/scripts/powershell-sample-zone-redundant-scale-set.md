---
title: Azure PowerShell 샘플 - 영역 중복 확장 집합
description: 이 스크립트는 여러 가용성 영역에 걸쳐 Windows Server 2016을 실행하는 가상 머신 확장 집합을 만듭니다.
author: mimckitt
ms.author: mimckitt
ms.topic: sample
ms.service: virtual-machine-scale-sets
ms.subservice: availability
ms.date: 04/05/2018
ms.reviewer: jushiman
ms.custom: mimckitt, devx-track-azurepowershell
ms.openlocfilehash: 89c3d32c1f69fa905272a07751ee64d0491d2d32
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "89067725"
---
# <a name="create-a-zone-redundant-virtual-machine-scale-set-with-powershell"></a>PowerShell을 사용하여 영역 중복 가상 머신 확장 집합 만들기
이 스크립트는 여러 가용성 영역에 걸쳐 Windows Server 2016을 실행하는 가상 머신 확장 집합을 만듭니다. 스크립트를 실행하면 RDP를 통해 가상 머신에 액세스할 수 있습니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az.md](../../../includes/updated-for-az.md)]

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/virtual-machine-scale-sets/create-zone-redundant-scale-set/create-zone-redundant-scale-set.ps1 "Create zone-redundant scale set")]

## <a name="clean-up-deployment"></a>배포 정리
다음 명령을 실행하여 리소스 그룹, 확장 집합 및 모든 관련된 리소스를 제거할 수 있습니다.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명
이 스크립트는 다음 명령을 사용하여 배포합니다. 테이블에 있는 각 항목은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [New-AzVmss](/powershell/module/az.compute/new-azvmss) | 가상 네트워크, 부하 분산 장치 및 NAT 규칙을 포함하여 가상 머신 확장 집합 및 모든 지원 리소스를 만듭니다. |
| [Get-AzVmss](/powershell/module/az.compute/get-azvmss) | 가상 머신 확장 집합에 대한 정보를 가져옵니다. |
| [Add-AzVmssExtension](/powershell/module/az.compute/add-azvmssextension) | 사용자 지정 스크립트용 VM 확장을 추가하여 기본 웹 애플리케이션을 설치합니다. |
| [업데이트 AzVmss](/powershell/module/az.compute/update-azvmss) | VM 확장을 적용하기 위해 가상 머신 확장 집합 모델을 업데이트합니다. |
| [Get-AzPublicIpAddress](/powershell/module/az.network/get-azpublicipaddress) | 부하 분산 장치에서 사용하는 할당된 공용 IP 주소에 대한 정보를 가져옵니다. |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | 리소스 그룹 및 포함된 모든 리소스를 제거합니다. |


## <a name="next-steps"></a>다음 단계
Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/)를 참조하세요.
