---
title: Azure Database for PostgreSQL 단일 서버
description: Azure Database for PostgreSQL - 단일 서버에 대한 개요를 제공합니다.
author: sunilagarwal
ms.author: sunila
ms.custom: mvc
ms.service: postgresql
ms.topic: overview
ms.date: 09/21/2020
ms.openlocfilehash: 18d944cd2b3bfde1a0ee5fc53e83e4016b11b01f
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "100379219"
---
# <a name="azure-database-for-postgresql-single-server"></a>Azure Database for PostgreSQL 단일 서버

PostgreSQL 커뮤니티 버전에서 제공하는 [Azure Database for PostgreSQL](./overview.md)은 다음과 같은 세 가지 배포 모드로 사용할 수 있습니다.

- 단일 서버
- 유연한 서버(미리 보기)
- 하이퍼스케일(Citus)

이 문서에서는 단일한 서버 배포 모델의 핵심 개념을 간략하게 설명하고 소개합니다. 유연한 서버 배포 모드에 대해 알아보려면 [유연한 서버 개요](./flexible-server/overview.md) 및 하이퍼스케일(Citus) 개요를 참조하세요.

## <a name="overview"></a>개요

단일 서버는 데이터베이스 사용자 지정을 최소화한 완전 관리형 데이터베이스 서비스입니다. 단일 서버 플랫폼은 최소한의 사용자 구성과 제어를 통해 패치, 백업, 고가용성, 보안 등 대부분의 데이터베이스 관리 기능을 처리하도록 설계되었습니다. 아키텍처는 단일 가용성 영역에서 99.99%의 가용성을 제공하도록 최적화되었습니다. PostgreSQL 커뮤니티 버전 9.5, 9.6, 10 및 11을 지원합니다. 이 서비스는 현재 다양한 [Azure 지역](https://azure.microsoft.com/global-infrastructure/services/)에서 일반 공급됩니다.

단일 서버는 패치 일정 및 사용자 지정 PostgreSQL 구성 설정에 대한 세부적인 제어 없이 자동화된 패치를 처리하도록 설계된 클라우드 네이티브 애플리케이션에 가장 적합합니다.

## <a name="high-availability"></a>고가용성

단일 서버 배포 모델은 저렴한 가격으로 기본 제공 고가용성 및 탄력성을 제공하도록 최적화되었습니다. 아키텍처는 컴퓨팅과 스토리지를 분리합니다. 데이터베이스 엔진은 독점적 컴퓨팅 컨테이너에서 실행되는 반면, 데이터 파일은 Azure 스토리지에 상주합니다. 스토리지는 데이터 내구성을 보장하는 데이터베이스 파일의 세 가지 로컬 중복 동기 복사본을 유지 관리합니다.

계획되거나 계획되지 않은 장애 조치(failover) 이벤트가 발생하는 동안 서버가 다운되면 서비스는 다음과 같은 자동화된 절차를 사용하여 서버의 고가용성을 유지합니다.

1. 새 컴퓨팅 컨테이너가 프로비저닝됩니다.
2. 데이터 파일이 있는 스토리지가 새 컨테이너에 매핑됩니다.
3. 새 컴퓨팅 컨테이너에서 PostgreSQL 데이터베이스 엔진이 온라인 상태로 전환됩니다.
4. 게이트웨이 서비스는 투명한 장애 조치(failover)를 보장하여 애플리케이션 쪽에서 변경할 필요가 없습니다
   
 :::image type="content" source="./media/overview/overview-azure-postgres-single-server.png" alt-text="Azure Database for PostgreSQL 단일 서버":::

일반적인 장애 조치(failover) 시간 범위는 60-120초입니다. 단일 서버 서비스의 클라우드 기본 설계를 통해 99.99%의 가용성을 지원하므로 패시브 상시 대기 비용이 들지 않습니다.

업계 최고 수준을 자랑하는 Azure의 99.99% 가용성 SLA(서비스 수준 계약)를 Microsoft에서 관리하는 글로벌 데이터 센터 네트워크의 지원을 받아 애플리케이션을 연중 무휴(24/7) 실행할 수 있습니다.

## <a name="automated-patching"></a>자동화된 패치

서비스는 기본 하드웨어, OS 및 데이터베이스 엔진의 자동화된 패치를 수행합니다. 패치에는 보안 및 소프트웨어 업데이트가 포함됩니다. PostgreSQL 엔진의 경우 부 버전 업그레이드는 자동으로 적용되며 패치 주기에 포함됩니다. 패치를 적용하는 데 필요한 사용자 작업 또는 구성 설정은 없습니다. 패치 주기는 페이로드의 중요도에 따라 관리되는 서비스입니다. 일반적으로 서비스는 연속 통합 및 릴리스의 일부로 월별 릴리스 일정을 따릅니다. 사용자는 [계획된 유지 관리 알림]()을 구독하여 이벤트 72시간 전에 예정된 유지 관리 알림을 받을 수 있습니다.

## <a name="automatic-backups"></a>자동 백업

단일 서버 서비스는 자동으로 서버 백업을 만들어 사용자가 로컬로 구성한 중복 스토리지(LRS) 또는 지역 중복 스토리지에 저장합니다. 백업을 통해 백업 보존 기간 내의 특정 지점으로 서버를 복원할 수 있습니다. 기본 백업 보존 기간은 7일입니다. 보존 기간은 선택적으로 최대 35일까지 구성할 수 있습니다. 모든 백업은 AES 256비트 암호화를 사용하여 암호화됩니다. 자세한 내용은 [백업](./concepts-backup.md)을 참조하세요.

## <a name="adjust-performance-and-scale-within-seconds"></a>몇 초 이내 성능 및 규모 조정

단일 서버 서비스는 기본, 범용 및 메모리 최적화의 세 가지 가격 책정 계층 중 하나에서 만들 수 있습니다. 기본 계층은 저렴한 개발과 낮은 동시성 워크로드에 가장 적합합니다. 범용 및 메모리 최적화는 높은 동시성, 규모 및 예측 가능한 성능이 필요한 프로덕션 워크로드에 더 적합합니다. 한 달에 몇 달러로 작은 데이터베이스에 첫 번째 앱을 빌드하고 솔루션의 요구에 맞게 규모를 조정할 수 있습니다. 스토리지 스케일링은 온라인으로 수행되며 스토리지 자동 확장을 지원합니다. 동적 확장성을 사용하면 데이터베이스가 빠르게 변화하는 리소스 요구 사항에 투명하게 대응할 수 있습니다. 사용하는 리소스 비용만 지불하면 됩니다. 자세한 내용은 [가격 책정 계층]()을 참조하세요.

## <a name="enterprise-grade-security-compliance-and-governance"></a>엔터프라이즈급 보안, 규정 준수 및 거버넌스

단일 서버 서비스는 미사용 데이터의 스토리지 암호화를 위해 FIPS 140-2 유효성 검사 암호화 모듈을 사용합니다. 백업이 포함된 데이터 및 쿼리를 실행하는 동안 생성된 임시 파일이 암호화됩니다. 이 서비스는 Azure 스토리지 암호화에 포함된 AES 256비트 암호화를 사용하며, 키는 시스템에서 관리(기본값)할 수도 있고 [고객이 관리]()할 수도 있습니다. 서비스는 기본적으로 적용되는 전송 계층 보안(SSL/TLS)을 사용하여 동작 중인 데이터를 암호화합니다. 이 서비스는 [최소 TLS 버전]()을 적용하는 기능을 통해 TLS 버전 1.2, 1.1 및 1.0을 지원합니다.

이 서비스는 프라이빗 링크를 사용하여 서버에 대한 프라이빗 액세스를 허용하고 Advanced Threat Protection 기능을 제공합니다. Advanced Threat Protection은 비정상적이며 잠재적으로 유해한 데이터베이스 액세스 또는 악용 시도를 나타내는 비정상 활동을 탐지합니다.

기본 인증 외에도, 단일 서버 서비스는 Azure Active Directory 인증을 지원합니다. Azure AD 인증은 Azure AD에서 정의되고 관리되는 ID를 사용하여 PostgreSQL 서버에 연결하는 메커니즘입니다. Azure AD 인증을 사용하면 중앙 위치에서 데이터베이스 사용자 ID 및 기타 Azure 서비스를 관리할 수 있으므로, 액세스 제어가 간소화되고 중앙 집중화됩니다.

[감사 로깅]()(미리 보기)은 모든 데이터베이스 수준 활동을 추적하는 데 사용할 수 있습니다.

단일 서버 서비스는 FedRAMP, HIPAA, PCI DSS 등 산업 최고 수준의 모든 인증을 준수합니다. Azure의 플랫폼 보안에 대한 자세한 내용을 보려면 [Azure 보안 센터]()를 방문하세요.

Azure Database for PostgreSQL 보안 기능에 대한 자세한 내용은 [보안 개요]()를 참조하세요.

## <a name="monitoring-and-alerting"></a>모니터링 및 경고

단일 서버 서비스는 기본 제공 성능 모니터링 및 경고 기능을 갖추고 있습니다. 모든 Azure 메트릭의 빈도는 1분이고 각 메트릭은 30일의 기록을 제공합니다. 메트릭에 대한 경고를 구성할 수 있습니다. 이 서비스는 느린 쿼리 로그를 구성할 수 있으며 차별화된 [쿼리 저장소](./concepts-query-store.md) 기능이 기본적으로 제공됩니다. 쿼리 저장소는 가장 오래 실행되고 리소스를 가장 많이 사용하는 쿼리를 신속하게 찾도록 지원하여 성능 문제 해결을 단순화합니다. 이러한 도구를 사용하여 워크로드를 신속하게 최적화하고 최적의 성능을 얻을 수 있도록 서버를 구성할 수 있습니다. 자세한 내용은 [모니터링](./concepts-monitoring.md)을 참조하세요.

## <a name="migration"></a>마이그레이션

이 서비스는 커뮤니티 버전의 PostgreSQL을 실행합니다. 따라서 전체 애플리케이션이 호환되며, PostgreSQL 엔진에서 개발된 기존 애플리케이션을 단일 서버로 마이그레이션하기 위한 리팩터링 비용이 최소화됩니다. 다음 옵션 중 하나를 사용하여 단일 서버로 마이그레이션할 수 있습니다.

- **덤프 및 복원** – 사용자가 약간의 가동 중지 시간을 감당할 수 있는 오프라인 마이그레이션의 경우, Pg_dump 및 Pg_restore 같은 커뮤니티 도구를 사용하여 덤프 및 복원하면 가장 빠른 마이그레이션 방법이 될 수 있습니다. 자세한 내용은 [덤프 및 복원을 사용하여 마이그레이션](./howto-migrate-using-dump-and-restore.md)을 참조하세요.
- **Azure Database Migration Service** – Azure Database Migration Service를 활용하면 가동 중지 시간을 최소화하면서 단일 서버로 원활하고 간단하게 마이그레이션할 수 있습니다. [포털을 통한 DMS](../dms/tutorial-postgresql-azure-postgresql-online-portal.md) 및 [CLI를 통한 DMS](../dms/tutorial-postgresql-azure-postgresql-online.md)를 참조하세요.

## <a name="contacts"></a>연락처

Azure Database for PostgreSQL 작업에 대해 궁금한 점이나 제안하고 싶은 의견이 있으면 Azure Database for PostgreSQL 팀([@Ask Azure DB for PostgreSQL](mailto:AskAzureDBforPostgreSQL@service.microsoft.com))으로 이메일을 보내주세요. 이 이메일 주소는 기술 지원 별칭이 아닙니다.

또한 문의의 다음 사항을 적절히 고려해 주세요.

- Azure 고객 지원팀에 문의하려면 [Azure Portal에서 티켓을 제출](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하세요.
- 계정 관련 문제를 해결하려면 Azure Portal에서 [지원 요청](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)을 제출합니다.
- 피드백을 제공하거나 새 기능을 요청하려면 [UserVoice](https://feedback.azure.com/forums/597976-azure-database-for-postgresql)를 통해 항목을 만드세요.

## <a name="next-steps"></a>다음 단계

Azure Database for PostgreSQL 단일 서버 배포 모드에 대한 소개를 읽어 보았으므로 이제 다음을 할 수 있습니다.
- 첫 번째 서버를 만듭니다.
