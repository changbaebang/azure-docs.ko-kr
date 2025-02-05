---
title: Autosuggest 검색어 - Bing Web Search API
titleSuffix: Azure Cognitive Services
description: Bing Web Search API는 Bing Autosuggest API와 함께 사용자에게 향상된 검색 환경을 제공합니다.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-web-search
ms.topic: conceptual
ms.date: 03/03/2019
ms.author: aahi
ms.openlocfilehash: 1a3f479fbbe68c8880cd7fefb3b57c77d4cfbbfe
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96349574"
---
# <a name="autosuggest-bing-search-terms-in-your-application"></a>애플리케이션의 Autosuggest Bing 검색어

> [!WARNING]
> Bing Search API는 Cognitive Services에서 Bing Search Services로 이동합니다. **2020년 10월 30일** 부터 Bing Search의 모든 새 인스턴스는 [여기](/bing/search-apis/bing-web-search/create-bing-search-service-resource)에 설명된 프로세스에 따라 프로비저닝되어야 합니다.
> Cognitive Services를 사용하여 프로비저닝된 Bing Search API는 향후 3년 동안 또는 기업계약이 종료될 때까지(둘 중 먼저 도래할 때까지) 지원됩니다.
> 마이그레이션 지침은 [Bing Search Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource)를 참조하세요.

사용자가 자신의 검색 용어를 입력할 수 있는 검색 상자를 제공하는 경우 [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md)를 사용하여 환경을 개선합니다. API는 부분 검색 용어 기반의 제안된 쿼리 문자열을 사용자 형식으로 반환합니다.

사용자가 검색 용어를 입력한 후, 이는 [q](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference#query) 쿼리 매개 변수가 설정되기 전에 인코딩된 URL이어야 합니다. 예를 들어 사용자가 입력 *소형 범선* 을 입력한 경우 `q`를 `sailing+dinghies` 또는 `sailing%20dinghies`로 설정합니다.

쿼리 용어에 오타가 있는 경우 검색 응답은 [QueryContext](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference#querycontext) 개체를 포함합니다. 이 개체는 원래 철자 및 Bing이 검색에 사용한 수정된 철자를 보여 줍니다.

```json
"queryContext": {
    "originalQuery": "sialing dingy for sale",
    "alteredQuery": "sailing dinghy for sale",
    "alterationOverrideQuery": "+sialing +dingy for sale"
}
```

검색 결과를 표시하는 경우 해당 쿼리 문자열을 수정했음을 사용자에게 알리도록 이 정보를 사용할 수 있습니다.

![쿼리 컨텍스트 UX 예제](./media/cognitive-services-bing-web-api/bing-query-context.PNG)  

## <a name="next-steps"></a>다음 단계  

* 샘플 [Bing Web Search API 응답](search-responses.md)을 참조하세요.  

## <a name="see-also"></a>참고 항목  

* [Bing Web Search API 참조](/rest/api/cognitiveservices-bingsearch/bing-web-api-v7-reference)