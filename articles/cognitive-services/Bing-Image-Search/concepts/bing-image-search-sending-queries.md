---
title: 이미지 검색 쿼리 사용자 지정 및 제안-Bing Image Search API
titleSuffix: Azure Cognitive Services
description: Bing Image Search API에 보낸 검색 쿼리를 사용자 지정하는 것에 대해 알아봅니다.
services: cognitive-services
author: aahill
manager: nitinme
ms.assetid: C2862E98-8BCC-423B-9C4A-AC79A287BE38
ms.service: cognitive-services
ms.subservice: bing-image-search
ms.topic: conceptual
ms.date: 06/27/2019
ms.author: aahi
ms.openlocfilehash: 2566b2cf950df915f8ea843c34ea1fb6f8e7ea21
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96342008"
---
# <a name="customize-and-suggest-image-search-queries"></a>이미지 검색 쿼리 사용자 지정 및 제안

> [!WARNING]
> Bing Search API는 Cognitive Services에서 Bing Search Services로 이동합니다. **2020년 10월 30일** 부터 Bing Search의 모든 새 인스턴스는 [여기](/bing/search-apis/bing-web-search/create-bing-search-service-resource)에 설명된 프로세스에 따라 프로비저닝되어야 합니다.
> Cognitive Services를 사용하여 프로비저닝된 Bing Search API는 향후 3년 동안 또는 기업계약이 종료될 때까지(둘 중 먼저 도래할 때까지) 지원됩니다.
> 마이그레이션 지침은 [Bing Search Services](/bing/search-apis/bing-web-search/create-bing-search-service-resource)를 참조하세요.

이 문서를 사용 하 여 쿼리를 사용자 지정 하 고 Bing Image Search API에 보낼 검색어를 제안 하는 방법을 알아보세요.

## <a name="suggest-search-terms"></a>검색어 제안

앱에 검색어를 입력한 검색 상자가 있는 경우 환경을 개선하기 위해 [Bing Autosuggest API](../../bing-autosuggest/get-suggested-search-terms.md)를 사용할 수 있습니다. API는 제안된 검색어를 실시간으로 표시할 수 있습니다. API는 부분 검색어 및 Cognitive Services를 기반으로 제안된 쿼리 문자열을 반환합니다.

## <a name="pivot-the-query"></a>쿼리 피벗

Bing이 원래 검색 쿼리를 분할할 수 있는 경우 반환된 [이미지](/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#images) 개체에는 `pivotSuggestions`가 포함됩니다. 사용자에게 선택적 검색어로 피벗 제안을 표시할 수 있습니다. 예를 들어 원래 쿼리가 *Microsoft Surface* 인 경우 Bing은 쿼리를 *Microsoft* 및 *Surface* 로 분할하고 각각에 피벗을 제안할 수 있습니다. 사용자에게 선택적 쿼리 용어로 이러한 제안을 표시할 수 있습니다.

다음 예제에서는 *Microsoft Surface* 에 대한 피벗 제안 사항을 보여줍니다.  

```json
{
    "_type": "Images",
    "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=microsoft%20surface&FORM=OIIARP",
    "totalEstimatedMatches": 1000,
    "value": [...],
    "queryExpansions": [...],
    "pivotSuggestions": [{
        "pivot": "microsoft",
        "suggestions": [{
            "text": "Contoso Surface",
            "displayText": "Contoso",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=OtterBox+Surface&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=Contoso...",
                    "searchLink": "https:\/\/api.cognitive.microsoft.com\/api...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Contoso+Surface..."
            }
        },
        {
            "text": "Adatum Surface",
            "displayText": "Adatum",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Adatum+Surface&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Adatum+Surface&pid=Ap..."
            }
        },
        ...
        ]
    },
    {
        "pivot": "surface",
        "suggestions": [{
            "text": "Microsoft Surface4",
            "displayText": "Surface4",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface...",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft..."
            }
        },
        {
            "text": "Microsoft Tablet",
            "displayText": "Tablet",
            "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Tablet&FORM=IRQBPS",
            "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?...",
            "thumbnail": {
                "thumbnailUrl": "https:\/\/tse3.mm.bing.net\/th?q=Microsoft+Tablet..."
            }
        },
        ...
    ],
    "nextOffsetAddCount": 0
}
```

`pivotSuggestions` 필드에는 원래 쿼리가 분할된 세그먼트(피벗) 목록이 포함됩니다. 각 피벗에 대한 응답에는 제안된 쿼리를 포함하는 [쿼리](/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#query_obj) 개체 목록이 포함됩니다. `text` 필드에는 제안된 쿼리가 포함됩니다. `displayText` 필드에는 원래 쿼리의 피벗을 대체하는 용어가 포함됩니다. 예를 들어 Release Date of Surface(Surface의 릴리스 날짜)입니다.

피벗 쿼리 문자열이 사용자가 찾는 것이라면 `text` 및 `thumbnail` 필드를 사용하여 피벗 쿼리 문자열을 표시합니다. `webSearchUrl` URL 또는 `searchLink` URL을 사용하여 썸네일 및 텍스트를 클릭할 수 있게 만듭니다. `webSearchUrl`을 사용하여 Bing 검색 결과로 사용자를 보냅니다. 고유한 결과 페이지를 제공하는 경우 `searchLink`를 사용합니다.

<!-- Need a sanitized version of the image
The following shows an example of the pivot queries.

![Pivot suggestions](./media/cognitive-services-bing-images-api/bing-image-pivotsuggestion.GIF)
-->

## <a name="expand-the-query"></a>쿼리 확장

Bing이 원래 검색을 좁히기 위해 쿼리를 확장하는 경우 [이미지](/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#images) 개체에는 `queryExpansions` 필드가 포함됩니다. 예를 들어 쿼리가 *Microsoft Surface* 인 경우 확장된 쿼리는 다음과 같을 수 있습니다.
- Microsoft Surface **Pro 3**.
- Microsoft Surface **RT**.
- Microsoft Surface **Phone**.
- Microsoft Surface **Hub** 입니다.

다음 예제에서는 *Microsoft Surface* 에 대한 확장된 쿼리를 보여줍니다.

```json
{
    "_type": "Images",
    "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=microsoft%20surface...",
    "totalEstimatedMatches": 1000,
    "value": [...],
    "queryExpansions":  [{
        "text": "Microsoft Surface Pro 3",
        "displayText": "Pro 3",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+Pro+3...",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=Microsoft...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+Pro+3..."
        }
    },
    {
        "text": "Microsoft Surface RT",
        "displayText": "RT",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+RT...",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+RT..."
        }
    },
    {
        "text": "Microsoft Surface Phone",
        "displayText": "Phone",
        "webSearchUrl": "https:\/\/www.bing.com\/images\/search?q=Microsoft+Surface+Phone",
        "searchLink": "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images\/search?q=...",
        "thumbnail": {
            "thumbnailUrl": "https:\/\/tse4.mm.bing.net\/th?q=Microsoft+Surface+Phone..."
        }
    }],
    "pivotSuggestions": [...],
    "nextOffsetAddCount": 0
}
```

`queryExpansions` 필드에는 [쿼리](/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#query_obj) 개체 목록이 포함됩니다. `text` 필드에는 확장된 쿼리가 포함됩니다. `displayText` 필드에는 확장 용어가 포함됩니다. 확장된 쿼리 문자열이 사용자가 찾는 것이라면 `text` 및 `thumbnail` 필드를 사용하여 확장된 쿼리 문자열을 표시합니다. `webSearchUrl` URL 또는 `searchLink` URL을 사용하여 썸네일 및 텍스트를 클릭할 수 있게 만듭니다. `webSearchUrl`을 사용하여 Bing 검색 결과로 사용자를 보냅니다. 고유한 결과 페이지를 제공하는 경우 `searchLink`를 사용합니다.

<!-- Removing until we can replace with a sanitized image.
The following shows an example Bing implementation that uses expanded queries. If the user clicks the Microsoft Surface Pro 3 link, they're taken to the Bing search results page, which shows them images of the Pro 3.

![Query expansion suggestions](./media/cognitive-services-bing-images-api/bing-image-queryexpansion.GIF)
-->


## <a name="throttling-requests"></a>제한 요청

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a>다음 단계

Bing Image Search API를 사용해본 적이 없다면 [빠른 시작](../quickstarts/csharp.md)을 사용하세요. 더 복잡한 항목을 찾는 경우 [단일 페이지 웹앱](../tutorial-bing-image-search-single-page-app.md)을 만들기 위한 자습서를 사용하세요.