---
title: '자습서: MongoDB를 Azure Cosmos DB API for MongoDB로 오프라인 마이그레이션'
titleSuffix: Azure Database Migration Service
description: Azure Database Migration Service를 사용하여 오프라인으로 MongoDB 온-프레미스에서 Azure Cosmos DB API for MongoDB로 마이그레이션하는 방법에 대해 알아봅니다.
services: dms
author: pochiraju
ms.author: rajpo
manager: craigg
ms.reviewer: craigg
ms.service: dms
ms.workload: data-services
ms.custom: seo-lt-2019
ms.topic: tutorial
ms.date: 02/03/2021
ms.openlocfilehash: b669870537ffb58d9ae7e8a5c65276d310ba6a7e
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "101722027"
---
# <a name="tutorial-migrate-mongodb-to-azure-cosmos-dbs-api-for-mongodb-offline-using-dms"></a>자습서: DMS를 사용하여 오프라인에서 MongoDB를 Azure Cosmos DB의 API for MongoDB로 마이그레이션

Azure Database Migration Service를 사용하여 오프라인(1회)으로 데이터베이스를 MongoDB 온-프레미스 또는 클라우드 인스턴스에서 Azure Cosmos DB의 API for MongoDB로 마이그레이션할 수 있습니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.
> [!div class="checklist"]
>
> * Azure Database Migration Service 인스턴스를 만듭니다.
> * Azure Database Migration Service를 사용하여 마이그레이션 프로젝트를 만듭니다.
> * 마이그레이션을 실행합니다.
> * 마이그레이션을 모니터링합니다.

이 자습서에서는 Azure Database Migration Service를 사용하여 Azure Virtual Machine에서 호스트되는 MongoDB의 데이터 세트를 Azure Cosmos DB의 API for MongoDB로 마이그레이션합니다. MongoDB 원본을 설정하지 않은 경우 [Azure의 Windows VM에서 MongoDB 설치 및 구성](/previous-versions/azure/virtual-machines/windows/install-mongodb) 문서를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 다음이 필요합니다.

* 처리량 추정, 파티션 키 선택 및 인덱싱 정책과 같은 [사전 마이그레이션 완료](../cosmos-db/mongodb-pre-migration.md) 단계.
* [Azure Cosmos DB의 API for MongoDB 계정을 만듭니다](https://ms.portal.azure.com/#create/Microsoft.DocumentDB).
* Azure Resource Manager 배포 모델을 사용하여 Azure Database Migration Service용 Microsoft Azure Virtual Network를 만듭니다. 그러면 [ExpressRoute](../expressroute/expressroute-introduction.md) 또는 [VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)을 사용하여 온-프레미스 원본 서버에 사이트 간 연결이 제공됩니다. 가상 네트워크를 만드는 방법에 대한 자세한 내용은 [Virtual Network 설명서](../virtual-network/index.yml)를 참조하세요. 특히 단계별 세부 정보를 제공하는 빠른 시작 문서를 참조하세요.

    > [!NOTE]
    > 가상 네트워크 설정 중에 Microsoft에 대한 네트워크 피어링에서 ExpressRoute를 사용하는 경우 서비스가 프로비저닝되는 서브넷에 다음 서비스 [엔드포인트](../virtual-network/virtual-network-service-endpoints-overview.md)를 추가합니다.
    >
    > * 대상 데이터베이스 엔드포인트(예: SQL 엔드포인트, Cosmos DB 엔드포인트 등)
    > * 스토리지 엔드포인트
    > * Service Bus 엔드포인트
    >
    > Azure Database Migration Service에는 인터넷 연결이 없으므로 이 구성이 필요합니다.

* 가상 네트워크 NSG(네트워크 보안 그룹) 규칙이 53, 443, 445, 9354 및 10000-20000 통신 포트를 차단하지 않는지 확인합니다. 가상 네트워크 NSG 트래픽 필터링에 대한 자세한 내용은 [네트워크 보안 그룹을 사용하여 네트워크 트래픽 필터링](../virtual-network/virtual-network-vnet-plan-design-arm.md) 문서를 참조하세요.
* Azure Database Migration Service에서 기본적으로 27017 TCP 포트인 원본 MongoDB 서버에 액세스할 수 있도록 Windows 방화벽을 엽니다.
* 원본 데이터베이스 앞에 방화벽 어플라이언스를 사용하는 경우 Azure Database Migration Service에서 원본 데이터베이스에 액세스하여 마이그레이션할 수 있도록 허용하는 방화벽 규칙을 추가해야 합니다.

## <a name="configure-azure-cosmos-db-server-side-retries-for-efficient-migration"></a>효율적인 마이그레이션을 위해 Azure Cosmos DB 서버 쪽 다시 시도 구성

MongoDB에서 Azure Cosmos DB로 마이그레이션하는 고객은 프로비저닝된 RU/s의 처리량을 완전히 활용할 수 있는 능력을 보장하는 리소스 거버넌스 기능의 혜택을 받습니다. Azure Cosmos DB는 해당 요청이 컨테이너 프로비저닝된 RU/s를 초과하는 경우 마이그레이션 과정에서 지정된 Data Migration Service 요청을 제한할 수 있습니다. 그런 다음, 해당 요청을 다시 시도해야 합니다. Data Migration Service는 다시 시도를 수행할 수 있지만 데이터 마이그레이션 서비스와 Azure Cosmos DB 간의 네트워크 홉과 관련된 왕복 시간은 해당 요청의 전체 응답 시간에 영향을 줍니다. 제한된 요청에 대한 응답 시간을 개선하면 마이그레이션에 필요한 총 시간을 단축할 수 있습니다. Azure Cosmos DB의 *서버 측 다시 시도* 기능을 통해 서비스는 스로틀 오류 코드를 가로채고 훨씬 낮은 왕복 시간으로 다시 시도할 수 있으므로 요청 응답 시간이 크게 단축됩니다.

Azure Cosmos DB 포털의 *기능* 블레이드에서 서버 쪽 다시 시도 기능을 찾을 수 있습니다.

![MongoDB SSR 기능](media/tutorial-mongodb-to-cosmosdb/mongo-server-side-retry-feature.png)

*사용 안 함* 인 경우 아래와 같이 사용하도록 설정하는 것이 좋습니다.

![MongoDB SSR 사용](media/tutorial-mongodb-to-cosmosdb/mongo-server-side-retry-enable.png)

## <a name="register-the-microsoftdatamigration-resource-provider"></a>Microsoft.DataMigration 리소스 공급자 등록

1. Azure Portal에 로그인하고, **모든 서비스** 를 선택한 다음, **구독** 을 선택합니다.

   ![포털 구독 표시](media/tutorial-mongodb-to-cosmosdb/portal-select-subscription1.png)

2. Azure Database Migration Service의 인스턴스를 만들 구독을 선택한 다음 **리소스 공급자** 를 선택합니다.

    ![리소스 공급자 보기](media/tutorial-mongodb-to-cosmosdb/portal-select-resource-provider.png)

3. 마이그레이션을 검색한 다음 **Microsoft.DataMigration** 의 오른쪽에서 **등록** 을 선택합니다.

    ![리소스 공급자 등록](media/tutorial-mongodb-to-cosmosdb/portal-register-resource-provider.png)    

## <a name="create-an-instance"></a>인스턴스 만들기

1. Azure Portal에서 **+ 리소스 만들기** 를 선택하고, Azure Database Migration Service를 검색한 다음, 드롭다운 목록에서 **Azure Database Migration Service** 를 선택합니다.

    ![Azure Marketplace](media/tutorial-mongodb-to-cosmosdb/portal-marketplace.png)

2. **Azure Database Migration Service** 화면에서 **만들기** 를 선택합니다.

    ![Azure Database Migration Service 인스턴스 만들기](media/tutorial-mongodb-to-cosmosdb/dms-create1.png)
  
3. **Migration Service 만들기** 화면에서 서비스, 구독, 신규 또는 기존 리소스 그룹의 이름을 지정합니다.

4. Azure Database Migration Service 인스턴스를 만들 위치를 선택합니다. 

5. 기존 가상 네트워크를 선택하거나 새로 만듭니다.

    가상 네트워크는 원본 MongoDB 인스턴스 및 대상 Azure Cosmos DB 계정에 대한 액세스 권한이 있는 Azure Database Migration Service를 제공합니다.

    Azure Portal에서 가상 네트워크를 만드는 방법에 대한 자세한 내용은 [Azure Portal을 사용하여 가상 네트워크 만들기](../virtual-network/quick-create-portal.md) 문서를 참조하세요.

6. 가격 책정 계층을 선택합니다.

    비용 및 가격 책정 계층에 대한 자세한 내용은 [가격 책정 페이지](https://aka.ms/dms-pricing)를 참조하세요.

    ![Azure Database Migration Service 인스턴스 설정 구성](media/tutorial-mongodb-to-cosmosdb/dms-settings2.png)

7. **만들기** 를 선택하여 서비스를 만듭니다.

## <a name="create-a-migration-project"></a>마이그레이션 프로젝트 만들기

서비스가 생성된 후 Azure Portal에서 서비스를 찾아 연 다음, 새로운 마이그레이션 프로젝트를 만듭니다.

1. Azure Portal에서 **모든 서비스** 를 선택하고, Azure Database Migration Service를 검색하고 나서, **Azure Database Migration Services** 를 선택합니다.

      ![Azure Database Migration Service의 모든 인스턴스 찾기](media/tutorial-mongodb-to-cosmosdb/dms-search.png)

2. **Azure Database Migration Services** 화면에서 방금 만든 Azure Database Migration Service 인스턴스의 이름을 검색한 다음, 인스턴스를 선택합니다.

3. **+ 새 마이그레이션 프로젝트** 를 선택합니다.

4. **새 마이그레이션 프로젝트** 화면에서 프로젝트의 이름을 지정하고, **원본 서버 형식** 텍스트 상자에서 **MongoDB** 를 선택하고, **대상 서버 형식** 텍스트 상자에서 **CosmosDB(MongoDB API)** 를 선택한 다음, **작업 형식 선택** 에서 **오프라인 데이터 마이그레이션** 을 선택합니다. 

    ![Database Migration Service 프로젝트 만들기](media/tutorial-mongodb-to-cosmosdb/dms-create-project.png)

5. **작업 만들기 및 실행** 을 선택하여 프로젝트를 만들고 마이그레이션 작업을 실행합니다.

## <a name="specify-source-details"></a>원본 세부 정보 지정

1. **원본 세부 정보** 화면에서 원본 MongoDB 서버에 대한 연결 세부 정보를 지정합니다.

   > [!IMPORTANT]
   > Azure Database Migration Service는 Azure Cosmos DB를 원본으로 지원하지 않습니다.

    원본에 연결하는 세 가지 모드가 있습니다.
   * **표준 모드** - 정규화된 도메인 이름이나 IP 주소, 포트 번호 및 연결 자격 증명을 수락합니다.
   * **연결 문자열 모드** - [연결 문자열 URI 형식](https://docs.mongodb.com/manual/reference/connection-string/) 문서에서 설명한 대로 MongoDB 연결 문자열을 수락합니다.
   * **Azure Storage의 데이터** - Blob 컨테이너 SAS URL을 수락합니다. MongoDB [bsondump 도구](https://docs.mongodb.com/manual/reference/program/bsondump/)에서 생성된 BSON 덤프가 Blob 컨테이너에 있는 경우 **Blob이 BSON 덤프를 포함합니다** 를 선택하고, JSON 파일이 컨테이너에 있으면 이를 선택 취소합니다.

     이 옵션을 선택할 경우 해당 스토리지 계정 연결 문자열이 다음 형식으로 나타나는지 확인하세요.

     ```
     https://blobnameurl/container?SASKEY
     ```

     이 Blob 컨테이너 SAS 연결 문자열은 Azure Storage Explorer에서 찾을 수 있습니다. 관련 컨테이너의 SAS를 만들면 위에서 요청한 형식으로 URL이 제공됩니다.
     
     또한 Azure Storage의 형식 덤프 정보에 기반하여 다음 세부 정보를 유념해 두세요.

     * BSON 덤프의 경우 Blob 컨테이너 내 데이터는 데이터 파일이 collection.bson 형식의 포함한 데이터베이스를 따라 이름이 지정된 폴더에 배치되는 bsondump 형식이어야 합니다. 메타데이터 파일(있는 경우)의 이름은 *collection*.metadata.json 형식을 사용하여 이름이 지정되어야 합니다.

     * JSON 덤프의 경우 Blob 컨테이너의 파일은 포함한 데이터베이스를 따라 이름이 지정된 폴더에 배치되어야 합니다. 각 데이터베이스 폴더 내에서 데이터 파일은 "data"라고 하는 하위 폴더에 배치되고 *collection*.json 형식을 사용하여 이름이 지정되어야 합니다. 메타데이터 파일(있는 경우)은 "metadata"라고 하는 하위 폴더에 배치되고 *collection*.json과 동일한 형식을 사용하여 이름이 지정되어야 합니다. 메타데이터 파일은 MongoDB bsondump 도구에서 생성한 것과 동일한 형식이어야 합니다.

    > [!IMPORTANT]
    > mongo 서버에서 자체 서명된 인증서를 사용하는 것은 바람직하지 않습니다. 그러나 하나를 사용할 경우 **연결 문자열 모드** 를 사용하여 서버에 연결하고 연결 문자열에 “”가 있는지 확인합니다.
    >
    >```
    >&sslVerifyCertificate=false
    >```

   또한 DNS 이름을 확인할 수 없는 경우에는 IP 주소를 사용할 수도 있습니다.

   ![원본 세부 정보 지정](media/tutorial-mongodb-to-cosmosdb/dms-specify-source.png)

2. **저장** 을 선택합니다.

## <a name="specify-target-details"></a>대상 세부 정보 지정

1. **마이그레이션 대상 세부 정보** 화면에서 대상 Azure Cosmos DB 계정에 대한 연결 세부 정보를 지정합니다. 이 계정은 MongoDB 데이터를 마이그레이션할 미리 프로비전된 Azure Cosmos DB의 API for MongoDB 계정입니다.

    ![대상 세부 정보 지정](media/tutorial-mongodb-to-cosmosdb/dms-specify-target.png)

2. **저장** 을 선택합니다.

## <a name="map-to-target-databases"></a>대상 데이터베이스에 매핑

1. **대상 데이터베이스에 매핑** 화면에서 마이그레이션하기 위해 원본 및 대상 데이터베이스를 매핑합니다.

    대상 데이터베이스의 이름이 원본 데이터베이스와 동일하면 Azure Database Migration Service는 기본적으로 이 대상 데이터베이스를 선택합니다.

    **만들기** 문자열이 데이터베이스 이름 옆에 나타나는 경우 Azure Database Migration Service가 대상 데이터베이스를 찾을 수 없으므로 해당 서비스가 데이터베이스를 만든다는 것을 나타냅니다.

    마이그레이션의 이 시점에서 [처리량을 프로비전](../cosmos-db/set-throughput.md)할 수 있습니다. Cosmos DB에서 데이터베이스 수준에서 또는 컬렉션 수준에서 개별적으로 처리량을 프로비전할 수 있습니다. 처리량은 RU([요청 단위](../cosmos-db/request-units.md))로 측정됩니다. [Azure Cosmos DB 가격 책정](https://azure.microsoft.com/pricing/details/cosmos-db/)에 대해 자세히 알아봅니다.

    ![대상 데이터베이스에 매핑](media/tutorial-mongodb-to-cosmosdb/dms-map-target-databases.png)

2. **저장** 을 선택합니다.
3. **컬렉션 설정** 화면에서 컬렉션 목록을 확장한 다음, 마이그레이션할 컬렉션 목록을 검토합니다.

    Azure Database Migration Service는 대상 Azure Cosmos DB 계정에 존재하지 않는 원본 MongoDB 인스턴스에 존재하는 모든 컬렉션을 자동으로 선택합니다. 이미 데이터를 포함하는 컬렉션을 다시 마이그레이션하려면 이 블레이드에서 컬렉션을 명시적으로 선택해야 합니다.

    컬렉션에서 사용할 RU의 수량을 지정할 수 있습니다. Azure Database Migration Service는 컬렉션 크기에 따라 스마트 기본값을 제공합니다.

    > [!NOTE]
    > 필요에 따라 Azure Database Migration Service 인스턴스를 여러 개 사용하여 데이터베이스 마이그레이션 및 컬렉션을 병렬로 수행하여 속도를 높일 수 있습니다.

    확장성을 최적화하기 위해 [Azure Cosmos DB에서 분할](../cosmos-db/partitioning-overview.md)을 활용하도록 분할된 데이터베이스 키를 지정할 수도 있습니다. [분할된 데이터베이스/파티션 키를 선택하는 모범 사례](../cosmos-db/partitioning-overview.md#choose-partitionkey)를 검토해야 합니다.

    ![컬렉션 선택 테이블](media/tutorial-mongodb-to-cosmosdb/dms-collection-setting.png)

4. **저장** 을 선택합니다.

5. **마이그레이션 요약** 화면의 **작업 이름** 텍스트 상자에서 마이그레이션 작업의 이름을 지정합니다.

    ![마이그레이션 요약](media/tutorial-mongodb-to-cosmosdb/dms-migration-summary.png)

## <a name="run-the-migration"></a>마이그레이션 실행

* **마이그레이션 실행** 을 선택합니다.

    마이그레이션 작업 창이 나타나고, 작업 **상태** 는 **시작되지 않음** 입니다.

    ![작업 상태](media/tutorial-mongodb-to-cosmosdb/dms-activity-status.png)

## <a name="monitor-the-migration"></a>마이그레이션 모니터링

* 마이그레이션 작업 화면에서 **새로 고침** 을 선택하여 마이그레이션 **상태** 가 **완료됨** 으로 표시될 때까지 디스플레이를 업데이트합니다.

   > [!NOTE]
   > 데이터베이스 및 컬렉션 수준 마이그레이션 메트릭의 세부 정보를 가져오는 작업을 선택할 수 있습니다.

    ![작업 상태 완료됨](media/tutorial-mongodb-to-cosmosdb/dms-activity-completed.png)

## <a name="verify-data-in-cosmos-db"></a>Cosmos DB에서 데이터 확인

* 마이그레이션이 완료되면 Azure Cosmos DB 계정을 검사하여 모든 컬렉션이 성공적으로 마이그레이션되었는지 확인할 수 있습니다.

    ![Azure Cosmos DB 계정을 검사하여 모든 컬렉션이 성공적으로 마이그레이션되었는지 확인할 수 있는 위치를 보여 주는 스크린샷](media/tutorial-mongodb-to-cosmosdb/dms-cosmosdb-data-explorer.png)

## <a name="post-migration-optimization"></a>마이그레이션 후 최적화

MongoDB 데이터베이스에 저장된 데이터를 MongoDB용 Azure Cosmos DB의 API로 마이그레이션한 후 Azure Cosmos DB에 연결하고 데이터를 관리할 수 있습니다. 인덱싱 정책 최적화와 같은 다른 마이그레이션 후 최적화 단계를 수행하거나, 기본 일관성 수준을 업데이트하거나, Azure Cosmos DB 계정에 대한 글로벌 배포를 구성할 수도 있습니다. 자세한 내용은 [마이그레이션 후 최적화](../cosmos-db/mongodb-post-migration.md) 문서를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

* [Cosmos DB 서비스 정보](https://azure.microsoft.com/services/cosmos-db/)

## <a name="next-steps"></a>다음 단계

* Microsoft [데이터베이스 마이그레이션 가이드](https://datamigration.microsoft.com/)에서 추가 시나리오에 대한 마이그레이션 지침을 검토합니다.