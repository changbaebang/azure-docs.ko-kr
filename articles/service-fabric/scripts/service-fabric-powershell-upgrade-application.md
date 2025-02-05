---
title: Powershell에서 Service Fabric 애플리케이션 업그레이드
description: Azure PowerShell 스크립트 샘플 - Powershell을 사용하여 Azure Service Fabric 애플리케이션을 업그레이드하고 모니터링합니다.
services: service-fabric
documentationcenter: ''
author: athinanthny
manager: chackdan
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: service-fabric
ms.workload: multiple
ms.topic: sample
ms.date: 01/18/2018
ms.author: atsenthi
ms.custom: mvc
ms.openlocfilehash: 7b55dc6a400f936ac23b233e4c84a6b1aebf45cb
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99821996"
---
# <a name="upgrade-a-service-fabric-application"></a>Service Fabric 애플리케이션 업그레이드

이 샘플 스크립트는 실행 중인 Service Fabric 애플리케이션 인스턴스를 버전 1.3.0으로 업그레이드합니다. 이 스크립트는 새 애플리케이션 패키지를 클러스터 이미지 저장소에 복사하고, 애플리케이션 유형을 등록하고, 불필요한 애플리케이션 패키지를 제거합니다.  또한 모니터링되는 업그레이드를 시작하고 업그레이드가 완료되거나 롤백될 때까지 업그레이드 상태를 계속 확인합니다. 필요에 따라 매개 변수를 사용자 지정합니다. 

필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication) | Service Fabric 클러스터의 모든 애플리케이션 또는 특정 애플리케이션을 가져옵니다.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade) | Service Fabric 애플리케이션 업그레이드의 상태를 가져옵니다. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype) | Service Fabric 클러스터에 등록된 Service Fabric 애플리케이션 유형을 가져옵니다. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype) | Service Fabric 애플리케이션 유형을 등록 취소합니다.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage) | Service Fabric 애플리케이션 패키지를 이미지 저장소에 복사합니다.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype) | Service Fabric 애플리케이션 유형을 등록합니다. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade) | Service Fabric 애플리케이션을 지정된 애플리케이션 유형 버전으로 업그레이드합니다. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage) | 이미지 저장소에서 Service Fabric 애플리케이션 패키지를 제거합니다.|


## <a name="next-steps"></a>다음 단계

Service Fabric PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/service-fabric/overview)를 참조하세요.

Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.
