---
title: Microsoft Azure Data Box Disk 개요 | Microsoft Docs
description: 많은 양의 데이터를 Azure로 전송할 수 있는 클라우드 솔루션인 Azure Data Box Disk에 대해 설명합니다.
services: databox
author: alkohli
ms.service: databox
ms.subservice: disk
ms.topic: overview
ms.date: 06/18/2019
ms.author: alkohli
Customer intent: As an IT admin, I need to understand what Data Box Disk is and how it works so I can use it to import on-premises data into Azure.
ms.openlocfilehash: ea9353ed8c1938fa9b33585a0650b4507c671451
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92125033"
---
# <a name="what-is-azure-data-box-disk"></a>Azure Data Box Disk란?

Microsoft Azure Data Box Disk 솔루션을 사용하면 테라바이트 단위의 온-프레미스 데이터를 빠르고 저렴하게 신뢰할 수 있는 방식으로 Azure로 보낼 수 있습니다. 1-5개의 SSD(반도체 디스크)를 배송함으로써 안전한 데이터 전송이 빨라집니다. 이러한 8TB 암호화된 디스크는 지역 배송업체를 통해 데이터 센터로 보내집니다.

Azure Portal에서 Data Box 서비스를 통해 디스크를 빠르게 구성, 연결 및 잠금 해제할 수 있습니다. 데이터를 디스크에 복사하고, 이 디스크를 Azure로 반송합니다. Azure 데이터 센터에서 고속 프라이빗망 업로드 링크를 사용하여 데이터를 드라이브에서 클라우드로 자동으로 업로드합니다.

## <a name="use-cases"></a>사용 사례

네트워크 연결이 제한되지 않는 시나리오에서 Data Box Disk를 사용하여 TB 단위의 데이터를 전송합니다. 데이터 이동은 일회성 전송, 정기적 전송 또는 초기 대량 데이터 전송 후의 정기적 전송일 수 있습니다.

- **일회성 마이그레이션** - 대량의 온-프레미스 데이터를 Azure로 이동하는 경우입니다. 예를 들어 Azure 쿨 스토리지에서 오프라인 테이프의 데이터를 보관 데이터로 이동합니다.
- **증분 전송** - Data Box Disk(초기값)를 사용하여 초기 대량 전송을 수행한 후에 네트워크를 통해 증분 전송이 수행되는 경우입니다. 예를 들어 Commvault 및 Data Box Disk를 사용하여 백업 복사본을 Azure로 이동합니다. 이 마이그레이션 후에 네트워크를 통해 증분 데이터를 Azure Storage에 복사합니다.
- **정기적 업로드** - 대량의 데이터를 정기적으로 생성하고 Azure로 이동해야 하는 경우입니다. 예를 들어 에너지를 탐사할 때 석유 굴착 장치와 풍력 발전 시설에서 비디오 콘텐츠를 생성하는 경우가 있습니다.

### <a name="ingestion-of-data-from-data-box"></a>Data Box의 데이터 수집

Azure 공급자 및 비 Azure 공급자는 Azure Data Box에서 데이터를 수집할 수 있습니다. Azure Data Box에서 데이터를 수집하는 Azure 서비스는 다음과 같습니다.

- **SharePoint Online** - Azure Data Box 및 SPMT(SharePoint Migration Tool)를 사용하여 파일 공유 콘텐츠를 SharePoint Online에 마이그레이션합니다. Data Box를 사용하면 WAN 링크에 대한 종속성을 제거하고 데이터를 전송할 수 있습니다. 자세한 정보는 [Azure Data Box Heavy를 사용하여 파일 공유 콘텐츠를 SharePoint Online으로 마이그레이션](data-box-heavy-migrate-spo.md)을 참조하세요.

- **Azure 파일 동기화** - 데이터에 대한 로컬 액세스는 유지하면서 Azure에 파일 서비스를 집중할 수 있도록 Data Box에서 Azure 파일 공유로 파일을 복제합니다. 자세한 정보는 [Azure 파일 동기화 배포](../storage/files/storage-sync-files-deployment-guide.md)를 참조하세요.

- **HDFS 저장소** - Data Box를 사용하여 Hadoop 클러스터의 온-프레미스 HDFS(Hadoop Distributed File System) 저장소 데이터를 Azure Storage에 마이그레이션합니다. 자세한 정보는 [Azure Data Box를 사용하여 온-프레미스 HDFS 저장소를 Azure Storage로 마이그레이션](../storage/blobs/data-lake-storage-migrate-on-premises-hdfs-cluster.md)을 참조하세요.

- **Azure Backup** - 오프라인 메커니즘을 통해 대규모 중요 엔터프라이즈 데이터의 백업을 Azure Recovery Services 자격 증명 모음으로 이동할 수 있습니다. 자세한 정보는 [Azure Backup 개요](../backup/backup-overview.md)를 참조하세요.

여러 비 Azure 서비스 공급자에서 Data Box 데이터를 사용할 수 있습니다. 예:

- **[Commvault](http://documentation.commvault.com/commvault/v11/article?p=97276.htm)** - Azure Data Box를 사용 하여 대용량 데이터를 Microsoft Azure로 마이그레이션할 수 있습니다.
- **[Veeam](https://helpcenter.veeam.com/docs/backup/hyperv/osr_adding_data_box.html?ver=100)** - Hyper-v 머신의 대용량 데이터를 Data Box로 백업 및 복제할 수 있습니다.

Data Box와 통합되는 다른 비 Azure 서비스 공급자 목록은 [Azure Data Box 파트너](https://cloudchampions.blob.core.windows.net/db-partners/PartnersTable.pdf)를 참조하세요.

## <a name="the-workflow"></a>워크플로

일반적인 흐름에 포함되는 단계는 다음과 같습니다.

1. **주문** - Azure Portal에서 주문을 만들고, 배송 정보를 제공하고, 데이터에 대한 대상 Azure Storage 계정을 만듭니다. 디스크를 사용할 수 있는 경우 Azure에서 배송 추적 ID를 사용하여 디스크를 암호화, 준비 및 배송합니다.

2. **수취** - 디스크가 전달되면 압축을 풀고 복사할 데이터가 있는 컴퓨터에 디스크를 연결합니다. 디스크의 잠금을 해제합니다.

3. **데이터 복사** - 끌어서 놓기를 통해 데이터를 디스크에 복사합니다.

4. **반송** - 디스크를 준비하고 Azure 데이터 센터로 반송합니다.

5. **업로드** - 데이터를 자동으로 디스크에서 Azure로 복사합니다. 디스크는 NIST(National Institute of Standard and Technology) 지침에 따라 안전하게 지워집니다.

이 과정에서 모든 상태 변경에 대해 이메일로 알림을 받습니다. 세부적인 흐름에 대한 자세한 내용은 [Azure Portal에서 Data Box Disk 배포](data-box-disk-quickstart-portal.md)를 참조하세요.

## <a name="benefits"></a>이점

Data Box Disk는 네트워크에 아무런 영향을 주지 않고 대량의 데이터를 Azure로 이동할 수 있도록 설계되었습니다. 이 솔루션에는 다음과 같은 이점이 있습니다.

- **속도** - Data Box Disk는 USB 3.0 연결을 사용하여 1주 이내에 최대 35TB의 데이터를 Azure로 이동할 수 있습니다.

- **사용 용이성** - Data Box는 사용하기 쉬운 솔루션입니다.

  - 디스크에는 거의 설정할 필요가 없는 USB 연결이 사용됩니다.
  - 디스크에는 쉽게 다룰 수 있는 작은 폼 팩터가 있습니다.
  - 디스크에는 외부 전원 요구 사항이 없습니다.
  - 디스크는 데이터 센터 서버, 데스크톱 또는 랩톱에서 사용할 수 있습니다.
  - 솔루션에서 Azure Portal을 통해 엔드투엔드 추적을 제공합니다.

- **보안** - Data Box Disk에는 디스크, 데이터 및 서비스에 대한 보안 보호 기능이 기본적으로 제공됩니다.
  - 디스크는 변조 방지 및 보안 업데이트 기능을 지원합니다.
  - 디스크의 데이터는 항상 AES 128비트 암호화로 보호됩니다.
  - 디스크는 Azure Portal에 제공된 키로만 잠금 해제할 수 있습니다.
  - 서비스는 Azure 보안 기능으로 보호됩니다.
  - 데이터가 Azure에 업로드되면 디스크는 NIST 800-88r1 표준에 따라 완전히 초기화됩니다.  

자세한 내용은 [Azure Data Box Disk 보안 및 데이터 보호](data-box-disk-security.md)를 참조하세요.

## <a name="features-and-specifications"></a>기능 및 사양

| 사양                                          | Description              |
|---------------------------------------------------------|--------------------------|
| 무게                                                  | Box당 2lb 미만, Box에 최대 5개 디스크                |
| 차원                                              | 디스크 - 2.5" SSD |
| 케이블                                                  | 디스크당 1개 USB 3.1 케이블|
| 주문당 스토리지 용량                              | 40TB(35TB까지 사용 가능)|
| 디스크 스토리지 용량                                   | 8TB(7TB까지 사용 가능)|
| 데이터 인터페이스                                          | USB   |
| 보안                                                | BitLocker 및 보안 업데이트를 사용하여 미리 암호화, <br> 지원 암호로 보호된 디스크, <br> 항상 암호화된 데이터  |
| 데이터 전송 속도                                      | 파일 크기에 따라 최대 430Mbps      |
|관리                                               | Azure portal |

## <a name="region-availability"></a>지역 가용성

지역 가용성에 대한 정보는 [지역별 사용 가능한 Azure 제품](https://azure.microsoft.com/global-infrastructure/services/?products=databox&regions=all)으로 이동하세요. Data Box Disk는 Azure Government 클라우드에도 배포할 수 있습니다. 자세한 내용은 [Azure Government란?](../azure-government/documentation-government-welcome.md)을 참조하세요.

## <a name="pricing"></a>가격 책정

가격 책정에 대한 자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/databox/disk/)를 참조하세요.

## <a name="next-steps"></a>다음 단계

- [Data Box Disk 요구 사항](data-box-disk-system-requirements.md)을 검토합니다.
- [Data Box Disk 제한](data-box-disk-limits.md)을 알아봅니다.
- Azure Portal에서 [Azure Data Box Disk](data-box-disk-quickstart-portal.md)를 빠르게 배포합니다.