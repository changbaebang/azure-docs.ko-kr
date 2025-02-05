---
title: '자습서: 포털의 지역 복제 및 장애 조치(Failover)'
description: Azure Portal을 사용하여 데이터베이스에 대한 지역에서 복제 구성 및 장애 조치(failover)를 시작합니다.
services: sql-database
ms.service: sql-database
ms.subservice: high-availability
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: tutorial
author: anosov1960
ms.author: sashan
ms.reviewer: mathoma, sstein
ms.date: 02/13/2019
ms.openlocfilehash: 71c73fec4f559b34b097556243617636acd77480
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92673277"
---
# <a name="tutorial-configure-active-geo-replication-and-failover-in-the-azure-portal-azure-sql-database"></a>자습서: Azure Portal에서 활성 지역 복제 및 장애 조치(failover) 구성(Azure SQL Database)

[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

이 문서에서는 [Azure Portal](https://portal.azure.com)을 사용하여 [Azure SQL Database에 대한 활성 지역 복제](active-geo-replication-overview.md#active-geo-replication-terminology-and-capabilities)를 구성하고 장애 조치(Failover)를 시작하는 방법을 보여 줍니다.

자동 장애 조치(Failover) 그룹을 사용하는 모범 사례는 [Azure SQL Database에 대한 모범 사례](auto-failover-group-overview.md#best-practices-for-sql-database) 및 [Azure SQL Managed Instance에 대한 모범 사례](auto-failover-group-overview.md#best-practices-for-sql-managed-instance)를 참조하세요. 



## <a name="prerequisites"></a>필수 요건

Azure Portal을 사용하여 활성 지역 복제를 구성하려면 다음 리소스가 필요합니다.

* Azure SQL Database의 데이터베이스: 다른 지역으로 복제하려는 주 데이터베이스입니다.

> [!Note]
> Azure Portal을 사용하는 경우 기본 데이터베이스와 동일한 구독 내에서만 보조 데이터베이스를 만들 수 있습니다. 보조 데이터베이스가 다른 구독에 있어야 하는 경우 [데이터베이스 만들기 REST API](/rest/api/sql/databases/createorupdate) 또는 [ALTER DATABASE Transact-SQL API](/sql/t-sql/statements/alter-database-transact-sql)를 사용하세요.

## <a name="add-a-secondary-database"></a>보조 데이터베이스 추가

다음 단계에서는 지역에서 복제 파트너 관계에 새 보조 데이터베이스를 만듭니다.  

보조 데이터베이스를 추가하려면 구독 소유자 또는 공동 소유자여야 합니다.

보조 데이터베이스는 주 데이터베이스와 이름이 같고, 기본적으로 서비스 계층과 컴퓨팅 크기가 동일합니다. 보조 데이터베이스는 단일 데이터베이스 또는 풀링된 데이터베이스가 될 수 있습니다. 자세한 내용은 [DTU 기반 구매 모델](service-tiers-dtu.md) 및 [vCore 기반 구매 모델](service-tiers-vcore.md)을 참조하세요.
보조가 만들어지고 시드된 후 데이터는 주 데이터베이스에서 새로운 보조 데이터베이스로 복제되기 시작합니다.

> [!NOTE]
> 파트너 데이터베이스가 이미 있는 경우(예: 이전 지역에서 복제 관계를 종료한 결과) 명령이 실패합니다.

1. [Azure Portal](https://portal.azure.com)에서 지역에서 복제를 위해 설치하려는 데이터베이스를 찾습니다.
2. SQL Database 페이지에서 **지역에서 복제** 를 선택하고 보조 데이터베이스를 만들 지역을 선택합니다. 주 데이터베이스를 호스트하는 지역과 다른 지역을 선택할 수 있지만 [쌍을 이루는 지역](../../best-practices-availability-paired-regions.md)이 권장됩니다.

    ![지역에서 복제 구성](./media/active-geo-replication-configure-portal/configure-geo-replication.png)
3. 보조 데이터베이스를 위한 서버 및 가격 책정 계층을 선택하거나 구성합니다.

    ![보조 양식 만들기](./media/active-geo-replication-configure-portal/create-secondary.png)
4. 필요에 따라 탄력적 풀에 보조 데이터베이스를 추가할 수 있습니다. 풀에서 보조 데이터베이스를 만들려면 **탄력적 풀** 을 클릭하고 대상 서버에서 풀을 선택합니다. 대상 서버에 풀이 이미 있어야 합니다. 이 워크플로는 풀을 만들지 않습니다.
5. **만들기** 를 클릭하여 보조를 추가합니다.
6. 보조 데이터베이스가 만들어지고 시드 프로세스가 시작됩니다.

    ![보조 맵](./media/active-geo-replication-configure-portal/seeding0.png)
7. 시드 프로세스가 완료되면 보조 데이터베이스가 해당 상태를 표시합니다.

    ![시드 완료](./media/active-geo-replication-configure-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>장애 조치(failover) 시작

보조 데이터베이스가 주 데이터베이스가 되도록 전환할 수 있습니다.  

1. [Azure Portal](https://portal.azure.com)에서 지역에서 복제 파트너 관계에 있는 주 데이터베이스를 찾습니다.
2. SQL Database 블레이드에서 **모든 설정** > **지역에서 복제** 를 선택합니다.
3. **보조** 목록에서 새로운 주 데이터베이스가 될 데이터베이스를 선택하고 **강제 장애 조치(failover)** 를 클릭합니다.

    ![failover](./media/active-geo-replication-configure-portal/secondaries.png)
4. 장애 조치를 시작하려면 **예** 를 클릭합니다.

이 명령은 보조 데이터베이스를 주 역할로 즉시 전환합니다. 이 프로세스는 일반적으로 30초 이내에 완료되어야 합니다.

역할이 전환되는 동안 두 데이터베이스를 모두 사용할 수 없는 (0-25초의 순서로) 짧은 기간이 있습니다. 주 데이터베이스에 여러 개의 보조 데이터베이스가 있는 경우 이 명령을 사용하면 새로운 주 데이터베이스에 연결할 다른 보조 데이터베이스가 자동으로 다시 구성됩니다. 전체 작업은 정상적인 상황에서 완료하는데 1분 미만이 걸려야 합니다.

> [!NOTE]
> 이 명령은 가동 중지 시에 데이터베이스의 빠른 복구를 위해 설계되었습니다. 데이터 동기화 없이 장애 조치(Failover)를 트리거합니다(강제 장애 조치).  주 데이터베이스가 온라인이고 명령이 실행될 때 트랜잭션을 커밋하면 일부 데이터가 손실될 수 있습니다.

## <a name="remove-secondary-database"></a>보조 데이터베이스 제거

이 작업은 보조 데이터베이스에 대한 복제를 영구적으로 종료하고 보조의 역할을 일반적인 읽기-쓰기 데이터베이스로 변경합니다. 보조 데이터베이스에 대한 연결이 끊어진 경우 명령이 성공하지만 연결이 복원된 후에야 보조는 읽기-쓰기가 됩니다.  

1. [Azure Portal](https://portal.azure.com)에서 지역에서 복제 파트너 관계에 있는 주 데이터베이스를 찾습니다.
2. SQL Database 페이지에서 **지역에서 복제** 를 선택합니다.
3. **보조** 목록에서 지역에서 복제 파트너 관계에서 제거할 데이터베이스를 선택합니다.
4. **복제 중지** 를 클릭합니다.

    ![보조 제거](./media/active-geo-replication-configure-portal/remove-secondary.png)
5. 확인 창이 열립니다. 지역에서 복제 파트너 관계에서 데이터베이스를 제거하려면 **예** 를 클릭합니다. (복제에 포함되지 않는 읽기-쓰기 데이터베이스로 설정)

## <a name="next-steps"></a>다음 단계

* 활성 지역 복제에 대한 자세한 내용은 [활성 지역 복제](active-geo-replication-overview.md)를 참조하세요.
* 자동 장애 조치(failover) 그룹에 대해 알아보려면 [자동 장애 조치(failover) 그룹](auto-failover-group-overview.md)을 참조하세요.
* 비즈니스 연속성의 개요 및 시나리오를 보려면 [비즈니스 연속성 개요](business-continuity-high-availability-disaster-recover-hadr-overview.md)를 참조하세요.