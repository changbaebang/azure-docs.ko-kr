---
title: Powershell의 클러스터에서 애플리케이션 제거
description: Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터에서 애플리케이션 제거
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
ms.openlocfilehash: 686afa791df88382e3e5e1b2d233317c36bf1dd6
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99821874"
---
# <a name="remove-an-application-from-a-service-fabric-cluster-using-powershell"></a>Powershell을 사용하여 Service Fabric 클러스터에서 애플리케이션 제거

이 샘플 스크립트는 실행 중인 Service Fabric 애플리케이션 인스턴스를 삭제하고, 클러스터에서 애플리케이션 유형 및 버전의 등록을 취소합니다.  애플리케이션 인스턴스를 삭제하면 해당 애플리케이션과 연결된 실행 중인 모든 서비스 인스턴스도 삭제됩니다. 필요에 따라 매개 변수를 사용자 지정합니다. 

필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication) | 클러스터에서 실행 중인 Service Fabric 애플리케이션 인스턴스를 제거합니다.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype) | 클러스터에서 Service Fabric 애플리케이션 유형 및 버전을 등록 취소합니다. |

## <a name="next-steps"></a>다음 단계

Service Fabric PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/service-fabric/overview)를 참조하세요.

Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.
