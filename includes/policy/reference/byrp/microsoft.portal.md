---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 03/24/2021
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 0df4035c75c124b33e299e1ccb2258ef41caebf6
ms.sourcegitcommit: bb330af42e70e8419996d3cba4acff49d398b399
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105037746"
---
|Name<br /><sub>(Azure Portal)</sub> |Description |효과 |버전<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[공유 대시보드에는 인라인 콘텐츠가 포함된 markdown 타일이 없어야 함](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F04c655fe-0ac7-48ae-9a32-3a2e208c7624) |markdown 타일에 인라인 콘텐츠를 포함하는 공유 대시보드를 만들 수 없도록 하고, 콘텐츠를 온라인으로 호스팅되는 markdown 파일로 저장되어야 합니다. markdown 타일에서 인라인 콘텐츠를 사용하는 경우 콘텐츠의 암호화를 관리할 수 없습니다. 사용자 고유의 스토리지를 구성하여 암호화와 이중 암호화하고 사용자 고유의 키도 가져올 수 있습니다. 이 정책을 사용하도록 설정하면 사용자가 2020-09-01-preview 이상 버전의 공유 대시보드 REST API를 사용하도록 제한됩니다. |감사, 거부, 사용 안 함 |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Portal/SharedDashboardInlineContent_Deny.json) |
