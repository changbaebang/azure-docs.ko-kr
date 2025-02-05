---
title: Computer Vision의 새로운 기능
titleSuffix: Azure Cognitive Services
description: 이 문서에는 Computer Vision에 대한 뉴스가 포함되어 있습니다.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: overview
ms.date: 01/13/2021
ms.author: pafarley
ms.openlocfilehash: 78746e7623f58af5ae9df829b48245295dc39f01
ms.sourcegitcommit: 8d1b97c3777684bd98f2cfbc9d440b1299a02e8f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102487103"
---
# <a name="whats-new-in-computer-vision"></a>Computer Vision의 새로운 기능

서비스의 새로운 기능에 대해 알아봅니다. 이러한 항목은 릴리스 정보, 비디오, 블로그 게시물 및 기타 유형의 정보입니다. 이 페이지에 책갈피를 설정하여 서비스를 최신 상태로 유지하세요.

## <a name="march-2021"></a>2021년 3월

### <a name="computer-vision-32-public-preview-update"></a>Computer Vision 3.2 공개 미리 보기 업데이트

Computer Vision API v3.2 공개 미리 보기가 업데이트되었습니다. 미리 보기 릴리스에는 업데이트된 읽기 및 분석 API와 함께 모든 Computer Vision 기능이 포함되어 있습니다.

> [!div class="nextstepaction"]
> [Computer Vision v3.2 공개 미리 보기 3 살펴보기](https://westus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2-preview-3/operations/5d986960601faab4bf452005)

## <a name="february-2021"></a>2021년 2월

### <a name="read-api-v32-public-preview-with-ocr-support-for-73-languages"></a>73개 언어에 대한 OCR 지원이 포함된 Read API v3.2 공개 미리 보기
클라우드 서비스 및 Docker 컨테이너로 사용할 수 있는 Computer Vision의 Read API v3.2 공개 미리 보기에는 다음 업데이트가 포함되어 있습니다.
* 중국어 간체 및 번체, 일본어, 한국어 및 라틴어를 포함한 [73개 언어에 대한 OCR](./language-support.md#optical-character-recognition-ocr)
* 텍스트 줄 출력의 자연스러운 읽기 순서(라틴어 언어에만 해당)
* 텍스트 줄의 필기 스타일 분류와 신뢰도 점수(라틴어 언어에만 해당).
* 다중 페이지 문서의 경우 선택한 페이지의 텍스트만 추출합니다.
* 온-프레미스 배포에 [Distroless 컨테이너](./computer-vision-how-to-install-containers.md?tabs=version-3-2)로 사용할 수 있습니다.

Read API에 대한 [자세한 정보](concept-recognizing-text.md)

> [!div class="nextstepaction"]
> [Read API v3.2 공개 미리 보기 사용](https://westus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2-preview-3/operations/5d986960601faab4bf452005)


## <a name="january-2021"></a>2021년 1월

### <a name="spatial-analysis-container-update"></a>공간 분석 컨테이너 업데이트

새 기능 집합과 함께 새 버전의 [공간 분석 컨테이너](spatial-analysis-container.md)가 릴리스되었습니다. 이 Docker 컨테이너를 사용하면 실시간 스트리밍 비디오를 분석하여 사용자와 사용자의 물리적 환경 간 이동의 공간 관계를 이해할 수 있습니다. 

* 이제 [공간 분석 작업](spatial-analysis-operations.md)을 구성하여 사람이 마스크와 같은 얼굴 보호 커버를 착용하고 있는지 감지할 수 있습니다. 
    * `ENABLE_FACE_MASK_CLASSIFIER` 매개 변수를 구성하여 `personcount`, `personcrossingline` 및 `personcrossingpolygon` 작업에 대해 마스크 분류자를 사용할 수 있습니다.
    * `face_mask` 및 `face_noMask` 특성은 비디오 스트림에서 검색된 각 사람에 대한 신뢰 점수와 함께 메타데이터로 반환됩니다.
* *personcrossingpolygon* 작업은 사람이 영역에서 소비하는 체류 시간을 계산할 수 있도록 확장되었습니다. 작업의 영역 구성에서 `type` 매개 변수를 `zonedwelltime`으로 설정할 수 있으며 새로운 이벤트 형식 *personZoneDwellTimeEvent* 에는 사람이 영역에서 소비한 시간(밀리초)으로 채워진 `durationMs` 필드가 포함됩니다.
* **호환성이 손상되는 변경**: *personZoneEvent* 이벤트의 이름이 *personZoneEnterExitEvent* 로 변경되었습니다. 이 이벤트는 사람이 영역에 들어가거나 영역에서 나갈 때 *personcrossingpolygon* 작업에 의해 발생하며, 사람이 건넌 영역의 번호가 매겨진 쪽을 사용하여 방향 정보를 제공합니다.
* 비디오 URL은 모든 작업에서 "프라이빗 매개 변수/난독 처리"로 제공할 수 있습니다. 난독 처리는 현재 선택 사항이며 `KEY` 및 `IV`가 환경 변수로 제공되는 경우에만 작동합니다.
* 보정은 기본적으로 모든 작업에 사용하도록 설정됩니다. `do_calibration: false`를 설정하여 사용하지 않도록 설정합니다.
* `enable_recalibration` 매개 변수를 통해 자동 재보정(기본적으로 해제됨)을 사용하기 위한 추가 지원에 대한 자세한 내용은 [공간 분석 작업](./spatial-analysis-operations.md)을 참조하세요.
* 카메라 보정 매개 변수가 `DETECTOR_NODE_CONFIG`로 설정되었습니다. 자세한 내용은 [공간 분석 작업](./spatial-analysis-operations.md)을 참조하세요.


## <a name="october-2020"></a>2020년 10월

### <a name="computer-vision-api-v31-ga"></a>Computer Vision API v3.1 GA

일반 공급의 Computer Vision API v3.1로 업그레이드되었습니다.

## <a name="september-2020"></a>2020년 9월

### <a name="spatial-analysis-container-preview"></a>공간 분석 컨테이너 미리 보기

[공간 분석 컨테이너](spatial-analysis-container.md)는 현재 미리 보기로 제공됩니다. Computer Vision의 공간 분석 기능을 사용하면 실시간 스트리밍 비디오를 분석하여 사용자와 사용자의 물리적 환경 간 이동의 공간 관계를 이해할 수 있습니다. 공간 분석은 온-프레미스에서 사용할 수 있는 Docker 컨테이너입니다. 

### <a name="read-api-v31-public-preview-adds-ocr-for-japanese"></a>Read API v3.1 공개 미리 보기에 일본어용 OCR 추가
Computer Vision의 Read API v3.1 공개 미리 보기에 다음 기능이 추가되었습니다.
* 일본어용 OCR
* 각 텍스트 줄에 글꼴이 필기체인지, 활자체인지와 신뢰도 점수(라틴어만 해당)를 지정합니다.
* 다중 페이지 문서의 경우 선택한 페이지 또는 페이지 범위에 대해서만 텍스트를 추출합니다.

* 이 미리 보기 버전의 Read API는 영어, 네덜란드어, 프랑스어, 독일어, 이탈리아어, 일본어, 포르투갈어, 중국어 간체 및 스페인어를 지원합니다.

자세한 내용은 [Read API 개요](concept-recognizing-text.md)를 참조하세요.

> [!div class="nextstepaction"]
> [Read API v3.1 공개 미리 보기 2에 대한 자세한 정보](https://westus2.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-1-preview-2/operations/5d986960601faab4bf452005)

## <a name="july-2020"></a>2020년 7월

### <a name="read-api-v31-public-preview-with-ocr-for-simplified-chinese"></a>Read API v3.1 공개 미리 보기에 중국어(간체)용 OCR 추가
Computer Vision의 Read API v3.1 공개 미리 보기에는 중국어(간체) 지원이 추가되었습니다.

* 이 미리 보기 버전의 Read API는 영어, 네덜란드어, 프랑스어, 독일어, 이탈리아어, 포르투갈어, 중국어 간체 및 스페인어를 지원합니다.

자세한 내용은 [Read API 개요](concept-recognizing-text.md)를 참조하세요.

> [!div class="nextstepaction"]
> [Read API v3.1 공개 미리 보기 1에 대한 자세한 정보](https://westus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-1-preview-1/operations/5d986960601faab4bf452005)

## <a name="may-2020"></a>2020년 5월
Computer Vision API v3.0에서 [읽기 API](concept-recognizing-text.md)에 대한 업데이트와 함께 일반 공급으로 전환되었습니다.

* 영어, 네덜란드어, 프랑스어, 독일어, 이탈리아어, 포르투갈어 및 스페인어 지원
* 정확도 개선
* 추출된 각 단어에 대한 신뢰도 점수
* 새 출력 형식

## <a name="march-2020"></a>2020년 3월

* 이제 TLS 1.2는 이 서비스에 대한 모든 HTTP 요청에 적용됩니다. 자세한 내용은 [Azure Cognitive Services 보안](../cognitive-services-security.md)을 참조하세요.

## <a name="january-2020"></a>2020년 1월

### <a name="read-api-30-public-preview"></a>Read API 3.0 공개 미리 보기

이제 Read API의 버전 3.0을 사용하여 이미지에서 인쇄 또는 필기한 텍스트를 추출할 수 있습니다. 이전 버전과 비교하여 3.0은 다음을 제공합니다.
* 정확도 개선
* 새 출력 형식
* 추출된 각 단어에 대한 신뢰도 점수
* 추가 언어 매개 변수를 사용하여 스페인어 및 영어 모두 지원

3\.0 API 사용을 시작하려면 [텍스트 추출 빠른 시작](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/dotnet/ComputerVision/REST/CSharp-hand-text.md?tabs=version-3)을 따르세요.

## <a name="cognitive-service-updates"></a>Cognitive Service 업데이트

[Cognitive Services에 대한 Azure 업데이트 공지](https://azure.microsoft.com/updates/?product=cognitive-services)