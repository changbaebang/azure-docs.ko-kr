---
title: 정부 포털에서 StorSimple 8000 시리즈 디바이스 배포 | Microsoft Docs
description: Azure Government 포털에서 업데이트 3 이상을 실행하는 StorSimple 8000 시리즈 디바이스 및 서비스를 배포하기 위한 단계와 모범 사례를 설명합니다.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: ''
ms.assetid: ''
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: alkohli
ms.openlocfilehash: d736c09fc1c9490f79dfc526895970e01b8b45cc
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94963184"
---
# <a name="deploy-your-on-premises-storsimple-device-in-the-government-portal"></a>Government 포털에서 온-프레미스 StorSimple 디바이스 배포

[!INCLUDE [storsimple-8000-eol-banner](../../includes/storsimple-8000-eol-banner.md)]

## <a name="overview"></a>개요
Microsoft Azure StorSimple 디바이스 배포를 시작합니다. 이러한 배포 자습서는 Azure Government 포털에서 업데이트 3 소프트웨어 이상을 실행하는 StorSimple 8000 시리즈에 적용됩니다. 이 자습서 시리즈에서는 StorSimple 디바이스를 구성하는 방법에 대해 설명하며 구성 검사 목록, 구성 필수 조건 목록 및 자세한 구성 단계를 포함합니다.

이 자습서의 정보는 안전 주의 사항을 검토했으며, StorSimple 디바이스의 포장을 풀었고, 랙을 탑재했으며, 케이블에 연결되어 있다고 가정합니다. 여전히 이러한 작업을 수행해야 하는 경우 [안전 주의 사항](storsimple-8000-safety.md)검토로 시작하세요. 디바이스를 개봉, 랙 탑재 및 케이블로 연결하려면 디바이스별 지침을 따릅니다.

* [8100 개봉, 랙 탑재, 케이블 연결](storsimple-8100-hardware-installation.md)
* [8600 개봉, 랙 탑재, 케이블 연결](storsimple-8600-hardware-installation.md)

설치 및 구성 프로세스를 완료하려면 관리자 권한이 필요합니다. 시작하기 전에 구성 검사 목록을 검토하는 것이 좋습니다. 배포 및 구성 프로세스는 완료하는 데 다소 시간이 걸릴 수 있습니다.

> [!NOTE]
> Microsoft Azure 웹 사이트에 게시된 StorSimple 배포 정보는 StorSimple 8000 시리즈 디바이스에만 적용됩니다. 7000 시리즈 장치에 대 한 자세한 내용은 항목을 참조 하세요 [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com) . 7000 시리즈 배포 정보는 [StorSimple 시스템 퀵 스타트 가이드](http://onlinehelp.storsimple.com/111_Appliance/)를 참조하세요.


## <a name="deployment-steps"></a>배포 단계
StorSimple 디바이스를 구성하여 StorSimple 디바이스 관리자 서비스에 연결하려면 다음과 같은 필수 단계를 수행합니다. 필수 단계 외에 선택적 단계 및 배포하는 동안 완료해야 할 수도 있는 절차가 있습니다. 단계별 배포 지침은 각 선택적 단계를 수행해야 하는 시기를 나타냅니다.

| 단계 | 설명 |
| --- | --- |
| **사전** |향후 배포 준비 과정에서 완료해야 합니다. |
| [배포 구성 검사 목록](#deployment-configuration-checklist) |이 검사 목록을 사용하여 배포 이전 및 배포하는 동안 정보를 수집하고 기록합니다. |
| [배포 필수 조건](#deployment-prerequisites) |배포할 준비가 되어 있는 환경인지 유효성을 검사합니다. |
|  | |
| **단계별 배포** |프로덕션 환경에서 StorSimple 디바이스를 배포하려면 다음 단계가 필요합니다. |
| [1 단계: 새 서비스 만들기](#step-1-create-a-new-service) |StorSimple 디바이스에 대한 클라우드 관리 및 스토리지를 설정합니다. *다른 StorSimple 디바이스에 대해 기존 서비스가 있는 경우 이 단계를 건너뜁니다*. |
| [2 단계: 서비스 등록 키 가져오기](#step-2-get-the-service-registration-key) |이 키를 사용하여 StorSimple 디바이스를 관리 서비스에 등록 및 연결합니다. |
| [3단계: StorSimple용 Windows PowerShell을 통해 디바이스 구성 및 등록](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |디바이스를 네트워크에 연결하고 관리 서비스를 사용하여 Azure로 등록하여 설정을 완료합니다. |
| [4단계: 최소 디바이스 설정 완료](#step-4-complete-minimum-device-setup) </br>선택 사항: StorSimple 디바이스를 업데이트합니다. |관리 서비스를 사용하여 디바이스 설정을 완료하고 스토리지를 제공할 수 있도록 설정합니다. |
| [5단계: 볼륨 컨테이너 만들기](#step-5-create-a-volume-container) |볼륨을 프로비전할 컨테이너를 만듭니다. 볼륨 컨테이너에는 스토리지 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다. |
| [6 단계: 볼륨 만들기](#step-6-create-a-volume) |서버에 대한 StorSimple 디바이스의 스토리지 볼륨을 프로비전합니다. |
| [7단계: 볼륨 탑재, 초기화 및 포맷](#step-7-mount-initialize-and-format-a-volume) </br>선택 사항: MPIO를 구성합니다. |서버를 디바이스에서 제공하는 iSCSI 스토리지에 연결합니다. 필요에 따라 MPIO를 구성하여 서버가 링크, 네트워크 및 인터페이스 실패를 허용할 수 있도록 합니다. |
| [8단계: 백업 수행](#step-8-take-a-backup) |백업 정책을 설정하여 데이터 보호 |
|  | |
| **기타 절차** |솔루션을 배포하는 경우 이러한 절차를 참조해야 합니다. |
| [서비스에 대 한 새 저장소 계정 구성](#configure-a-new-storage-account-for-the-service) | |
| [PuTTY를 사용 하 여 장치 직렬 콘솔에 연결](#use-putty-to-connect-to-the-device-serial-console) | |
| [업데이트 검색 및 적용](#scan-for-and-apply-updates) | |
| [Windows Server 호스트의 IQN 가져오기](#get-the-iqn-of-a-windows-server-host) | |
| [수동 백업 만들기](#create-a-manual-backup) | |


## <a name="deployment-configuration-checklist"></a>배포 구성 검사 목록
StorSimple 디바이스를 배포하기 전에 정보를 수집하여 디바이스에 소프트웨어를 구성해야 합니다. 이 정보의 일부를 미리 준비하면 사용자 환경에서 StorSimple 디바이스를 배포하는 과정을 간소화하는데 도움이 됩니다. 또한 이 검사 목록을 다운로드 및 사용하여 디바이스를 배포하는 동안 구성 세부 정보를 기록합니다.

[StorSimple 배포 구성 검사 목록 다운로드](https://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>배포 필수 조건
다음 섹션에서는 StorSimple 디바이스 관리자 서비스 및 StorSimple 디바이스에 대한 필수 조건에 대해 설명합니다.

### <a name="for-the-storsimple-device-manager-service"></a>StorSimple 디바이스 관리자 서비스의 경우
시작하기 전에 다음 사항을 확인합니다.

* 액세스 자격 증명이 있는 Microsoft 계정이 있습니다.
* 액세스 자격 증명이 있는 Microsoft Azure Storage 계정이 있습니다.
* 사용자의 Microsoft Azure 구독을 StorSimple 디바이스 관리자 서비스에 사용할 수 있습니다. 구독은 [기업 계약](https://azure.microsoft.com/pricing/enterprise-agreement/)을 통해 구매해야 합니다.
* PuTTY와 같은 터미널 에뮬레이션 소프트웨어에 액세스할 수 있습니다.

### <a name="for-the-device-in-the-datacenter"></a>데이터 센터에서 디바이스의 경우
디바이스를 구성하기 전에 다음 사항을 확인합니다.

* 다음에서 설명한 대로 디바이스가 완전히 개봉, 랙에 탑재되고 전원, 네트워크 및 직렬 액세스에 완전히 연결되었습니다.
  
  * [8100 디바이스 개봉, 랙 탑재, 케이블 연결](storsimple-8100-hardware-installation.md)
  * [8600 디바이스 개봉, 랙 탑재, 케이블 연결](storsimple-8600-hardware-installation.md)

### <a name="for-the-network-in-the-datacenter"></a>데이터 센터에서 네트워크의 경우
시작하기 전에 다음 사항을 확인합니다.

* [StorSimple 디바이스에 대한 네트워킹 요구 사항](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device)에서 설명한 대로 데이터 센터 방화벽에서 포트가 열려 있어 iSCSI 및 클라우드 트래픽을 허용합니다.

## <a name="step-by-step-deployment"></a>단계별 배포
다음 단계별 지침을 사용하여 데이터 센터에서 StorSimple 디바이스를 배포합니다.

## <a name="step-1-create-a-new-service"></a>1단계: 새 서비스 만들기
StorSimple 디바이스 관리자 서비스는 여러 StorSimple 디바이스를 관리할 수 있습니다. StorSimple 디바이스 관리자 서비스의 새 인스턴스를 만들려면 다음 단계를 수행합니다.

[!INCLUDE [storsimple-8000-create-new-service-gov](../../includes/storsimple-8000-create-new-service-gov.md)]

> [!IMPORTANT]
> 서비스와 함께 스토리지 계정을 자동으로 만들도록 설정하지 않은 경우, 서비스를 성공적으로 만든 후 하나 이상의 스토리지 계정을 만들어야 합니다. 이 스토리지 계정은 볼륨 컨테이너를 만들 때 사용됩니다.
> 
> * 스토리지 계정을 자동으로 만들지 않은 경우 자세한 지침은 [서비스에 대한 새 스토리지 계정 구성](#configure-a-new-storage-account-for-the-service) 을 참조하세요.
> * 스토리지 계정을 자동으로 생성하도록 설정한 경우, [2단계: 서비스 등록 키 받기](#step-2-get-the-service-registration-key)로 이동합니다.


## <a name="step-2-get-the-service-registration-key"></a>2단계: 서비스 등록 키 받기
StorSimple 디바이스 관리자 서비스를 실행한 후에는 서비스 등록 키를 받아야 합니다. 이 키는 StorSimple 디바이스를 서비스에 등록 및 연결하는 데 사용됩니다.

Government 포털에서 다음 단계를 수행합니다.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple"></a>3단계: StorSimple용 Windows PowerShell을 통해 디바이스 구성 및 등록
다음 절차에서 설명한 대로 StorSimple 디바이스의 초기 설정을 완료하려면 StorSimple용 Windows PowerShell을 사용합니다. 이 단계를 완료하려면 터미널 에뮬레이션 소프트웨어를 사용해야 합니다. 자세한 내용은 [디바이스 직렬 콘솔 연결에 PuTTY 사용](#use-putty-to-connect-to-the-device-serial-console)을 참조하세요.

[!INCLUDE [storsimple-8000-configure-and-register-device-gov](../../includes/storsimple-8000-configure-and-register-device-gov-u2.md)]

## <a name="step-4-complete-minimum-device-setup"></a>4단계: 최소 디바이스 설정 완료
StorSimple 디바이스의 최소 디바이스 구성에는 다음 사항이 필요합니다.

* 디바이스에 대한 친숙한 이름을 제공합니다.
* 디바이스 표준 시간대를 설정합니다.
* 두 컨트롤러에 고정된 IP 주소를 할당합니다.

Azure Government 포털에서 최소 디바이스 설정을 완료하려면 Government 포털에서 다음 단계를 수행합니다.

[!INCLUDE [storsimple-8000-complete-minimum-device-setup-u2](../../includes/storsimple-8000-complete-minimum-device-setup-u2.md)]

## <a name="step-5-create-a-volume-container"></a>5단계: 볼륨 컨테이너 만들기
볼륨 컨테이너에는 스토리지 계정, 대역폭 및 그 안에 포함된 모든 볼륨에 대한 암호화 설정이 있습니다. StorSimple 디바이스에서 볼륨 프로비저닝을 시작하려면 볼륨 컨테이너를 만들어야 합니다.

볼륨 컨테이너를 만들려면 Government 포털에서 다음 단계를 수행합니다.

[!INCLUDE [storsimple-8000-create-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>6단계: 볼륨 만들기
볼륨 컨테이너를 만든 후에 서버에 대한 StorSimple 디바이스에 스토리지 볼륨을 프로비전할 수 있습니다. 볼륨을 만들려면 Government 포털에서 다음 단계를 수행합니다.

> [!IMPORTANT]
> StorSimple 디바이스 관리자는 씬 프로비저닝된 볼륨만 만들 수 있습니다.  그러나 부분적으로 프로비전된 볼륨은 만들 수 없습니다.

[!INCLUDE [storsimple-8000-create-volume](../../includes/storsimple-8000-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>7단계: 볼륨 탑재, 초기화 및 포맷
Windows Server 호스트에서 이러한 단계를 수행합니다.

> [!IMPORTANT]
> * StorSimple 솔루션의 고가용성을 위해 iSCSI를 구성하기 전에 호스트 서버에 MPIO를 구성하는 것이 좋습니다(선택 사항). 호스트 서버에 MPIO를 구성하면 서버가 링크, 네트워크 또는 인터페이스 오류를 허용할 수 있습니다.
> * Windows Server 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple 디바이스에 대한 MPIO 구성](./storsimple-8000-configure-mpio-windows-server.md)으로 이동합니다. StorSimple 볼륨을 탑재, 초기화 및 포맷하는 단계도 포함됩니다.
> * Linux 호스트에서 MPIO 및 iSCSI 설치 및 구성 지침은 [StorSimple Linux 호스트에 대한 MPIO 구성](storsimple-configure-mpio-on-linux.md)

MPIO를 구성하지 않으려는 경우 다음 단계를 수행하여 Windows Server 호스트에서 StorSimple 볼륨을 탑재, 초기화 및 포맷합니다.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>8단계: 백업 수행
Backup은 볼륨의 지정 시간 보호 기능을 제공하며 복원 시간을 최소화하면서 복구 기능을 개선합니다. StorSimple 디바이스에서 두 유형(로컬 스냅샷 및 클라우드 스냅샷)의 백업을 수행할 수 있습니다. 이러한 각 백업 유형은 **예약된 백업** 일 수도 있고 **수동 백업** 일 수도 있습니다.

예약된 백업을 만들려면 Government 포털에서 다음 단계를 수행합니다.

[!INCLUDE [storsimple-8000-take-backup](../../includes/storsimple-8000-take-backup.md)]

언제든지 수동 백업을 수행할 수 있습니다. 과정은 [수동 백업 만들기](#create-a-manual-backup)로 이동합니다.

## <a name="configure-a-new-storage-account-for-the-service"></a>서비스에 대한 새 스토리지 계정 구성
서비스와 스토리지 계정을 자동으로 생성하도록 설정하지 않은 경우에만 수행해야 하는 선택적 단계입니다. StorSimple 볼륨 컨테이너를 만들려면 Microsoft Azure Storage 계정이 필요합니다.

다른 지역에 Azure Storage 계정을 만들어야 하는 경우 단계별 지침은 [Azure Storage 계정 정보](../storage/common/storage-account-create.md) 를 참조하세요.

Government 포털의 **StorSimple 디바이스 관리자 서비스** 페이지에서 다음 단계를 수행합니다.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

## <a name="use-putty-to-connect-to-the-device-serial-console"></a>디바이스 직렬 콘솔 연결에 PuTTY 사용
StorSimple용 Windows PowerShell에 연결하려면 PuTTY와 같은 터미널 에뮬레이션 소프트웨어를 사용해야 합니다. 직렬 콘솔을 통해 직접 또는 원격 컴퓨터에서 텔넷 세션을 열어 디바이스에 액세스할 때 PuTTY를 사용할 수 있습니다.

[!INCLUDE [Use PuTTY to connect to the device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>업데이트 검색 및 적용
디바이스 업데이트는 몇 시간이 걸릴 수 있습니다. 최신 업데이트를 설치하는 방법에 대한 자세한 단계는 [업데이트 4 설치](storsimple-8000-install-update-4.md)로 이동하세요.

## <a name="get-the-iqn-of-a-windows-server-host"></a>Windows Server 호스트의 IQN 가져오기
Windows Server® 2012를 실행하는 Windows 호스트의 iSCSI 정규화된 이름(IQN)을 가져오려면 다음 단계를 수행합니다.

[!INCLUDE [Get IQN of your Windows Server host](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>수동 백업 만들기
StorSimple 디바이스에서 단일 볼륨에 대한 주문형 수동 백업을 만들려면 Government 포털에서 다음 단계를 수행합니다.

[!INCLUDE [Create a manual backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>다음 단계
* [가상 디바이스](storsimple-8000-cloud-appliance-u2.md)를 구성합니다.
* Storsimple [장치 관리자 서비스](storsimple-8000-manager-service-administration.md) 를 사용 하 여 storsimple 장치를 관리 합니다.