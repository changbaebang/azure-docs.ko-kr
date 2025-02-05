---
author: alkohli
ms.service: storsimple
ms.topic: include
ms.date: 10/26/2018
ms.author: alkohli
ms.openlocfilehash: 658fd9178495f14274c85eab2129c9dcd3be7693
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "67182234"
---
| **제한 식별자** | **제한** | **설명** |
| --- | --- | --- |
| 총 용량(클라우드 포함) |가상 디바이스당 최대 64TB |전체 StorSimple 가상 배열을 다른 빈 배열에 장애 조치(Failover)할 수 있습니다. 동일한 디바이스를 복원하려는 경우 이 작업을 완료하기에 충분한 공간이 디바이스에 있는지 확인합니다. 32TB을 초과한 후에는 동일한 디바이스에 복원할 수 없습니다. |
| 디바이스당 스토리지 계정 자격 증명의 최대 수 |1 | |
| 볼륨/공유 최대 수 |16 | |
| 계층화 공유의 최소 크기 |500GB | |
| 계층화 볼륨의 최소 크기 |500GB | |
| 계층화 공유의 최대 크기 |20TB | |
| 계층화 볼륨의 최대 크기 |5TB | |
| 로컬로 고정된 공유의 최소 크기 |50GB | |
| 로컬로 고정된 볼륨의 최소 크기 |50GB | |
| 로컬로 고정된 공유의 최대 크기 |2TB | |
| 로컬로 고정된 볼륨의 최대 크기 |200GB | |
| 초기자에서 iSCSI 연결의 최대 수 |512 | |
| 디바이스당 액세스 제어 레코드의 최대 수 |64 | |
| 가상 디바이스에 의해 파일 서버의 *.backups* 폴더에 보존되는 백업의 최대 수 |5 |여기에는 가장 최근에 예약된(기본 백업 정책에 의해 생성되는) 백업과 수동 백업이 포함됩니다. |
| 디바이스에 의해 보존되는 예약된 백업의 최대 수 |55 |일별 백업 30개<br>월별 백업 12개<br>연도별 백업 13개 |
| 디바이스에 의해 보존되는 수동 백업의 최대 수 |45 | |
| 파일 서버에 대한 공유당 최대 파일 수 |1백만 |디바이스 복원을 수행할 때 복원 시간은 디바이스의 모든 공유에 있는 파일의 수에 비례합니다. |
| iSCSI 서버에 대한 볼륨당 최대 파일 수 |1백만 | |
| 가상 배열 당 최대 파일 수 |400만 | |
| 복구 시간 복원 |빠른 복원 |복원은 열 지도를 기반으로 하며 볼륨 크기에 따라 달라집니다.<br>Backup 작업은 복원 작업이 진행 중일 때 발생할 수 있습니다. |

