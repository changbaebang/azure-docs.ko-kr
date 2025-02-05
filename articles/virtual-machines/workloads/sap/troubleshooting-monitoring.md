---
title: Azure의 SAP HANA(대규모 인스턴스) 모니터링 | Microsoft Docs
description: Azure의 SAP HANA(대규모 인스턴스)를 모니터링합니다.
services: virtual-machines-linux
documentationcenter: ''
author: msjuergent
manager: bburns
editor: ''
ms.service: virtual-machines-sap
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/10/2018
ms.author: juergent
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 246b9398824597ec337ee9e9ea3dc24267311f60
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101669599"
---
# <a name="how-to-monitor-sap-hana-large-instances-on-azure"></a>Azure의 SAP HANA(대규모 인스턴스)를 모니터링하는 방법

Azure의 SAP HANA(대규모 인스턴스)는 다른 IaaS 배포와 다르지 않습니다. OS 및 애플리케이션이 수행하는 작업 및 애플리케이션이 다음 리소스 사용하는 방법을 모니터링해야 합니다.

- CPU
- 메모리
- 네트워크 대역폭
- 디스크 공간

Azure Virtual Machines를 사용하여 위에 명시된 리소스 클래스가 충분한지 또는 고갈되는지 여부를 파악해야 합니다. 다른 클래스 각각에 대한 자세한 내용은 다음과 같습니다.

**CPU 리소스 소비량:** 메모리에 저장되는 데이터를 사용할 수 있는 CPU 리소스가 충분하도록 하기 위해 SAP에서 HANA에 대한 특정 워크로드에 정의한 비율이 적용됩니다. 그럼에도 HANA가 누락된 인덱스 또는 유사한 문제점으로 인해 쿼리를 실행하는 데 많은 CPU를 사용할 수 있습니다. 즉, HANA 큰 인스턴스 단위의 CPU 리소스 사용량뿐만 아니라 특정 HANA 서비스에서 사용하는 CPU 리소스를 모니터링해야 합니다.

**메모리 사용량:** 단위의 HANA 외부뿐만 아니라 HANA 내부에서도 모니터링해야 합니다. HANA 내에서 데이터가 SAP의 필수 크기 조정 지침 내로 유지되기 위해 HANA 할당 메모리를 사용하는 방법을 모니터링합니다. 또한 큰 인스턴스 수준에서 메모리 사용량을 모니터링하여 추가 설치된 HANA 이외의 소프트웨어가 너무 많은 메모리를 소비하게 되어 메모리를 두고 HANA와 경쟁하지 않도록 하려고 합니다.

**네트워크 대역폭:** Azure VNet 게이트웨이는 Azure VNet으로 이동하는 데이터의 대역폭으로 제한됩니다. 따라서 VNet 내의 모든 Azure VM에서 수신한 데이터를 모니터링하여 선택한 Azure 게이트웨이 SKU의 제한에 얼마나 근접했는지 파악하는 데 유용합니다. HANA 큰 인스턴스 단위에서 들어오고 나가는 네트워크 트래픽도 모니터링하고 시간이 지남에 따라 처리되는 볼륨도 추적하는 것이 합리적입니다.

**디스크 공간:** 디스크 공간 사용량은 일반적으로 시간이 지남에 따라 증가합니다. 가장 일반적인 이유는 데이터 볼륨 증가, 트랜잭션 로그 백업 실행, 추적 파일 저장 및 스토리지 스냅샷 수행입니다. 따라서 디스크 공간 사용량을 모니터링하고 HANA 큰 인스턴스 단위와 연결된 디스크 공간을 관리하는 것이 중요합니다.

HANA 대규모 인스턴스의 **유형 II SKU** 에서 서버에는 미리 로드된 시스템 진단 도구가 포함됩니다. 이러한 진단 도구를 사용하여 시스템 상태 검사를 수행할 수 있습니다. 다음 명령을 실행하여 /var/log/health_check에서 상태 검사 로그 파일을 생성합니다.
```
/opt/sgi/health_check/microsoft_tdi.sh
```
Microsoft 지원 팀과 함께 문제를 해결할 경우 이러한 진단 도구를 사용하여 로그 파일을 제공하도록 요청될 수 있습니다. 다음 명령을 사용하여 파일을 zip으로 압축할 수 있습니다.
```
tar  -czvf health_check_logs.tar.gz /var/log/health_check
```

**다음 단계**

- [Azure의 SAP HANA(대규모 인스턴스)를 모니터링하는 방법](./hana-monitor-troubleshoot.md)을 참조하세요.
