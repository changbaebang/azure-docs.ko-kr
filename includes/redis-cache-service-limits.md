---
author: wesmc7777
ms.service: redis-cache
ms.topic: include
ms.date: 11/09/2018
ms.author: wesmc
ms.openlocfilehash: 1ab6243be39bf30bc060ed5745fbf600924743a9
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "71839197"
---
| 리소스 | 제한 |
| --- | --- |
| 캐시 크기 |1.2TB |
| 데이터베이스 |64 |
| 연결된 최대 클라이언트 수 |40,000 |
| 고가용성을 위한 Azure Cache for Redis 복제본 |1 |
| 클러스터링을 사용하여 프리미엄 캐시 분할 |10 |

Azure Cache for Redis 제한 및 크기는 각 가격 책정 계층에 따라 다릅니다. 가격 책정 계층 및 해당 관련 크기를 확인하려면 [Azure Cache for Redis 가격 책정](https://azure.microsoft.com/pricing/details/cache/)을 참조하세요.

Azure Cache for Redis 구성 제한에 대한 자세한 내용은 [기본 Redis 서버 구성](../articles/azure-cache-for-redis/cache-configure.md#default-redis-server-configuration)을 참조하세요.

Azure Cache for Redis 인스턴스의 구성 및 관리는 Microsoft에서 수행하므로 Azure Cache for Redis에서 모든 Redis 명령이 지원되지는 않습니다. 자세한 내용은 [Azure Cache for Redis에서 지원되지 않는 Redis 명령](../articles/azure-cache-for-redis/cache-configure.md#redis-commands-not-supported-in-azure-cache-for-redis)을 참조하세요.

