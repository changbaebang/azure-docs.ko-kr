---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: ac46d531cda0a9ab352ba43b5bd1b873b9e256c1
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105033437"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure SignalR Service는 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F21a9766a-82a5-4747-abb5-650b6dbba6d0) |Azure SignalR Service 리소스의 보안을 향상하려면 공용 인터넷에 노출되지 않고 프라이빗 엔드포인트에서만 액세스할 수 있는지 확인합니다. [https://aka.ms/asrs/networkacls](https://aka.ms/asrs/networkacls)에 설명된 대로 공용 네트워크 액세스 속성을 사용하지 않도록 설정합니다. 이 옵션은 Azure IP 범위를 벗어나는 공용 주소 공간에서의 액세스를 사용하지 않도록 설정하고, IP 또는 가상 네트워크 기반 방화벽 규칙과 일치하는 모든 로그인을 거부합니다. 이로 인해 데이터 누출 위험이 줄어듭니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/SignalR/SignalR_PublicNetworkAccessDisabled_AuditDeny.json) |
|[Azure SignalR Service는 Private Link 지원 SKU를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F464a1620-21b5-448d-8ce6-d4ac6d1bc49a) |Azure Private Link를 통해 원본 또는 대상의 공용 IP 주소가 없어도 가상 네트워크를 Azure 서비스에 연결할 수 있어 공용 데이터 유출 위험으로부터 리소스를 보호할 수 있습니다. 정책은 Azure SignalR Service에 대한 Private Link 지원 SKU로 제한됩니다. [https://aka.ms/asrs/privatelink](https://aka.ms/asrs/privatelink)에서 프라이빗 링크에 대해 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/SignalR/SignalR_AllowedSKU_AuditDeny.json) |
|[Azure SignalR Service는 프라이빗 링크를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F53503636-bcc9-4748-9663-5348217f160f) |Azure Private Link를 통해 원본 또는 대상의 공용 IP 주소가 없어도 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 링크 플랫폼은 Azure 백본 네트워크를 통해 소비자와 서비스 간의 연결을 처리합니다. 프라이빗 엔드포인트를 전체 서비스가 아닌 Azure SignalR Service 리소스에 매핑하면 데이터 유출 위험을 줄일 수 있습니다. [https://aka.ms/asrs/privatelink](https://aka.ms/asrs/privatelink)에서 프라이빗 링크에 대해 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/SignalR/SignalR_PrivateEndpointEnabled_Audit.json) |
|[배포 - 프라이빗 엔드포인트의 프라이빗 DNS 영역을 구성하여 Azure SignalR Service에 연결](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb0e86710-7fb7-4a6c-a064-32e9b829509e) |프라이빗 DNS 영역을 사용하여 프라이빗 엔드포인트에 대한 DNS 확인을 재정의합니다. 프라이빗 DNS 영역은 가상 네트워크에 연결하여 Azure SignalR Service 리소스로 확인합니다. [https://aka.ms/asrs/privatelink](https://aka.ms/asrs/privatelink)에서 자세히 알아보세요. |DeployIfNotExists, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/SignalR/SignalR_PrivateEndpointDNSZone_DeployIfNotExists.json) |
|[Azure SignalR Service 리소스를 수정하여 공용 네트워크 액세스를 사용하지 않도록 설정](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F62a3ae95-8169-403e-a2d2-b82141448092) |Azure SignalR Service 리소스의 보안을 향상하려면 공용 인터넷에 노출되지 않고 프라이빗 엔드포인트에서만 액세스할 수 있는지 확인합니다. [https://aka.ms/asrs/networkacls](https://aka.ms/asrs/networkacls)에 설명된 대로 공용 네트워크 액세스 속성을 사용하지 않도록 설정합니다. 이 옵션은 Azure IP 범위를 벗어나는 공용 주소 공간에서의 액세스를 사용하지 않도록 설정하고, IP 또는 가상 네트워크 기반 방화벽 규칙과 일치하는 모든 로그인을 거부합니다. 이로 인해 데이터 누출 위험이 줄어듭니다. |수정, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/SignalR/SignalR_PublicNetworkAccessDisabled_Modify.json) |
