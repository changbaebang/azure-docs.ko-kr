---
title: 장식 표식을 사용하여 텍스트를 강조 표시하는 방법 - Bing Web Search API
titleSuffix: Azure Cognitive Services
description: Bing Web Search API를 사용하여 텍스트 장식을 사용하여 검색 결과에서 강조 표시를 적중하는 방법을 알아봅니다.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.assetid: 5365B568-EA55-4D97-8FBE-0AF60158D4D5
ms.service: cognitive-services
ms.subservice: bing-web-search
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: scottwhi
ms.openlocfilehash: 32c3279cacddf10e77e8d245ba525ab766efd6fd
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96351881"
---
# <a name="using-decoration-markers-to-highlight-text"></a>장식 표식을 사용하여 텍스트를 강조 표시

> [!WARNING]
> Bing Search API는 Cognitive Services에서 Bing Search Services로 이동합니다. **2020년 10월 30일** 부터 Bing Search의 모든 새 인스턴스는 [여기](/bing/search-apis/bing-web-search/create-bing-search-service-resource)에 설명된 프로세스에 따라 프로비저닝되어야 합니다.
> Cognitive Services를 사용하여 프로비저닝된 Bing Search API는 향후 3년 동안 또는 기업계약이 종료될 때까지(둘 중 먼저 도래할 때까지) 지원됩니다.
> 마이그레이션 지침은 [Bing Search Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource)를 참조하세요.

Bing은 몇 가지 답변의 표시 문자열에서 쿼리 용어 (또는 Bing에서 관련 된 다른 용어)를 표시 하는 적중 항목 강조 표시를 지원 합니다. 예를 들어, 웹 페이지 결과의 `name` , `displayUrl` 및 필드에는 표시 된 `snippet` 쿼리 용어가 포함 될 수 있습니다. 

기본적으로 Bing은 표시 문자열에 강조 표시 마커를 포함하지 않습니다. 표식을 사용 하도록 설정 하려면 `textDecorations` 요청에 쿼리 매개 변수를 포함 하 고로 설정 `true` 합니다.

## <a name="hit-highlighting-example"></a>적중 항목 강조 표시 예제

다음 예제에서는에 대 한 웹 결과를 보여 줍니다 `Sailing Dinghy` . Bing은 E000 및 E001 유니코드 문자를 사용 하 여 쿼리 용어의 시작과 끝을 표시 합니다.
  
![적중 항목 강조 표시](./media/cognitive-services-bing-web-api/bing-hit-highlighting.png) 

사용자 인터페이스에 결과를 표시 하기 전에 유니코드 문자를 표시 형식에 적합 한 문자로 바꿉니다.

## <a name="marker-formatting"></a>표식 서식 지정

Bing에서는 유니코드 문자 또는 HTML 태그를 표식으로 사용할 수 있는 옵션을 제공 합니다. 사용할 표식을 지정 하려면 [textFormat](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference#textformat) 쿼리 매개 변수를 포함 합니다. 

| 값             | 표식                       |
|-------------------|------------------------------|
| `textFormat=Raw`  | 유니코드 문자 (기본값) |
| `textFormat=HTML` | HTML 문자              |

## <a name="additional-text-decorations"></a>추가 텍스트 장식

Bing은 여러 다른 텍스트 장식을 반환할 수 있습니다. 예를 들어 대답에는 `Computation` 필드의 쿼리 용어에 대 한 아래 첨자 표식이 포함 될 수 있습니다 `log(2)` `expression` .

![계산 마커](./media/cognitive-services-bing-web-api/bing-markers-computation.png) 

요청에서 장식을 지정 하지 않은 경우 필드에는 `expression` 가 포함 됩니다 `log10(2)` . 

`textDecorations`가 이면 `true` Bing은 응답 표시 문자열에 다음 표식을 포함할 수 있습니다. 해당 하는 HTML 태그가 없는 경우 테이블 셀은 비어 있습니다.

|유니코드(Unicode)|HTML|설명
|-|-|-
|U+E000|\<b>|쿼리 용어의 시작을 표시(적중 항목 강조 표시)
|U+E001|\</b>|쿼리 용어의 끝을 표시
|U+E002|\<i>|기울임꼴로 표시된 콘텐츠의 시작을 표시 
|U+E003|\</i>|기울임꼴로 표시된 콘텐츠의 끝을 표시
|U+E004|\<br/>|줄 바꿈을 표시
|U+E005||전화 번호의 시작을 표시
|U+E006||전화 번호의 끝을 표시
|U+E007||주소의 시작을 표시
|U+E008||주소의 끝을 표시
|U+E009|\&nbsp;|줄 바꿈하지 않는 공백을 표시
|U+E00C|\<strong>|굵게 표시된 콘텐츠의 시작을 표시
|U+E00D|\</strong>|굵게 표시된 콘텐츠의 끝을 표시
|U+E00E||배경이 주변 배경보다 밝아야 하는 콘텐츠의 시작을 표시
|U+E00F||배경이 주변 배경보다 밝아야 하는 콘텐츠의 끝을 표시
|U+E010||배경이 주변 배경보다 어두워야 하는 콘텐츠의 시작을 표시
|U+E011||배경이 주변 배경보다 어두워야 하는 콘텐츠의 끝을 표시
|U+E012|\<del>|취소선을 그어야 하는 콘텐츠의 시작을 표시
|U+E013|\</del>|취소선을 그어야 하는 콘텐츠의 끝을 표시
|U+E016|\<sub>|아래 첨자 콘텐츠의 시작을 표시
|U+E017|\</sub>|아래 첨자 콘텐츠의 끝을 표시
|U+E018|\<sup>|위 첨자 콘텐츠의 시작을 표시
|U+E019|\</sup>|위 첨자 콘텐츠의 끝을 표시

## <a name="next-steps"></a>다음 단계

* [Bing Web Search API란?](overview.md) 
* [크기 조정 및 자르기 썸네일](resize-and-crop-thumbnails.md)