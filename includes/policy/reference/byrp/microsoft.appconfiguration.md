---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 1962cd2e3b7f771915e39ade20a80b0b2eeb4175
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105038205"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[App Configuration은 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3d9f5e4c-9947-4579-9539-2a7695fbc187) |공용 네트워크 액세스를 사용하지 않도록 설정하면 리소스가 공용 인터넷에 노출되지 않도록 하여 보안이 향상됩니다. 대신 프라이빗 엔드포인트를 만들어 리소스 노출을 제한할 수 있습니다. [https://aka.ms/appconfig/private-endpoint](https://aka.ms/appconfig/private-endpoint)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_PublicNetworkAccess_Audit.json) |
|[App Configuration에는 고객 관리형 키를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F967a4b4b-2da9-43c1-b7d0-f98d0d74d0b1) |고객 관리형 키는 암호화 키를 관리할 수 있도록 허용하여 향상된 데이터 보호를 제공합니다. 이는 주로 규정 준수 요구 사항을 충족하는 데 필요합니다. |감사, 거부, 사용 안 함 |[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/CustomerManagedKey_Audit.json) |
|[App Configuration은 프라이빗 링크를 지원하는 SKU를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F89c8a434-18f0-402c-8147-630a8dea54e0) |지원되는 SKU를 사용하는 경우 Azure Private Link를 사용하면 원본 또는 대상에서 공용 IP 주소 없이 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 링크 플랫폼은 Azure 백본 네트워크를 통해 소비자와 서비스 간의 연결을 처리합니다. 전체 서비스가 아닌 앱 구성 인스턴스에 프라이빗 엔드포인트를 매핑하면 데이터 유출 위험으로부터 보호받을 수 있습니다. [https://aka.ms/appconfig/private-endpoint](https://aka.ms/appconfig/private-endpoint)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_AllowedSku_Audit.json) |
|[App Configuration은 프라이빗 링크를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fca610c1d-041c-4332-9d88-7ed3094967c7) |Azure Private Link를 통해 원본 또는 대상의 공용 IP 주소가 없어도 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 링크 플랫폼은 Azure 백본 네트워크를 통해 소비자와 서비스 간의 연결을 처리합니다. 전체 서비스가 아닌 앱 구성 인스턴스에 프라이빗 엔드포인트를 매핑하면 데이터 유출 위험으로부터 보호받을 수 있습니다. [https://aka.ms/appconfig/private-endpoint](https://aka.ms/appconfig/private-endpoint)에서 자세히 알아보세요. |AuditIfNotExists, 사용 안 함 |[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_Audit.json) |
|[공용 네트워크 액세스를 사용하지 않도록 App Configuration 구성](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F73290fa2-dfa7-4bbb-945d-a5e23b75df2c) |공용 인터넷을 통해 액세스할 수 없도록 App Configuration에 대한 공용 네트워크 액세스를 사용하지 않도록 설정합니다. 이 구성은 데이터 유출 위험으로부터 보호할 수 있습니다. 대신 프라이빗 엔드포인트를 만들어 리소스 노출을 제한할 수 있습니다. [https://aka.ms/appconfig/private-endpoint](https://aka.ms/appconfig/private-endpoint)에서 자세히 알아보세요. |수정, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_PublicNetworkAccess_Modify.json) |
|[App Configuration의 프라이빗 엔드포인트 구성](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F614ffa75-862c-456e-ad8b-eaa1b0844b07) |프라이빗 엔드포인트를 사용하면 원본 또는 대상의 공용 IP 주소가 없어도 Azure 서비스에 가상 네트워크를 연결할 수 있습니다. 프라이빗 엔드포인트를 앱 구성 인스턴스에 매핑하면 데이터 누출 위험이 줄어듭니다. [https://aka.ms/appconfig/private-endpoint](https://aka.ms/appconfig/private-endpoint)에서 자세히 알아보세요. |DeployIfNotExists, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Configuration/PrivateLink_Deploy.json) |
