---
title: Azure HDInsight의 ML 서비스 소개
description: HDInsight의 ML Services를 사용하여 빅 데이터 분석용 애플리케이션을 만드는 방법에 대해 알아봅니다.
ms.service: hdinsight
ms.topic: overview
ms.custom: hdinsightactive,seoapr2020
ms.date: 04/20/2020
ms.openlocfilehash: 87f4181e820b1c6ecdeb0fda85a88e80db248dd2
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98943923"
---
# <a name="what-is-ml-services-in-azure-hdinsight"></a>Azure HDInsight에서 ML Services란

Microsoft Machine Learning Server를 사용하면 Azure에서 HDInsight 클러스터를 만들 때 배포 옵션으로 사용할 수 있습니다. 이 옵션을 제공하는 클러스터 유형을 **ML Services** 라고 합니다. 이 기능을 사용하면 HDInsight에서 융통성 있는 분산형 분석 메서드에 주문형으로 액세스할 수 있습니다.

HDInsight의 ML Services는 거의 모든 규모의 데이터 세트에 R 기반 분석을 수행할 수 있는 최신 기능을 제공합니다. 데이터 세트는 Azure Blob 또는 Data Lake Storage에 로드할 수 있습니다. R 기반 애플리케이션은 오픈 소스 R 패키지를 8000개 이상 사용할 수 있습니다. Microsoft의 빅 데이터 분석 패키지인 ScaleR의 루틴도 사용할 수 있습니다.

에지 노드는 클러스터에 연결하고 R 스크립트를 실행하기에 편리한 위치를 제공합니다. 에지 노드를 사용하면 서버 코어 전체에서 ScaleR 병렬화된 분산형 함수를 실행할 수 있습니다. 또한 ScaleR의 Hadoop Map Reduce를 사용하여 클러스터의 노드에서 실행할 수도 있습니다. Apache Spark 컴퓨팅 컨텍스트를 사용할 수도 있습니다.

분석 결과에서 얻은 모델 또는 예측을 온-프레미스 용도로 다운로드할 수 있습니다. 또한 Azure의 다른 곳에서 `operationalized`일 수 있습니다. 특히 [Azure Machine Learning Studio(클래식)](https://studio.azureml.net)와 [웹 서비스](../../machine-learning/classic/deploy-a-machine-learning-web-service.md)를 통해 가능합니다.

## <a name="get-started-with-ml-services-on-hdinsight"></a>HDInsight에서 ML Services 시작

HDInsight에서 ML Services 클러스터를 만들려면 **ML Services** 클러스터 유형을 선택합니다. ML Services 클러스터 유형에는 데이터 노드의 ML Server 및 에지 노드가 포함됩니다. 에지 노드는 ML Services 기반 분석을 위한 랜딩 존으로 사용됩니다. 클러스터를 만드는 방법에 대한 자세한 내용은 [Azure Portal을 사용하여 Apache Hadoop 클러스터 만들기](../hdinsight-hadoop-create-linux-clusters-portal.md)를 참조하세요.

## <a name="why-choose-ml-services-in-hdinsight"></a>HDInsight에서 ML Services를 사용하는 이유

HDInsight의 ML Services는 다음과 같은 이점을 제공합니다.

### <a name="ai-innovation-from-microsoft-and-open-source"></a>Microsoft 및 오픈-소스의 AI 혁신

  ML Services에는 [RevoscaleR](/machine-learning-server/r-reference/revoscaler/revoscaler), [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), [microsoftML](/machine-learning-server/python-reference/microsoftml/microsoftml-package)과 같이 융통성이 높은 분산형 알고리즘 세트가 포함됩니다. 이러한 알고리즘은 실제 메모리보다 크기가 큰 데이터에 대해 작동할 수 있습니다. 또한 매우 다양한 플랫폼에서 분산 방식으로 실행됩니다. 이 제품에 포함되어 있는 Microsoft의 사용자 지정 [R 패키지](/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 및 [Python 패키지](/machine-learning-server/python-reference/introducing-python-package-reference) 모음에 대해 자세히 알아보세요.
  
  ML Services는 이러한 Microsoft의 혁신 기술과 오픈 소스 커뮤니티(R, Python 및 AI 도구 키트)의 기여를 이어주는 가교 역할을 하며, 단일 엔터프라이즈급 플랫폼을 기반으로 합니다. 모든 R 또는 Python 오픈 소스 기계 학습 패키지는 Microsoft의 독자적인 혁신 기능과 함께 작동될 수 있습니다.

### <a name="simple-secure-and-high-scale-operationalization-and-administration"></a>간단하고 안전하고 확장성이 뛰어난 운용 및 관리

  기존 운용 패러다임 및 환경에 의존하는 기업은 이 영역으로 전환하기 위해 많은 시간과 노력을 투자해야 합니다. 이러한 조치를 취하면 모델의 변환 시간, 유효한 최신 상태로 유지하기 위한 반복 작업, 규제 승인 및 사용 권한 관리 등에 따른 비용 증가와 지연 문제가 발생합니다.

  ML Services는 엔터프라이즈급 [운용화](/machine-learning-server/what-is-operationalization)를 제공합니다. 기계 학습 모델이 완성되면 몇 번의 클릭만으로 웹 서비스 API를 생성할 수 있습니다. 이러한 [웹 서비스](/machine-learning-server/operationalize/concept-what-are-web-services)는 클라우드의 서버 그리드에서 호스트되며, LOB(기간 업무) 애플리케이션에 통합될 수 있습니다. 탄력적 그리드에 배포할 수 있으므로 일괄 처리 및 실시간 채점에 대한 비즈니스 요구에 맞춰 원활하게 확장 가능합니다. 지침을 보려면 [HDInsight에서 ML Services 운용](r-server-operationalize.md)을 참조하세요.

<!---
* **Deep ecosystem engagements to deliver customer success with optimal total cost of ownership**

  Individuals embarking on the journey of making their applications intelligent or simply wanting to learn the new world of AI and machine learning, need the right resources to help them get started. In addition to this documentation, Microsoft provides several learning resources and has engaged several training partners to help you ramp up and become productive quickly.
--->

> [!NOTE]  
> HDInsight의 ML 서비스 클러스터 유형은 HDInsight 3.6에서만 지원됩니다. HDInsight 3.6은 2020년 12월 31일에 사용 중지될 예정입니다.

## <a name="key-features-of-ml-services-on-hdinsight"></a>HDInsight의 ML Services 주요 기능

HDInsight의 ML Services에는 다음 기능이 포함됩니다.

| 기능 범주 | Description |
|------------------|-------------|
| R 지원 | R로 작성된 솔루션용 [R 패키지](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)(R의 오픈 소스 배포와 스크립트 실행을 위한 런타임 인프라 포함) |
| Python 지원 | Python으로 작성된 솔루션용 [Python 모듈](/machine-learning-server/python-reference/introducing-python-package-reference)(Python의 오픈 소스 배포와 스크립트 실행을 위한 런타임 인프라 포함)
| [미리 학습된 모델](/machine-learning-server/install/microsoftml-install-pretrained-models) | 시각적 분석 및 텍스트 감정 분석(사용자가 제공한 데이터를 채점할 수 있음) |
| [배포 및 사용](r-server-operationalize.md) | `Operationalize` 서버 및 솔루션을 웹 서비스로 배포합니다. |
| [원격 실행](r-server-hdinsight-manage.md#connect-remotely-to-microsoft-ml-services) | 클라이언트 워크스테이션에서 네트워크의 ML Services에 대한 원격 세션을 시작합니다. |

## <a name="data-storage-options-for-ml-services-on-hdinsight"></a>HDInsight의 ML Services에 대한 데이터 스토리지 옵션

HDFS 파일 시스템의 기본 스토리지는 Azure Storage 계정 또는 Azure Data Lake Storage일 수 있습니다. 분석 중에 클러스터 스토리지에 업로드된 데이터는 영구적입니다. 이러한 데이터는 클러스터가 삭제된 후에도 사용할 수 있습니다. 스토리지로 데이터 전송을 처리할 수 있는 도구는 다양합니다. 이 도구에는 스토리지 계정의 포털 기반 업로드 기능과 AzCopy 유틸리티가 포함됩니다.

클러스터를 만드는 동안 추가 Blob 및 Data Lake Store에 액세스가 가능하도록 설정할 수 있습니다. 사용 중인 기본 스토리지 옵션으로 제한되지 않습니다.  여러 스토리지 계정 사용에 대해 자세히 알아보려면 [HDInsight의 ML Services에 대한 Azure Storage 옵션](./r-server-storage.md) 문서를 참조하세요.

에지 노드에서 사용하기 위해 Azure Files를 스토리지 옵션으로 사용할 수도 있습니다. Azure Files를 사용하면 Azure Storage에 만든 파일 공유를 Linux 파일 시스템으로 사용하도록 설정할 수 있습니다. 자세한 내용은 [HDInsight의 ML Services에 대한 Azure Storage 옵션](r-server-storage.md)을 참조하세요.

## <a name="access-ml-services-edge-node"></a>ML Services 에지 노드 액세스

브라우저나 SSH/PuTTY를 사용하여 에지 노드의 Microsoft ML Server에 연결할 수 있습니다. R 콘솔은 클러스터를 만드는 동안 기본적으로 설치됩니다.  

## <a name="develop-and-run-r-scripts"></a>R 스크립트 개발 및 실행

R 스크립트는 8000개 이상의 오픈 소스 R 패키지를 사용할 수 있습니다. ScaleR 라이브러리에서 병렬화된 분산형 루틴을 사용할 수도 있습니다. 에지 노드에서 실행되는 스크립트는 해당 노드의 R 인터프리터 내에서 실행됩니다. 단, Map Reduce(RxHadoopMR) 또는 Spark(RxSpark) 컴퓨팅 컨텍스트를 사용하여 ScaleR 함수를 호출하는 단계는 제외됩니다. 이러한 함수는 데이터와 연결된 데이터 노드에서 분산 방식으로 실행됩니다. 컨텍스트 옵션에 대한 자세한 내용은 [HDInsight의 ML Services에 대한 컴퓨팅 컨텍스트 옵션](r-server-compute-contexts.md)을 참조하세요.

## <a name="operationalize-a-model"></a>`Operationalize` 모델

데이터 모델링이 완료되면 Azure 또는 온-프레미스에서 새 데이터를 예측하는 `operationalize` 모델을 운영할 수 있습니다. 이 프로세스를 점수 매기기라고 합니다. 점수 매기기는 HDInsight, Azure Machine Learning 또는 온-프레미스에서 수행할 수 있습니다.

### <a name="score-in-hdinsight"></a>HDInsight에서 점수 매기기

HDInsight에서 점수를 매기려면 R 함수를 작성합니다. 이 함수는 모델을 호출하여 스토리지 계정에 로드한 새 데이터 파일을 예측합니다. 그런 다음 예측을 스토리지 계정에 다시 저장합니다. 클러스터의 에지 노드에서 요청 시 루틴을 실행하거나 예약된 작업을 사용하여 루틴을 실행할 수 있습니다.

### <a name="score-in-azure-machine-learning-aml"></a>AML(Azure Machine Learning)에서 점수 매기기

Azure Machine Learning을 사용하여 점수를 매기려면 [AzureML](https://cran.r-project.org/src/contrib/Archive/AzureML/)로 알려진 오픈 소스 Azure Machine Learning R 패키지를 사용하여 모델을 Azure 웹 서비스로 게시합니다. 이 패키지는 편의상 에지 노드에 미리 설치됩니다. 다음으로, Azure Machine Learning의 기능을 사용하여 웹 서비스에 대한 사용자 인터페이스를 만든 후 점수 매기기에 필요한 대로 웹 서비스를 호출합니다. 그런 다음, ScaleR 모델 개체를 웹 서비스에서 사용할 동등한 오픈 소스 모델 개체로 변환합니다. 이 변환은 앙상블 기반 모델에 대해 ScaleR 강제 변환 함수(예: `as.randomForest()` )를 통해 수행할 수 있습니다.

### <a name="score-on-premises"></a>온-프레미스 점수 매기기

모델을 만든 후 온-프레미스 점수를 매기려면 R에서 모델을 직렬화하여 다운로드하고 역직렬화한 다음, 새 데이터의 점수를 매기는 데 사용합니다. [HDInsight에서 점수 매기기]에서 설명한 접근 방식을 사용하여 또는 [웹 서비스](/machine-learning-server/operationalize/concept-what-are-web-services)를 사용하여 새 데이터의 점수를 매길 수 있습니다.

## <a name="maintain-the-cluster"></a>클러스터 유지 관리

### <a name="install-and-maintain-r-packages"></a>R 패키지 설치 및 유지 관리

R 스크립트의 단계 대부분이 에지 노드에서 실행되므로 사용하는 R 패키지 대부분이 에지 노드에 필요합니다. 에지 노드에 추가 R 패키지를 설치하려면 R에서 `install.packages()` 메서드를 사용할 수 있습니다.

ScaleR 라이브러리 루틴만 사용하는 경우에는 일반적으로 R 패키지가 추가로 필요하지 않습니다. 데이터 노드에서 **rxExec** 또는 **RxDataStep** 을 실행하기 위한 추가 패키지가 필요할 수 있습니다.

추가 패키지는 클러스터를 만든 후 스크립트 작업을 통해 설치할 수 있습니다. 자세한 내용은 [HDInsight 클러스터에서 ML Services 관리](r-server-hdinsight-manage.md)를 참조하세요.

### <a name="change-apache-hadoop-mapreduce-memory-settings"></a>Apache Hadoop MapReduce 메모리 설정 변경

ML Services에 사용 가능한 메모리는 MapReduce 작업을 실행할 때 수정할 수 있습니다. 클러스터를 수정하려면 클러스터용 Apache Ambari UI를 사용합니다. Ambari UI 지침은 [Ambari 웹 UI를 사용하여 HDInsight 클러스터 관리](../hdinsight-hadoop-manage-ambari.md)를 참조하세요.

ML Services에 사용 가능한 메모리는 **RxHadoopMR** 호출에서 Hadoop 스위치를 사용하여 변경할 수 있습니다.

```r
hadoopSwitches = "-libjars /etc/hadoop/conf -Dmapred.job.map.memory.mb=6656"
```

### <a name="scale-your-cluster"></a>클러스터 규모 조정

포털을 통해 HDInsight의 기존 ML Services 클러스터를 확장하거나 축소할 수 있습니다. 확장하면 더 큰 처리 작업을 위한 추가 용량이 확보됩니다. 유휴 상태일 때는 클러스터를 다시 축소할 수 있습니다. 클러스터 크기를 조정하는 방법에 대한 지침은 [HDInsight 클러스터 관리](../hdinsight-administer-use-portal-linux.md)를 참조하세요.

### <a name="maintain-the-system"></a>시스템 유지 관리

OS 유지 관리는 업무 외 시간 동안 HDInsight 클러스터의 기본 Linux VM에서 수행됩니다. 일반적으로 유지 관리는 월요일과 목요일마다 오전 3시 30분(VM의 현지 시간)에 수행됩니다. 업데이트는 한 번에 1/4이 넘는 클러스터에 영향을 주지 않습니다.

유지 관리 중에는 작업 실행 속도가 느려질 수 있습니다. 하지만 완료될 때까지 계속 실행되어야 합니다. 모든 사용자 지정 소프트웨어 또는 로컬 데이터는 클러스터를 다시 빌드해야 하는 심각한 오류가 발생하지 않는 한 이러한 유지 관리에서 보존됩니다.

## <a name="ide-options-for-ml-services-on-hdinsight"></a>HDInsight의 ML Services에 대한 IDE 옵션

HDInsight 클러스터의 Linux 에지 노드는 R 기반 분석의 연결 영역입니다. 최신 버전의 HDInsight는 에지 노드에 RStudio Server의 브라우저 기반 IDE를 제공합니다. RStudio Server는 개발 및 실행 시 R 콘솔보다 생산성이 높습니다.

데스크톱 IDE는 원격 MapReduce 또는 Spark 컴퓨팅 컨텍스트를 통해 클러스터에 액세스할 수 있습니다. 옵션은 다음과 같습니다. Microsoft의 [RTVS](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)(Visual Studio용 R 도구), RStudio 및 Walware의 Eclipse 기반 StatET.

명령 프롬프트에 **R** 을 입력하여 에지 노드의 R 콘솔에 액세스합니다. 콘솔 인터페이스를 사용하는 경우 텍스트 편집기에서 R 스크립트를 개발하는 것이 편리합니다. 그런 다음, 필요에 맞게 스크립트의 섹션을 잘라내어 R 콘솔에 붙여넣습니다.

## <a name="pricing"></a>가격 책정

ML Services HDInsight 클러스터와 관련된 요금은 다른 HDInsight 클러스터 유형과 유사하게 구성됩니다. 이름, 데이터 및 에지 노드에서 기본 VM의 크기를 기반으로 합니다. 코어 시간 향상도 포함됩니다. 자세한 내용은 [HDInsight 가격](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.

## <a name="next-steps"></a>다음 단계

HDInsight 클러스터에서 ML Services를 사용하는 방법을 자세히 알아보려면 다음 항목을 참조하세요.

* [RStudio Server를 사용하여 Azure HDInsight의 ML Services 클러스터에서 R 스크립트 실행](machine-learning-services-quickstart-job-rstudio.md)
* [HDInsight에서 ML Services 클러스터에 대한 컴퓨팅 컨텍스트 옵션](r-server-compute-contexts.md)
* [HDInsight에서 ML Services 클러스터에 대한 스토리지 옵션](r-server-storage.md)