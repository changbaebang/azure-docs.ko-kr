---
author: linda33wj
ms.service: data-factory
ms.topic: include
ms.date: 11/09/2018
ms.author: jingwang
ms.openlocfilehash: 19927fd274cbb7337248fb2ae8cf9d882612d570
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92369245"
---
Azure Data Factory는 개별적 또는 다른 작업과 연계하여 파이프라인에 추가할 수 있는 다음과 같은 변환 작업을 지원합니다.

| 데이터 변환 작업 | 컴퓨팅 환경 |
|:--- |:--- |
| [Hive](../articles/data-factory/v1/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/v1/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/v1/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop 스트리밍](../articles/data-factory/v1/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/v1/data-factory-spark.md) | HDInsight [Hadoop] |
| [Azure Machine Learning Studio(클래식) 작업: 일괄 처리 실행 및 리소스 업데이트](../articles/data-factory/v1/data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [저장 프로시저](../articles/data-factory/v1/data-factory-stored-proc-activity.md) |Azure SQL, Azure Synapse Analytics 또는 SQL Server |
| [데이터 레이크 분석 U-SQL](../articles/data-factory/v1/data-factory-usql-activity.md) |Azure 데이터 레이크 분석 |
| [DotNet](../articles/data-factory/v1/data-factory-use-custom-activities.md) |HDInsight [Hadoop] 또는 Azure Batch |

> [!NOTE]
> MapReduce 작업을 사용하여 HDInsight Spark 클러스터에서 Spark 프로그램을 실행할 수 있습니다. 자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](../articles/data-factory/v1/data-factory-spark.md) 을 참조하세요.
> R이 설치된 HDInsight 클러스터에서 R 스크립트를 실행하는 사용자 지정 작업을 만들 수 있습니다. [Azure Data Factory를 사용하여 R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/SamplesV1/RunRScriptUsingADFSample)을 참조하세요.
> 
> 

