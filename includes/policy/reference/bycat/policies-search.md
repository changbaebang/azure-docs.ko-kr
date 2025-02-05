---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 111518d13cccb135541b9fedf167edd53d75a00e
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105033409"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure Cognitive Search 서비스는 프라이빗 링크를 지원하는 SKU를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa049bf77-880b-470f-ba6d-9f21c530cf83) |Azure Cognitive Search의 지원되는 SKU를 통해 Azure Private Link를 사용하면 원본 또는 대상에서 공용 IP 주소 없이 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 링크 플랫폼은 Azure 백본 네트워크를 통해 소비자와 서비스 간의 연결을 처리합니다. 프라이빗 엔드포인트를 Search Service에 매핑하면 데이터 누출 위험이 줄어듭니다. [https://aka.ms/azure-cognitive-search/inbound-private-endpoints](https://aka.ms/azure-cognitive-search/inbound-private-endpoints)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/Search_RequirePrivateLinkSupportedResource_Deny.json) |
|[Azure Cognitive Search 서비스는 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fee980b6d-0eca-4501-8d54-f6290fd512c3) |공용 네트워크 액세스를 사용하지 않도록 설정하면 Azure Cognitive Search 서비스가 공용 인터넷에 노출되지 않도록 하여 보안이 향상됩니다. 프라이빗 엔드포인트를 만들면 Search Service의 노출을 제한할 수 있습니다. [https://aka.ms/azure-cognitive-search/inbound-private-endpoints](https://aka.ms/azure-cognitive-search/inbound-private-endpoints)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/Search_RequirePublicNetworkAccessDisabled_Deny.json) |
|[공용 네트워크 액세스를 비활성화하도록 Azure Cognitive Search 서비스 구성](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9cee519f-d9c1-4fd9-9f79-24ec3449ed30) |공용 인터넷을 통해 액세스할 수 없도록 Azure Cognitive Search 서비스에 대한 공용 네트워크 액세스를 사용하지 않도록 설정합니다. 이를 통해 데이터 유출 위험을 줄일 수 있습니다. [https://aka.ms/azure-cognitive-search/inbound-private-endpoints](https://aka.ms/azure-cognitive-search/inbound-private-endpoints)에서 자세히 알아보세요. |수정, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/Search_PublicNetworkAccessDisabled_Modify.json) |
|[프라이빗 DNS 영역을 사용하도록 Azure Cognitive Search 서비스 구성](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffbc14a67-53e4-4932-abcc-2049c6706009) |프라이빗 DNS 영역을 사용하여 프라이빗 엔드포인트에 대한 DNS 확인을 재정의합니다. 프라이빗 DNS 영역은 가상 네트워크에 연결되어 Azure Cognitive Search 서비스를 확인합니다. [https://aka.ms/azure-cognitive-search/inbound-private-endpoints](https://aka.ms/azure-cognitive-search/inbound-private-endpoints)에서 자세히 알아보세요. |DeployIfNotExists, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/Search_PrivateDNSZone_DeployIfNotExists.json) |
|[Search Service의 리소스 로그를 사용하도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb4330a05-a843-4bc8-bf9a-cacce50c67f4) |리소스 로그 사용을 감사합니다. 이렇게 하면 보안 인시던트가 발생하거나 네트워크가 손상된 경우 조사 목적으로 사용할 활동 내역을 다시 만들 수 있습니다. |AuditIfNotExists, 사용 안 함 |[4.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Search/Search_AuditDiagnosticLog_Audit.json) |
