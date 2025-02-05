---
title: Powershell의 부하 분산 장치에서 애플리케이션 포트 열기
description: Azure PowerShell 스크립트 샘플 - Service Fabric 애플리케이션에 대한 Azure Load Balancer에서 애플리케이션 포트 열기
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
ms.date: 05/18/2018
ms.author: atsenthi
ms.custom: mvc
ms.openlocfilehash: 4be9944a53aaf0c697d55ff567dee7f2fbb3ed85
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87038089"
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a>Azure Load Balancer에서 애플리케이션 포트 열기

Azure에서 실행되는 Service Fabric 애플리케이션은 Azure Load Balancer 뒤에 있습니다. 이 샘플 스크립트는 Service Fabric 애플리케이션이 외부 클라이언트와 통신할 수 있도록 Azure Load Balancer에서 포트를 엽니다. 필요에 따라 매개 변수를 사용자 지정합니다. 또한 클러스터가 네트워크 보안 그룹에 위치하는 경우 [인바운드 네트워크 보안 그룹 규칙을 추가](service-fabric-powershell-add-nsg-rule.md)하여 인바운드 트래픽을 허용합니다.

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

필요한 경우 [Service Fabric SDK](../service-fabric-get-started.md)를 사용하여 Service Fabric PowerShell 모듈을 설치합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용합니다. 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [Get-AzResource](/powershell/module/az.resources/get-azresource) | Azure 리소스를 가져옵니다.  |
| [Get-AzLoadBalancer](/powershell/module/az.network/get-azloadbalancer) | Azure Load Balancer를 가져옵니다. |
| [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/add-azloadbalancerprobeconfig) | Load Balancer에 프로브 구성을 추가합니다.|
| [Get-AzLoadBalancerProbeConfig](/powershell/module/az.network/get-azloadbalancerprobeconfig) | Load Balancer에 대한 프로브 구성을 가져옵니다. |
| [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/add-azloadbalancerruleconfig) | Load Balancer에 규칙 구성을 추가합니다. |
| [Set-AzLoadBalancer](/powershell/module/az.network/set-azloadbalancer) | Load Balancer에 대한 목표 상태를 설정합니다. |

## <a name="next-steps"></a>다음 단계

Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/)를 참조하세요.

Azure Service Fabric에 대한 추가 PowerShell 샘플은 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)에서 확인할 수 있습니다.
