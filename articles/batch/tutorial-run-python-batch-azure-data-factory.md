---
title: 자습서 - Data Factory를 통해 Python 스크립트 실행
description: Azure Batch를 사용하여 Azure Data Factory를 통해 Python 스크립트를 파이프라인의 일부로 실행하는 방법을 알아봅니다.
author: pkshultz
ms.devlang: python
ms.topic: tutorial
ms.date: 03/12/2021
ms.author: peshultz
ms.custom: mvc, devx-track-python
ms.openlocfilehash: 241a47ccf9021c6065fea907b4d9914744a64972
ms.sourcegitcommit: afb9e9d0b0c7e37166b9d1de6b71cd0e2fb9abf5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2021
ms.locfileid: "103461694"
---
# <a name="tutorial-run-python-scripts-through-azure-data-factory-using-azure-batch"></a>자습서: Azure Batch를 사용하여 Azure Data Factory를 통해 Python 스크립트 실행

이 자습서에서는 다음을 수행하는 방법을 알아봅니다.

> [!div class="checklist"]
> * Batch 및 Storage 계정 인증
> * Python에서 스크립트 개발 및 실행
> * 컴퓨팅 노드 풀을 만들어 애플리케이션 실행
> * Python 워크로드 예약
> * 분석 파이프라인 모니터링
> * 로그 파일에 액세스

아래 예제에서는 Blob 스토리지 컨테이너에서 CSV 입력을 받고, 데이터 조작 프로세스를 수행하며, 출력을 별도의 Blob 스토리지 컨테이너에 쓰는 Python 스크립트를 실행합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/)을 만듭니다.

## <a name="prerequisites"></a>필수 구성 요소

* 로컬 테스트를 위해 설치된 [Python](https://www.python.org/downloads/) 배포
* [azure-storage-blob](https://pypi.org/project/azure-storage-blob/) `pip` 패키지.
* [iris.csv 데이터 세트](https://github.com/Azure-Samples/batch-adf-pipeline-tutorial/blob/master/iris.csv)
* Azure Batch 계정 및 연결된 Azure Storage 계정. Batch 계정을 만들고 스토리지 계정에 연결하는 방법에 대한 자세한 내용은 [Batch 계정 만들기](quick-create-portal.md#create-a-batch-account)를 참조하세요.
* Azure Data Factory 계정. Azure Portal을 통해 데이터 팩터리를 만드는 방법에 대한 자세한 내용은 [데이터 팩터리 만들기](../data-factory/quickstart-create-data-factory-portal.md#create-a-data-factory)를 참조하세요.
* [Batch Explorer](https://azure.github.io/BatchExplorer/)
* [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).

## <a name="sign-in-to-azure"></a>Azure에 로그인

[https://portal.azure.com](https://portal.azure.com)에서 Azure Portal에 로그인합니다.

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)]

## <a name="create-a-batch-pool-using-batch-explorer"></a>Batch Explorer를 사용하여 Batch 풀 만들기

이 섹션에서는 Batch Explorer를 사용하여 Azure Data factory 파이프라인에서 사용할 Batch 풀을 만듭니다. 

1. Azure 자격 증명을 사용하여 Batch Explorer에 로그인합니다.
1. Batch 계정 선택
1. 왼쪽 메뉴 모음에서 **풀** 을 선택한 다음, 검색 양식 위의 **추가** 버튼을 선택하여 풀을 만듭니다. 
    1. ID와 표시 이름을 선택합니다. 이 예제에서는 `custom-activity-pool`을 사용합니다.
    1. 크기 조정 유형을 **고정 크기** 로 설정하고 전용 노드 수를 2로 설정합니다.
    1. **데이터 과학** 아래에서 운영 체제로 **Dsvm Windows** 를 선택합니다.
    1. 가상 머신 크기에 `Standard_f2s_v2`를 선택합니다.
    1. 시작 작업을 사용하도록 설정하고 `cmd /c "pip install azure-storage-blob pandas"` 명령을 추가합니다. 사용자 ID는 기본 **풀 사용자** 로 유지할 수 있습니다.
    1. **확인** 을 선택합니다.

## <a name="create-blob-containers"></a>Blob 컨테이너 만들기

여기에서는 OCR Batch 작업에 대한 입력 및 출력 파일을 저장하는 Blob 컨테이너를 만듭니다.

1. Azure 자격 증명을 사용하여 Storage Explorer에 로그인합니다.
1. Batch 계정에 연결된 스토리지 계정을 사용하여 [Blob 컨테이너 만들기](../vs-azure-tools-storage-explorer-blobs.md#create-a-blob-container)의 단계에 따라 두 개의 Blob 컨테이너(입력 파일용 1개, 출력 파일용 1개)를 만듭니다.
    * 이 예제에서는 입력 컨테이너 `input`과 출력 컨테이너 `output`을 호출합니다.
1. [Blob 컨테이너의 Blob 관리](../vs-azure-tools-storage-explorer-blobs.md#managing-blobs-in-a-blob-container)의 단계에 따라 Storage Explorer를 사용하여 [`iris.csv`](https://github.com/Azure-Samples/batch-adf-pipeline-tutorial/blob/master/iris.csv)를 입력 컨테이너 `input`에 업로드합니다.

## <a name="develop-a-script-in-python"></a>Python에서 스크립트 개발

다음 Python 스크립트는 `input` 컨테이너에서 `iris.csv` 데이터 세트를 로드하고, 데이터 조작 프로세스를 수행하며, 결과를 `output` 컨테이너에 다시 저장합니다.

``` python
# Load libraries
from azure.storage.blob import BlobClient
import pandas as pd

# Define parameters
connectionString = "<storage-account-connection-string>"
containerName = "output"
outputBlobName  = "iris_setosa.csv"

# Establish connection with the blob storage account
blob = BlobClient.from_connection_string(conn_str=connectionString, container_name=containerName, blob_name=outputBlobName)

# Load iris dataset from the task node
df = pd.read_csv("iris.csv")

# Take a subset of the records
df = df[df['Species'] == "setosa"]

# Save the subset of the iris dataframe locally in task node
df.to_csv(outputBlobName, index = False)

with open(outputBlobName, "rb") as data:
    blob.upload_blob(data)
```

스크립트를 `main.py`로 저장하고 **Azure Storage** `input` 컨테이너에 업로드합니다. Blob 컨테이너에 업로드하기 전에 해당 기능을 로컬로 테스트하고 확인해야 합니다.

``` bash
python main.py
```

## <a name="set-up-an-azure-data-factory-pipeline"></a>Azure Data Factory 파이프라인 설정

이 섹션에서는 Python 스크립트를 사용하여 파이프라인을 만들고 유효성을 검사합니다.

1. [이 문서](../data-factory/quickstart-create-data-factory-portal.md#create-a-data-factory)의 "데이터 팩터리 만들기" 섹션에서 설명하는 데이터 팩터리를 만드는 단계를 수행합니다.
1. **팩터리 리소스** 상자에서 더하기(+) 단추, **파이프라인** 을 차례로 선택합니다.
1. **일반** 탭에서 파이프라인 이름을 "Python 실행"으로 설정합니다.

    ![일반 탭에서 파이프라인 이름을 "Python 실행"으로 설정합니다.](./media/run-python-batch-azure-data-factory/create-pipeline.png)

1. **활동** 상자에서 **Batch 서비스** 를 펼칩니다. 사용자 지정 활동을 **활동** 도구 상자에서 파이프라인 디자이너 화면으로 끌어서 놓습니다. 사용자 지정 작업에 대해 다음 탭을 작성합니다.
    1. **일반** 탭에서 이름에 **testPipeline** 을 지정합니다. ![일반 탭에서 이름에 testPipeline을 지정합니다.](./media/run-python-batch-azure-data-factory/create-custom-task.png)
    1. **Azure Batch** 탭에서 이전 단계에서 만든 **Batch 계정** 과 **연결 테스트** 를 추가하여 성공적으로 연결되었는지 확인합니다.
    ![Azure Batch 탭에서 이전 단계에서 만든 Batch 계정을 추가한 다음, 연결을 테스트합니다.](./media/run-python-batch-azure-data-factory/integrate-pipeline-with-azure-batch.png)
    1. **설정** 탭에서 다음을 수행합니다.
        1. **명령** 을 `python main.py`로 설정합니다.
        1. **리소스 연결된 서비스** 에 대해 이전 단계에서 만든 스토리지 계정을 추가합니다. 연결을 테스트하여 성공적으로 연결되었는지 확인합니다.
        1. **폴더 경로** 에서 Python 스크립트와 관련 입력이 포함된 **Azure Blob Storage** 컨테이너의 이름을 선택합니다. 그러면 Python 스크립트를 실행하기 전에 선택한 파일이 컨테이너에서 풀 노드 인스턴스로 다운로드됩니다.

        ![폴더 경로에서 Azure Blob 스토리지 컨테이너의 이름을 선택합니다.](./media/run-python-batch-azure-data-factory/create-custom-task-py-script-command.png)

1. 캔버스 위에 있는 파이프라인 도구 모음에서 **유효성 검사** 를 클릭하여 파이프라인 설정의 유효성을 검사합니다. 파이프라인에 대한 유효성이 성공적으로 검사되었는지 확인합니다. 유효성 검사 출력을 닫으려면 &gt;&gt;(오른쪽 화살표) 단추를 선택합니다.
1. **디버그** 를 클릭하여 파이프라인을 테스트하고 파이프라인이 정확하게 작동하는지 확인합니다.
1. **게시** 를 클릭하여 파이프라인을 게시합니다.
1. **트리거** 를 클릭하여 Python 스크립트를 일괄 처리 프로세스의 일부로 실행합니다.

    ![트리거를 클릭하여 Python 스크립트를 일괄 처리 프로세스의 일부로 실행합니다.](./media/run-python-batch-azure-data-factory/create-custom-task-py-success-run.png)

### <a name="monitor-the-log-files"></a>로그 파일 모니터링

스크립트 실행에서 경고 또는 오류를 생성하는 경우 기록된 출력에 대한 자세한 내용은 `stdout.txt` 또는 `stderr.txt`에서 확인할 수 있습니다.

1. Batch Explorer의 왼쪽에서 **작업** 을 선택합니다.
1. 데이터 팩터리에서 만든 작업을 선택합니다. 풀 이름을 `custom-activity-pool`이라고 가정하고 `adfv2-custom-activity-pool`을 선택합니다.
1. 오류 종료 코드가 있는 작업을 클릭합니다.
1. `stdout.txt` 및 `stderr.txt`를 확인하여 문제를 조사하고 진단합니다.

## <a name="clean-up-resources"></a>리소스 정리

작업 및 태스크 자체에 대한 요금이 부과되지 않지만 컴퓨팅 노드에 대한 요금이 청구됩니다. 따라서 풀을 필요할 때만 할당하는 것이 좋습니다. 풀을 삭제하면 노드의 모든 태스크 출력이 삭제됩니다. 그러나 입력 및 출력 파일은 스토리지 계정에 남아 있습니다. 더 이상 필요하지 않은 경우 Batch 계정과 스토리지 계정을 삭제할 수도 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.

> [!div class="checklist"]
> * Batch 및 Storage 계정 인증
> * Python에서 스크립트 개발 및 실행
> * 컴퓨팅 노드 풀을 만들어 애플리케이션 실행
> * Python 워크로드 예약
> * 분석 파이프라인 모니터링
> * 로그 파일에 액세스

Azure Data Factory에 대해 자세히 알아보려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [Azure Data Factory 개요](../data-factory/introduction.md)
