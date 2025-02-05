---
title: StorSimple 8000 시리즈 업데이트 2.2 릴리스 정보 | Microsoft Docs
description: StorSimple 8000 시리즈 업데이트 2.2의 새로운 기능, 문제 및 해결 방법을 설명합니다.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: ''
ms.assetid: 5cf03ea8-2a0f-4552-b6dc-7ea517783d7b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/03/2017
ms.author: alkohli
ms.openlocfilehash: 73b9ecd03875b60ed2d9b9d4c8e8a3a0c8de3cfa
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94956605"
---
# <a name="storsimple-8000-series-update-22-release-notes"></a>StorSimple 8000 시리즈 업데이트 2.2 릴리스 정보

## <a name="overview"></a>개요
다음 릴리스 정보는 새로운 기능에 대해 설명하고 StorSimple 8000 시리즈 업데이트 2.2에 대한 중요한 미해결 문제를 식별합니다. 또한 이 릴리스에 포함된 StorSimple 소프트웨어 업데이트 목록을 포함합니다.

업데이트 2.2는 릴리스(GA) 또는 업데이트 0.1~업데이트 2.1을 실행하는 모든 StorSimple 디바이스에 적용할 수 있습니다. 업데이트 2.2에 연결된 디바이스 버전은 6.3.9600.17708입니다.

StorSimple 솔루션에 업데이트를 배포하기 전에 릴리스 정보에 포함된 정보를 검토하십시오.

> [!IMPORTANT]
> * 업데이트 2.2에는 소프트웨어 전용 업데이트가 포함되어 있습니다. 이 업데이트를 설치하는 데는 1.5~2시간 정도 걸립니다. 
> * 업데이트 2.1을 실행하는 경우, 가능한 한 빨리 업데이트 2.2를 적용하는 것이 좋습니다.
> * 새 릴리스의 경우, 업데이트의 단계적 롤아웃을 수행하기 때문에 즉시 업데이트를 볼 수는 없습니다. 업데이트가 곧 제공될 예정이니 몇 일 후에 업데이트를 다시 검색하세요.
> 
> 

## <a name="whats-new-in-update-22"></a>업데이트 2.2의 새로운 기능
업데이트 2.2에는 다음과 같은 주요 향상 기능이 포함되어 있습니다.

* **자동화된 공간 재사용 최적화** : 씬 프로비전된 볼륨에서 데이터가 삭제된 경우 사용되지 않은 스토리지 블록을 재사용해야 합니다. 이 릴리스에서는 클라우드에서 공간 재사용 프로세스가 개선되어 이전 버전보다 사용되지 않은 공간을 더 빨리 사용할 수 있게 되었습니다.
* **스냅샷 성능 향상** - 업데이트 2.2에서는 큰 볼륨이 사용되고 데이터 변동이 최소이거나 없는 특정 시나리오에서 클라우드 스냅샷을 처리하는 데 걸리는 시간이 개선되었습니다. 이러한 향상에서 이점을 얻는 시나리오는 보관 볼륨입니다.
* **지원 패키지 수집 강화** - 이 릴리스에서는 지원 패키지가 수집 및 업로드되는 방식이 개선되었습니다. 
* **업데이트 안정성 향상** - 이 릴리스에는 업데이트 안정성을 향상하는 버그 수정이 포함되어 있습니다.

## <a name="issues-fixed-in-update-22"></a>업데이트 2.2에서 해결된 문제
다음 표에서는 업데이트 2.2 및 2.1에서 해결된 문제를 간략하게 설명합니다.    

| 아니요 | 기능 | 문제 | 실제 디바이스에 적용 | 가상 디바이스에 적용 |
| --- | --- | --- | --- | --- |
| 1 |호스트 성능 |이전 릴리스에서는 로컬로 고정된 볼륨을 만들고 계층화된 볼륨을 로컬로 고정된 볼륨으로 변환하는 동안 호스트 쪽 성능 문제가 관찰되었습니다. 이 릴리스에서는 이러한 문제가 해결되어 볼륨 만들기 및 변환 절차 동안 호스트 성능이 개선되었습니다. |예 |아니요 |
| 2 |로컬로 고정된 볼륨 |드물지만, 로컬로 고정된 볼륨을 만들 때 시스템 작동이 중단되는 경우가 있습니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 3 |계층화 |StorSimple Cloud Appliance(8010 및 8020)에 대한 메타데이터가 클라우드에 계층화된 경우 드물게 작동이 중단됩니다. 이 문제는 이 릴리스에서 해결되었습니다. |아니요 |예 |
| 4 |스냅샷 만들기 |큰 볼륨이 사용되고 데이터 변동이 최소이거나 없는 시나리오에서 증분 스냅샷 만들기와 관련된 문제가 있었습니다. 이러한 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 5 |Openstack 인증 |클라우드 서비스 공급자로 Openstack을 사용하는 경우 JSON 파서가 작동 중단되는 인증 관련 버그가 드물게 발생합니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 6 |호스트 쪽 복사 |이전 버전의 소프트웨어에서, 한 볼륨에서 다른 볼륨으로 데이터를 복사할 때 ODX 타이밍 관련 버그가 드물게 발생했습니다. 이로 인해 컨트롤러 장애 조치(failover)가 발생하고 시스템이 복구 보드로 전환될 수 있습니다. 이 버그는 이 릴리스에서 수정되었습니다. |예 |아니요 |
| 7 |WMI(Windows Management Instrumentation) |이전 버전의 소프트웨어에는 "\<ManagementException> 공급자 로드 실패입니다." 예외가 발생하는 웹 프록시 오류의 몇 가지 예가 있었습니다. 이 버그는 WMI 메모리 누수로 인해 발생했으며 이제 수정되었습니다. |예 |아니요 |
| 8 |업데이트 |이전 버전의 소프트웨어에서 특정 경우에 업데이트를 검색하거나 설치하려고 할 때 "CisPowershellHcsscripterror"가 드물게 발생했습니다. 이 문제는 이 릴리스에서 해결되었습니다. |예 |예 |
| 9 |지원 패키지 |이 릴리스에서는 지원 패키지가 수집 및 업로드되는 방식이 개선되었습니다. |예 |예 |

## <a name="known-issues-in-update-22"></a>업데이트 2.2의 알려진 문제
다음 표에서 이 릴리스의 알려진 문제를 간략하게 설명합니다.

| 아니요. | 기능 | 문제 | 주석/해결 방법 | 실제 디바이스에 적용 | 가상 디바이스에 적용 |
| --- | --- | --- | --- | --- | --- |
| 1 |디스크 쿼럼 |드문 경우에 8600 디바이스의 EBOD 인클로저에 있는 대부분의 디스크의 연결이 끊겨 디스크 쿼럼이 없는 경우, 스토리지 풀이 오프라인 상태가 됩니다. 디스크가 다시 연결되더라도 오프라인 상태로 유지됩니다. |디바이스를 다시 부팅해야 합니다. 문제가 지속되면 다음 단계에 대해 Microsoft 지원에 문의하세요. |예 |아니요 |
| 2 |잘못된 컨트롤러 ID |컨트롤러가 교체되면 컨트롤러 0이 컨트롤러 1로 표시될 수 있습니다. 컨트롤러 교체 중, 이미지가 피어 노드에서 로드되면 컨트롤러 ID는 처음에 피어 컨트롤러의 ID로 표시될 수 있습니다. 드문 경우에 시스템을 다시 부팅한 후 이 동작이 나타날 수도 있습니다. |추가적인 조치가 필요하지 않습니다. 컨트롤러 교체를 완료 한 후 이 상황이 저절로 해결됩니다. |예 |아니요 |
| 3 |Storage 계정 |Storage 계정 삭제에 Storage 서비스를 사용하는 것은 지원되지 않는 시나리오입니다. 이렇게 되면 사용자 데이터를 검색할 수 없게 됩니다. | |예 |예 |
| 4 |디바이스 장애 조치 |동일한 원본 디바이스에서 다른 대상 디바이스로의 볼륨 컨테이너의 다중 장애 조치는 지원되지 않습니다. 단일 데드 디바이스에서 여러 디바이스로의 장애 조치로 첫 번째 장애 조치된 디바이스의 볼륨 컨테이너에서 데이터 소유권이 손실됩니다. 이러한 장애 조치 후 Azure 클래식 포털에서 볼 때 이 볼륨 컨테이너가 나타나거나 다르게 동작합니다. | |예 |아니요 |
| 5 |설치 |SharePoint용 StorSimple 어댑터 설치 중, 성공적으로 설치를 완료하려면 장비 IP를 입력해야 합니다. | |예 |아니요 |
| 6 |웹 프록시 |웹 프록시 구성에 지정된 프로토콜로 HTTPS가 있는 경우, 디바이스 대 서비스의 통신에 영향을 줄 수 있으며 디바이스는 오프라인 상태가 됩니다. 지원 패키지는 디바이스에서 중요한 리소스를 소모하는 프로세스에도 생성됩니다. |웹 프록시 URL에 지정된 프로토콜로 HTTP가 있는지 확인합니다. 자세한 내용은 [디바이스에 웹 프록시 구성](./storsimple-8000-configure-web-proxy.md)으로 이동합니다. |예 |아니요 |
| 7 |웹 프록시 |등록된 디바이스에서 웹 프록시를 구성하고 사용하는 경우, 디바이스에서 활성 컨트롤러를 다시 시작해야 합니다. | |예 |아니요 |
| 8 |긴 클라우드 대기 시간 및 많은 I/O 작업 |StorSimple 디바이스에서 클라우드 대기 시간(초 순서)이 매우 길고 I/O 워크로드가 많으면 디바이스 볼륨의 성능이 저하되며 "디바이스가 준비 되지 않았습니다"라는 오류와 함께 I/O가 실패할 수 있습니다. |이 상황에서 복구하려면 수동으로 디바이스 컨트롤러를 다시 부팅하거나 디바이스 장애 조치를 수행해야 합니다. |예 |아니요 |
| 9 |Azure PowerShell |StorSimple cmdlet **Get-AzureStorSimpleStorageAccountCredential &#124; Select-Object -First 1 -Wait** 를 사용하여 새 **VolumeContainer** 개체를 만들 수 있도록 첫 번째 개체를 선택한 경우, cmdlet은 모든 개체를 리턴합니다. |다음과 같이 cmdlet을 괄호로 래핑합니다. **(Get-Azure-StorSimpleStorageAccountCredential) &#124; Select-Object -First 1 -Wait** |예 |예 |
| 10 |마이그레이션 |여러 볼륨 컨테이너가 마이그레이션을 위해 전달되는 경우, 최신 백업에 대한 ETA는 첫 번째 볼륨 컨테이너에 대해서만 정확합니다. 또한 병렬 마이그레이션은 첫 번째 볼륨 컨테이너에서 처음 4개의 백업이 마이그레이션된 후 시작됩니다. |한번에 하나의 볼륨 컨테이너를 마이그레이션하는 것이 좋습니다. |예 |아니요 |
| 11 |마이그레이션 |복원 후 볼륨은 백업 정책 또는 가상 디스크 그룹에 추가되지 않습니다. |백업을 만들기 위해 이러한 볼륨을 백업 정책에 추가해야 합니다. |예 |예 |
| 12 |마이그레이션 |마이그레이션이 완료되면 5000/7000 시리즈 디바이스는 마이그레이션된 데이터 컨테이너에 액세스하지 않아야 합니다. |마이그레이션이 완료되고 커밋된 후 마이그레이션된 데이터 컨테이너를 삭제하는 것이 좋습니다. |예 |아니요 |
| 13 |복제 및 DR |업데이트 1을 실행하는 StorSimple 디바이스는 사전 업데이트 1 소프트웨어를 실행하는 디바이스에 대한 재해 복구를 복제하거나 수행할 수 없습니다. |이러한 작업을 허용하려면 대상 디바이스를 업데이트 1로 업데이트해야 합니다. |예 |예 |
| 14 |마이그레이션 |볼륨 그룹과 연결된 볼륨이 없으면 마이그레이션에 대한 구성 백업은 5000-7000 시리즈 디바이스에서 실패할 수 있습니다. |연결된 볼륨이 없는 모든 빈 볼륨 그룹을 삭제한 다음 구성 백업을 다시 시도하세요. |예 |아니요 |
| 15 |Azure PowerShell cmdlet 및 로컬에 고정된 볼륨 |Azure PowerShell cmdlet을 통해 로컬에 고정된 볼륨을 만들 수 없습니다. (Azure PowerShell을 통해 만드는 모든 볼륨은 계층화됩니다.) |로컬에 고정된 볼륨을 구성하려면 항상 StorSimple 관리자 서비스를 사용하세요. |예 |아니요 |
| 16 |로컬에 고정된 볼륨에 사용 가능한 공간 |로컬에 고정된 볼륨을 삭제하면 새 볼륨에 사용할 수 있는 공간이 즉시 업데이트되지 않을 수 있습니다. StorSimple 관리자 서비스는 사용 가능한 로컬 공간을 거의 매 시간마다 업데이트합니다. |새 볼륨을 만들기 전에 한 시간을 기다려 주세요. |예 |아니요 |
| 17 |로컬로 고정된 볼륨 |복원 작업에서는 Backup 카탈로그의 임시 스냅샷 백업을 복원 작업 기간에만 노출합니다. 또한 접두사 **tmpCollection** 이 붙은 가상 디스크 그룹을 **Backup 정책** 페이지에 복원 작업 기간에만 노출합니다. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 복원 작업에 계층화된 볼륨만 있으면 이 동작이 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 18 |로컬로 고정된 볼륨 |복원 작업을 취소하면 그 즉시 컨트롤러 장애 조치(failover)가 발생하고, 복원 작업에서는 **취소됨** 대신 **실패** 를 표시합니다. 복원 작업을 취소하면 그 즉시 컨트롤러 장애 조치(failover)가 발생하고, 복원 작업에서는 **취소됨** 대신 **실패** 로 표시합니다. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 복원 작업에 계층화된 볼륨만 있으면 이 동작이 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 19 |로컬로 고정된 볼륨 |복원 작업을 취소하거나 복원이 실패하면 컨트롤러 장애 조치(failover)가 발생하고 **작업** 페이지에 추가 복원 작업이 나타납니다. |복원 작업에 로컬로 고정된 볼륨만 있거나 로컬로 고정된 볼륨과 계층화된 볼륨이 함께 있는 경우에 이 동작이 발생할 수 있습니다. 복원 작업에 계층화된 볼륨만 있으면 이 동작이 발생 하지 않습니다. 사용자 개입이 필요 없습니다. |예 |아니요 |
| 20 |로컬로 고정된 볼륨 |계층화된 볼륨(업데이트 1.2 이전을 통해 생성 또는 복제됨)을 로컬로 고정된 볼륨으로 변환하려고 하고 디바이스에 공간이 부족하거나 클라우드가 중단된 경우 복제는 손상될 수 있습니다. |이 문제는 업데이트 2.1 이전 소프트웨어로 만들어지고 복제된 볼륨을 사용하는 경우에만 발생합니다. 자주 발생하지 않는 시나리오여야 합니다. | | |
| 21 |볼륨 변환 |볼륨 변환이 진행 중인 동안 볼륨에 연결된 ACR을 업데이트하지 마세요.(로컬로 고정된 볼륨에 계층화되거나 그 반대임) ACR를 업데이트하는 작업은 데이터가 손상될 수 있습니다. |필요한 경우 볼륨 변환 전에 ACR을 업데이트하고 변환이 진행 중인 동안 ACR을 더 이상 업데이트하지 않습니다. | | |

## <a name="controller-and-firmware-updates-in-update-22"></a>업데이트 2.2의 컨트롤러 및 펌웨어 업데이트
이 릴리스에는 소프트웨어 전용 업데이트가 포함되어 있습니다. 그러나 업데이트 2 이전 버전에서 업데이트하는 경우 디바이스에서 드라이버, Spaceport, Storport 및 (일부 경우) 디스크 펌웨어 업데이트를 설치해야 합니다.

드라이버, Storport, Spaceport 및 디스크 펌웨어 업데이트를 설치하는 방법에 대한 자세한 내용은 StorSimple 디바이스의 [업데이트 2.2 설치](./storsimple-8000-install-update-5.md)를 참조하세요.

## <a name="virtual-device-updates-in-update-22"></a>업데이트 2.2의 가상 디바이스 업데이트
이 업데이트는 가상 디바이스에 적용할 수 없습니다. 새 가상 디바이스를 만들어야 합니다. 

## <a name="next-step"></a>다음 단계
StorSimple 디바이스에 [업데이트 2.2를 설치](./storsimple-8000-install-update-5.md)하는 방법을 알아봅니다.