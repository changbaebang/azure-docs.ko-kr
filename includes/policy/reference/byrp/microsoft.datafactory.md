---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 3319429dca1f4f3060d38d3417c7efbc3dc74d2a
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105038052"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure Data Factory는 고객 관리형 키로 암호화해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4ec52d6d-beb7-40c4-9a9e-fe753254690e) |고객 관리형 키를 사용하여 Azure Data Factory의 미사용 데이터 암호화를 관리합니다. 기본적으로 고객 데이터는 서비스 관리형 키로 암호화되지만, 고객 관리형 키는 일반적으로 규정 준수 기준을 충족하는 데 필요합니다. 고객 관리형 키를 사용하면 사용자가 만들고 소유한 Azure Key Vault 키를 사용하여 데이터를 암호화할 수 있습니다. 순환 및 관리를 포함하여 키의 수명 주기를 고객이 모두 제어하고 책임져야 합니다. [https://aka.ms/adf-cmk](https://aka.ms/adf-cmk)에서 자세히 알아보세요. |감사, 거부, 사용 안 함 |[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/DataFactory_CustomerManagedKey_Audit.json) |
|[Azure Data Factory 통합 런타임에는 코어 수 제한이 있어야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F85bb39b5-2f66-49f8-9306-77da3ac5130f) |리소스 및 비용을 관리하려면 통합 런타임에 대한 코어 수를 제한합니다. |감사, 거부, 사용 안 함 |[1.0.0 - 미리 보기](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/IR_Core_Count_Exceeds_Audit.json) |
|[Azure Data Factory 연결된 서비스 리소스 종류가 허용 목록에 있어야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6809a3d0-d354-42fb-b955-783d207c62a8) |Azure Data Factory 연결된 서비스 유형의 허용 목록을 정의합니다. 허용되는 리소스 종류를 제한하면 데이터 이동의 경계를 제어할 수 있습니다. 예를 들어 분석을 위해 Data Lake Storage Gen1 및 Gen2를 사용하는 Blob Storage만 허용하거나, 실시간 쿼리를 위해 SQL 및 Kusto 액세스만 허용하도록 범위를 제한합니다. |감사, 거부, 사용 안 함 |[1.0.0 - 미리 보기](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/LinkedService_ResourceType_Audit.json) |
|[Azure Data Factory 연결된 서비스는 비밀 저장에 Key Vault를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F127ef6d7-242f-43b3-9eef-947faf1725d0) |비밀(예: 연결 문자열)을 안전하게 관리하려면 사용자가 연결된 서비스에서 인라인으로 지정하는 대신 Azure Key Vault를 사용하여 비밀을 제공해야 합니다. |감사, 거부, 사용 안 함 |[1.0.0 - 미리 보기](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/LinkedService_InlineSecrets_Audit.json) |
|[Azure Data Factory 연결된 서비스는 지원되는 경우 시스템 할당 관리 ID 인증을 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff78ccdb4-7bf4-4106-8647-270491d2978a) |연결된 서비스를 통해 데이터 저장소와 통신할 때 시스템 할당 관리 ID를 사용하면 암호나 연결 문자열과 같은 덜 안전한 자격 증명을 사용하지 않아도 됩니다. |감사, 거부, 사용 안 함 |[1.0.0 - 미리 보기](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/LinkedService_All_Auth_Audit_except_MSI.json) |
|[Azure Data Factory는 소스 제어에 Git 리포지토리를 사용해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F77d40665-3120-4348-b539-3192ec808307) |변경 내용 추적, 협업, 연속 통합 및 배포와 같은 기능을 얻기 위해 Data Factory에 대한 소스 제어를 사용하도록 설정합니다. |감사, 거부, 사용 안 함 |[1.0.0 - 미리 보기](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/Factory_None_GIT_Audit.json) |
|[Azure Data Factory에서 공용 네트워크 액세스를 사용하지 않도록 설정해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1cf164be-6819-4a50-b8fa-4bcaa4f98fb6) |공용 네트워크 액세스 속성을 사용하지 않도록 설정하면 프라이빗 엔드포인트에서만 Azure Data Factory에 액세스할 수 있어 보안이 향상됩니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/DataFactory_PublicNetworkAccess_Audit.json) |
|[Azure Data Factory의 SQL Server Integration Services 통합 런타임을 가상 네트워크에 조인해야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0088bc63-6dee-4a9c-9d29-91cfdc848952) |Azure Virtual Network를 배포하면 서브넷, 액세스 제어 정책, 추가로 액세스를 제어하는 기타 기능이 제공될 뿐만 아니라 Azure Data Factory에서 SQL Server Integration Services 통합 런타임에 대한 보안과 격리가 향상됩니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Data%20Factory/SSISIR_JoinVirtualNetwork_Audit.json) |
