---
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 11/09/2018
ms.author: cynthn
ms.openlocfilehash: 994a7726adec07f2f6533d460d05469a0f3c7bf3
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87102851"
---
| 리소스 | 제한 |
| --- | --- |
| 클라우드 서비스당 가상 머신 <sup>1</sup> |50 |
| 클라우드 서비스당 입력 엔드포인트 <sup>2</sup> |150 |

<sup>1</sup> Azure Resource Manager 대신 클래식 배포 모델을 사용하여 만든 가상 머신은 클라우드 서비스에 자동으로 저장됩니다. 부하 분산 및 가용성을 위해 해당 클라우드 서비스에 더 많은 가상 머신을 추가할 수 있습니다. 

<sup>2</sup> 입력 엔드포인트를 사용하여 가상 머신의 클라우드 서비스 외부에서 가상 머신에 통신할 수 있습니다. 같은 클라우드 서비스나 가상 네트워크에 있는 가상 머신은 서로 간에 자동으로 통신할 수 있습니다.  
