---
author: tfitzmac
ms.service: azure-resource-manager
ms.topic: include
ms.date: 09/01/2020
ms.author: tomfitz
ms.openlocfilehash: 543aa50d72de5a06a9a1c7ac88ac5ecae993bc9d
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98697890"
---
| 리소스 | 제한 |
| --- | --- |
| [리소스 그룹](../articles/azure-resource-manager/management/overview.md#resource-groups)당 리소스 | 리소스는 리소스 그룹으로 제한되지 않습니다. 대신 리소스 그룹의 리소스 형식에 의해 제한됩니다. 다음 행을 참조하세요. |
| 리소스 그룹당, 리소스 유형당 리소스 |800 - 일부 리소스 유형은 800 제한을 초과할 수 있습니다. [리소스 그룹당 800 인스턴스로 제한되지 않는 리소스](../articles/azure-resource-manager/management/resources-without-resource-group-limit.md)를 참조하세요. |
| 배포 기록의 리소스 그룹당 배포 |800<sup>1</sup> |
| 배포당 리소스 |800 |
| 고유 [범위](../articles/azure-resource-manager/management/overview.md#understand-scope)당 관리 잠금  |20 |
| 리소스당 또는 리소스 그룹당 태그 수 |50 |
| 태그 키 길이 |512 |
| 태그 값 길이 |256 |

<sup>1</sup>한도에 가까워지면 배포가 기록에서 자동으로 삭제됩니다. 배포 기록에서 항목을 삭제해도 배포된 리소스에는 영향을 주지 않습니다. 자세한 내용은 [배포 기록에서 자동 삭제](../articles/azure-resource-manager/templates/deployment-history-deletions.md)를 참조하세요.

#### <a name="template-limits"></a>템플릿 제한

| 값 | 제한 |
| --- | --- |
| 매개 변수 |256 |
| variables |256 |
| 리소스(인쇄 매수 포함) |800 |
| 출력 |64 |
| 템플릿 식 |24,576개 문자 |
| 내보낸 템플릿의 리소스 |200 |
| 템플릿 크기 |4MB |
| 매개 변수 파일 크기 |64KB |

중첩된 템플릿을 사용하여 일부 템플릿 제한을 초과할 수 있습니다. 자세한 내용은 [Azure 리소스를 배포할 때 연결된 템플릿 사용](../articles/azure-resource-manager/templates/linked-templates.md)을 참조하세요. 매개 변수, 변수 또는 출력의 수를 줄이려면 개체에 여러 값을 결합할 수 있습니다. 자세한 내용은 [매개 변수로 개체 사용](/azure/architecture/guide/azure-resource-manager/advanced-templates/objects-as-parameters)을 참조하세요.