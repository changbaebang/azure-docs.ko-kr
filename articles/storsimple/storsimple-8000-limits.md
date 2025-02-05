---
title: StorSimple 8000 시리즈 시스템 제한 | Microsoft Docs
description: StorSimple 8000 시리즈 구성 요소 및 연결에 대한 시스템 제한 및 권장 크기에 대해 설명합니다.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/28/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70f2d9542082ddf7ecf1d1e7361b0ecdb14c5ef8
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "68963383"
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>StorSimple 8000 시리즈 시스템 제한이란?

[!INCLUDE [storsimple-8000-eol-banner](../../includes/storsimple-8000-eol-banner.md)]

## <a name="overview"></a>개요

StorSimple는 데이터 센터에 대해 확장 가능하고 유연한 스토리지를 제공합니다. 그러나 StorSimple 솔루션의 계획, 배포 및 작동 시 염두에 두어야 하는 일부 제한 사항이 있습니다. 다음 표에서 이러한 제한에 대해 설명하고 일부 권장 사항을 제공하므로 StorSimple 솔루션을 최대한 활용할 수 있습니다.

| 제한 식별자 | 제한 | 주석 |
| --- | --- | --- |
| 스토리지 계정 자격 증명의 최대 수 |64 | |
| 볼륨 컨테이너의 최대 수 |64 | |
| 최대 볼륨 수 |255 | |
| 로컬로 고정된 볼륨의 최대 수 |32 | |
| 대역폭 템플릿당 일정의 최대 수 |168 |매시간, 매일에 대한 일정(24*7). |
| 물리적 디바이스의 계층화된 볼륨 최대 크기 |8100 및 8600의 경우 64TB |8100과 8600은 물리적 디바이스입니다. |
| Azure 내 가상 디바이스의 계층화된 볼륨 최대 크기 |8010의 경우 30TB <br></br>  8020의 경우 64TB |8010과 8020은 각각 Standard Storage와 Premium Storage를 사용하는 Azure의 가상 디바이스입니다. |
| 물리적 디바이스의 로컬로 고정된 볼륨 최대 크기 |8100의 경우 8.5TB <br></br>  8600의 경우 22.5TB |8100과 8600은 물리적 디바이스입니다. |
| iSCSI 연결의 최대 수 |512 | |
| 초기자에서 iSCSI 연결의 최대 수 |512 | |
| 디바이스당 액세스 제어 레코드의 최대 수 |64 | |
| 백업 정책당 볼륨의 최대 수 |20 | |
| 일정당 유지된 백업의 최대 수(백업 정책에서) |64 | |
| 백업 정책당 일정의 최대 수 |10 | |
| 볼륨당 유지할 수 있는 모든 형식의 최대 스냅샷 수 |256 |이 숫자에는 로컬 스냅샷과 클라우드 스냅샷이 포함됩니다. |
| 어느 디바이스에나 표시할 수 있는 최대 스냅샷 수 |10000 | |
| 백업, 복원 또는 복제를 위해 병렬로 처리할 수 있는 최대 볼륨 수 |16 |<ul><li>볼륨이 16개를 초과하는 경우, 처리 중인 슬롯을 사용할 수 있게 되면 순차적으로 처리됩니다.</li><li>복제 또는 복원된 계층화된 볼륨의 새 백업은 작업이 완료될 때까지 발생할 수 없습니다. 그러나 로컬 볼륨의 경우 볼륨이 온라인 상태가 된 후에 백업이 허용됩니다.</li></ul> |
| 계층화된 볼륨의 복원 및 복제 복구 시간 |2분 미만 |<ul><li>볼륨은 볼륨의 크기에 상관없이 복원 또는 복제 작업 중 2분 내에 사용할 수 있습니다.</li><li>대부분의 데이터 및 메타데이터가 여전히 클라우드에 상주하므로 볼륨의 성능은 초기에는 느려질 수도 있습니다. 성능은 데이터가 클라우드에서 StorSimple 디바이스로 흐르면서 향상될 수도 있습니다.</li><li>메타데이터의 총 다운로드 시간은 할당된 볼륨 크기에 따라 다릅니다. 메타데이터는 할당된 볼륨 데이터의 TB당 5분의 속도로 자동으로 백그라운드에 가져와집니다. 이 속도는 클라우드에 대한 인터넷 대역폭에 의해 영향을 받을 수 있습니다.</li><li>모든 메타데이터가 디바이스에 있는 경우 복원 또는 복제 작업이 완료됩니다.</li><li>복원 또는 복제 작업이 완료될 때까지 Backup 작업을 수행할 수 없습니다. |
| 로컬로 고정된 볼륨의 복원 복구 시간 |2분 미만 |<ul><li>볼륨은 볼륨의 크기에 상관없이 복원 작업 중 2분 내에 사용할 수 있습니다.</li><li>대부분의 데이터 및 메타데이터가 여전히 클라우드에 상주하므로 볼륨의 성능은 초기에는 느려질 수도 있습니다. 성능은 데이터가 클라우드에서 StorSimple 디바이스로 흐르면서 향상될 수도 있습니다.</li><li>메타데이터의 총 다운로드 시간은 할당된 볼륨 크기에 따라 다릅니다. 메타데이터는 할당된 볼륨 데이터의 TB당 5분의 속도로 자동으로 백그라운드에 가져와집니다. 이 속도는 클라우드에 대한 인터넷 대역폭에 의해 영향을 받을 수 있습니다.</li><li>계층화된 볼륨과 달리, 로컬로 고정된 볼륨의 경우 볼륨 데이터도 디바이스에 로컬로 다운로드됩니다. 모든 볼륨 데이터를 디바이스로 가져왔으면 복원 작업이 완료된 것입니다.</li><li>복원 작업은 시간이 오래 걸릴 수 있습니다. 복원을 완료하는 데 드는 총 시간은 프로비전된 로컬 볼륨의 크기, 인터넷 대역폭 및 디바이스에 있는 기존 데이터에 따라 달라집니다. 로걸로 고정된 볼륨에서는 복원 작업이 진행 중인 동안 백업 작업이 허용됩니다. |
| 클라우드 스냅샷에 대한 처리 속도 |15분/TB |<ul><li>클라우드 스냅샷이 백업에서 할당된 볼륨 데이터의 TB당 업로드할 수 있도록 준비하는 최소 시간입니다. </li><li> 총 클라우드 스냅샷 시간은 이 시간을 스냅샷 업로드 시간에 더해서 계산합니다. 이 시간은 클라우드에 대한 인터넷 대역폭의 영향을 받습니다. |
| 최대 클라이언트 읽기/쓰기 처리량(SSD 계층에서 제공 시)* |단일 10GbE 네트워크 인터페이스와 함께 920/720MB/초 |MPIO 및 2개의 네트워크 인터페이스와 함께 최대 2x |
| 최대 클라이언트 읽기/쓰기 처리량(HDD 계층에서 제공 시)* |120/250MB/초 | |
| 업데이트 3 이상\*\*의 경우 최대 클라이언트 읽기/쓰기 처리량(클라우드 계층에서 제공 시)\* |계층화된 볼륨의 경우 40/60MB/s<br><br>볼륨을 만드는 동안 선택된 보관 옵션이 있는 계층화된 볼륨의 경우 60/80MB/s |읽기 처리량은 충분한 I/O 큐 깊이를 생성 및 유지 관리하는 클라이언트에 따라 달라집니다. <br><br>수행하는 속도는 사용되는 기본 스토리지 계정의 속도에 따라 달라 집니다. |

&#42; I/O 형식당 최대 처리량은 100% 읽기 및 100% 쓰기 시나리오로 측정되었습니다. 실제 처리량은 낮을 수 있으며 I/O 조합 및 네트워크 상태에 따라 다릅니다.

&#42;&#42; 업데이트 3 이전의 성능 수치는 이보다 낮을 수 있습니다.

## <a name="next-steps"></a>다음 단계
[StorSimple 시스템 요구 사항](storsimple-8000-system-requirements.md)을 검토하십시오.

