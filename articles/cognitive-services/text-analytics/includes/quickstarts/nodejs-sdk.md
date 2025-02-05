---
title: '빠른 시작: Node.js용 Text Analytics v3 클라이언트 라이브러리 | Microsoft Docs'
description: Node.js용 v3 Text Analytics 클라이언트 라이브러리를 시작합니다.
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: include
ms.date: 02/09/2021
ms.author: aahi
ms.reviewer: sumeh, assafi
ms.custom: devx-track-js
ms.openlocfilehash: 60676310f3176c86e2dcb752428eb27730c63fc3
ms.sourcegitcommit: ba676927b1a8acd7c30708144e201f63ce89021d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2021
ms.locfileid: "102445643"
---
<a name="HOLTop"></a>

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

[v3 참조 설명서](/javascript/api/overview/azure/ai-text-analytics-readme?preserve-view=true&view=azure-node-preview) | [v3 라이브러리 소스 코드](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics) | [v3 패키지(NPM)](https://www.npmjs.com/package/@azure/ai-text-analytics) | [v3 샘플](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics/samples)


# <a name="version-30"></a>[버전 3.0](#tab/version-3)

[v3 참조 설명서](/javascript/api/overview/azure/ai-text-analytics-readme) | [v3 라이브러리 소스 코드](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics) | [v3 패키지(NPM)](https://www.npmjs.com/package/@azure/ai-text-analytics) | [v3 샘플](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics/samples)


---

## <a name="prerequisites"></a>사전 요구 사항

* Azure 구독 - [체험 구독 만들기](https://azure.microsoft.com/free/cognitive-services)
* 현재 버전의 [Node.js](https://nodejs.org/)
* Azure 구독을 보유한 후에는 Azure Portal에서 <a href="https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesTextAnalytics"  title="Text Analytics 리소스를 만들어"  target="_blank">Text Analytics 리소스를 만들어</a> 키와 엔드포인트를 가져옵니다. 배포 후 **리소스로 이동** 을 클릭합니다.
    * 애플리케이션을 Text Analytics API에 연결하려면 만든 리소스의 키와 엔드포인트가 필요합니다. 이 빠른 시작의 뒷부분에 나오는 코드에 키와 엔드포인트를 붙여넣습니다.
    * 평가판 가격 책정 계층(`F0`)을 통해 서비스를 사용해보고, 나중에 프로덕션용 유료 계층으로 업그레이드할 수 있습니다.
* Analyze(분석) 기능을 사용하려면 표준 가격 책정 계층을 사용하는 Text Analytics 리소스가 필요합니다.

## <a name="setting-up"></a>설치

### <a name="create-a-new-nodejs-application"></a>새 Node.js 애플리케이션 만들기

콘솔 창(예: cmd, PowerShell 또는 Bash)에서 앱에 대한 새 디렉터리를 만들고 이 디렉터리로 이동합니다. 

```console
mkdir myapp 

cd myapp
```

`package.json` 파일을 사용하여 노드 애플리케이션을 만들려면 `npm init` 명령을 실행합니다. 

```console
npm init
```
### <a name="install-the-client-library"></a>클라이언트 라이브러리 설치

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

`@azure/ai-text-analytics` NPM 패키지 설치:

```console
npm install --save @azure/ai-text-analytics@5.1.0-beta.3
```

> [!TIP]
> 한 번에 전체 빠른 시작 코드 파일을 보시겠습니까? [GitHub에서](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/javascript/TextAnalytics/text-analytics-v3-client-library.js) 찾을 수 있으며 이 빠른 시작의 코드 예제를 포함합니다. 


# <a name="version-30"></a>[버전 3.0](#tab/version-3)

`@azure/ai-text-analytics` NPM 패키지 설치:

```console
npm install --save @azure/ai-text-analytics@5.0.0
```

> [!TIP]
> 한 번에 전체 빠른 시작 코드 파일을 보시겠습니까? [GitHub에서](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/javascript/TextAnalytics/text-analytics-v3-client-library.js) 찾을 수 있으며 이 빠른 시작의 코드 예제를 포함합니다. 

---

종속성이 있는 앱의 `package.json` 파일이 업데이트됩니다.
`index.js`라는 파일을 만들고 다음을 추가합니다.

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

```javascript
"use strict";

const { TextAnalyticsClient, AzureKeyCredential } = require("@azure/ai-text-analytics");
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

```javascript
"use strict";

const { TextAnalyticsClient, AzureKeyCredential } = require("@azure/ai-text-analytics");
```

---

리소스의 Azure 엔드포인트 및 키에 대한 변수를 만듭니다.

[!INCLUDE [text-analytics-find-resource-information](../find-azure-resource-info.md)]

```javascript
const key = '<paste-your-text-analytics-key-here>';
const endpoint = '<paste-your-text-analytics-endpoint-here>';
```

## <a name="object-model"></a>개체 모델

Text Analytics 클라이언트는 키를 사용하여 Azure에 인증하는 `TextAnalyticsClient` 개체입니다. 클라이언트는 텍스트를 단일 문자열 또는 일괄 처리로 분석하는 몇 가지 메서드를 제공합니다.

텍스트는 사용된 메서드에 따라 `id`, `text` 및 `language` 특성의 조합이 포함된 `dictionary` 개체인 `documents`의 목록으로 API에 보내집니다. `text` 특성은 분석할 텍스트를 `language` 원본에 저장하며, `id`는 임의의 값이 될 수 있습니다. 

응답 개체는 각 문서에 대한 분석 정보가 포함된 목록입니다. 

## <a name="code-examples"></a>코드 예제

* [클라이언트 인증](#client-authentication)
* [감정 분석](#sentiment-analysis) 
* [오피니언 마이닝](#opinion-mining)
* [언어 감지](#language-detection)
* [명명된 엔터티 인식](#named-entity-recognition-ner)
* [엔터티 연결](#entity-linking)
* 개인 식별이 가능한 정보
* [핵심 구 추출](#key-phrase-extraction)

## <a name="client-authentication"></a>클라이언트 인증

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

키와 엔드포인트를 매개 변수로 사용하여 새 `TextAnalyticsClient` 개체를 만듭니다.

```javascript
const textAnalyticsClient = new TextAnalyticsClient(endpoint,  new AzureKeyCredential(key));
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

키와 엔드포인트를 매개 변수로 사용하여 새 `TextAnalyticsClient` 개체를 만듭니다.

```javascript
const textAnalyticsClient = new TextAnalyticsClient(endpoint,  new AzureKeyCredential(key));
```

---

## <a name="sentiment-analysis"></a>정서 분석

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `analyzeSentiment()` 메서드를 호출하고 반환된 `SentimentBatchResult` 개체를 가져옵니다. 결과 목록을 반복하고 각 문서의 ID, 문서 수준 감정을 신뢰도 점수로 인쇄합니다. 각 문서에 대해 결과에는 오프셋, 길이 및 신뢰도 점수와 함께 문장 수준 감정이 포함됩니다.

```javascript
async function sentimentAnalysis(client){

    const sentimentInput = [
        "I had the best day of my life. I wish you were there with me."
    ];
    const sentimentResult = await client.analyzeSentiment(sentimentInput);

    sentimentResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tDocument Sentiment: ${document.sentiment}`);
        console.log(`\tDocument Scores:`);
        console.log(`\t\tPositive: ${document.confidenceScores.positive.toFixed(2)} \tNegative: ${document.confidenceScores.negative.toFixed(2)} \tNeutral: ${document.confidenceScores.neutral.toFixed(2)}`);
        console.log(`\tSentences Sentiment(${document.sentences.length}):`);
        document.sentences.forEach(sentence => {
            console.log(`\t\tSentence sentiment: ${sentence.sentiment}`)
            console.log(`\t\tSentences Scores:`);
            console.log(`\t\tPositive: ${sentence.confidenceScores.positive.toFixed(2)} \tNegative: ${sentence.confidenceScores.negative.toFixed(2)} \tNeutral: ${sentence.confidenceScores.neutral.toFixed(2)}`);
        });
    });
}
sentimentAnalysis(textAnalyticsClient)
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Document Sentiment: positive
        Document Scores:
                Positive: 1.00  Negative: 0.00  Neutral: 0.00
        Sentences Sentiment(2):
                Sentence sentiment: positive
                Sentences Scores:
                Positive: 1.00  Negative: 0.00  Neutral: 0.00
                Sentence sentiment: neutral
                Sentences Scores:
                Positive: 0.21  Negative: 0.02  Neutral: 0.77
```

### <a name="opinion-mining"></a>의견 마이닝

오피리언 마이닝을 사용하여 감정 분석을 수행하려면 분석하려는 문서가 포함된 문자열의 배열을 만듭니다. 옵션 플래그 `includeOpinionMining: true`를 추가하여 클라이언트의 `analyzeSentiment()` 메서드를 호출하고 반환된 `SentimentBatchResult` 개체를 가져옵니다. 결과 목록을 반복하고 각 문서의 ID, 문서 수준 감정을 신뢰도 점수로 인쇄합니다. 각 문서에 대해 결과는 위와 같은 문장 수준 감정뿐만 아니라 측면 및 의견 수준 감정도 포함합니다.

```javascript
async function sentimentAnalysisWithOpinionMining(client){

    const sentimentInput = [
        {
            text: "The food and service were unacceptable, but the concierge were nice",
            id: "0",
            language: "en"
        }
    ];
    const sentimentResult = await client.analyzeSentiment(sentimentInput, { includeOpinionMining: true });

    sentimentResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tDocument Sentiment: ${document.sentiment}`);
        console.log(`\tDocument Scores:`);
        console.log(`\t\tPositive: ${document.confidenceScores.positive.toFixed(2)} \tNegative: ${document.confidenceScores.negative.toFixed(2)} \tNeutral: ${document.confidenceScores.neutral.toFixed(2)}`);
        console.log(`\tSentences Sentiment(${document.sentences.length}):`);
        document.sentences.forEach(sentence => {
            console.log(`\t\tSentence sentiment: ${sentence.sentiment}`)
            console.log(`\t\tSentences Scores:`);
            console.log(`\t\tPositive: ${sentence.confidenceScores.positive.toFixed(2)} \tNegative: ${sentence.confidenceScores.negative.toFixed(2)} \tNeutral: ${sentence.confidenceScores.neutral.toFixed(2)}`);
            console.log("\tMined opinions");
            for (const { aspect, opinions } of sentence.minedOpinions) {
                console.log(`\t\tAspect text: ${aspect.text}`);
                console.log(`\t\tAspect sentiment: ${aspect.sentiment}`);
                console.log(`\t\tAspect Positive: ${aspect.confidenceScores.positive.toFixed(2)} \tNegative: ${aspect.confidenceScores.negative.toFixed(2)}`);
                console.log("\t\tAspect opinions:");
                for (const { text, sentiment, confidenceScores } of opinions) {
                    console.log(`\t\tOpinion text: ${text}`);
                    console.log(`\t\tOpinion sentiment: ${sentiment}`);
                    console.log(`\t\tOpinion Positive: ${confidenceScores.positive.toFixed(2)} \tNegative: ${confidenceScores.negative.toFixed(2)}`);
                }
            }
        });
    });
}
sentimentAnalysisWithOpinionMining(textAnalyticsClient)
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Document Sentiment: positive
        Document Scores:
                Positive: 0.84  Negative: 0.16  Neutral: 0.00
        Sentences Sentiment(1):
                Sentence sentiment: positive
                Sentences Scores:
                Positive: 0.84  Negative: 0.16  Neutral: 0.00
        Mined opinions
                Aspect text: food
                Aspect sentiment: negative
                Aspect Positive: 0.01   Negative: 0.99
                Aspect opinions:
                Opinion text: unacceptable
                Opinion sentiment: negative
                Opinion Positive: 0.01  Negative: 0.99
                Aspect text: service
                Aspect sentiment: negative
                Aspect Positive: 0.01   Negative: 0.99
                Aspect opinions:
                Opinion text: unacceptable
                Opinion sentiment: negative
                Opinion Positive: 0.01  Negative: 0.99
                Aspect text: concierge
                Aspect sentiment: positive
                Aspect Positive: 1.00   Negative: 0.00
                Aspect opinions:
                Opinion text: nice
                Opinion sentiment: positive
                Opinion Positive: 1.00  Negative: 0.00
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `analyzeSentiment()` 메서드를 호출하고 반환된 `SentimentBatchResult` 개체를 가져옵니다. 결과 목록을 반복하고 각 문서의 ID, 문서 수준 감정을 신뢰도 점수로 인쇄합니다. 각 문서에 대해 결과에는 오프셋, 길이 및 신뢰도 점수와 함께 문장 수준 감정이 포함됩니다.

```javascript
async function sentimentAnalysis(client){

    const sentimentInput = [
        "I had the best day of my life. I wish you were there with me."
    ];
    const sentimentResult = await client.analyzeSentiment(sentimentInput);

    sentimentResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tDocument Sentiment: ${document.sentiment}`);
        console.log(`\tDocument Scores:`);
        console.log(`\t\tPositive: ${document.confidenceScores.positive.toFixed(2)} \tNegative: ${document.confidenceScores.negative.toFixed(2)} \tNeutral: ${document.confidenceScores.neutral.toFixed(2)}`);
        console.log(`\tSentences Sentiment(${document.sentences.length}):`);
        document.sentences.forEach(sentence => {
            console.log(`\t\tSentence sentiment: ${sentence.sentiment}`)
            console.log(`\t\tSentences Scores:`);
            console.log(`\t\tPositive: ${sentence.confidenceScores.positive.toFixed(2)} \tNegative: ${sentence.confidenceScores.negative.toFixed(2)} \tNeutral: ${sentence.confidenceScores.neutral.toFixed(2)}`);
        });
    });
}
sentimentAnalysis(textAnalyticsClient)
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Document Sentiment: positive
        Document Scores:
                Positive: 1.00  Negative: 0.00  Neutral: 0.00
        Sentences Sentiment(2):
                Sentence sentiment: positive
                Sentences Scores:
                Positive: 1.00  Negative: 0.00  Neutral: 0.00
                Sentence sentiment: neutral
                Sentences Scores:
                Positive: 0.21  Negative: 0.02  Neutral: 0.77
```

---

## <a name="language-detection"></a>언어 검색

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `detectLanguage()` 메서드를 호출하고 반환된 `DetectLanguageResultCollection`를 가져옵니다. 그런 다음, 결과를 반복하고 각 문서의 ID를 해당 기본 언어로 인쇄합니다.

```javascript
async function languageDetection(client) {

    const languageInputArray = [
        "Ce document est rédigé en Français."
    ];
    const languageResult = await client.detectLanguage(languageInputArray);

    languageResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tPrimary Language ${document.primaryLanguage.name}`)
    });
}
languageDetection(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Primary Language French
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `detectLanguage()` 메서드를 호출하고 반환된 `DetectLanguageResultCollection`를 가져옵니다. 그런 다음, 결과를 반복하고 각 문서의 ID를 해당 기본 언어로 인쇄합니다.

```javascript
async function languageDetection(client) {

    const languageInputArray = [
        "Ce document est rédigé en Français."
    ];
    const languageResult = await client.detectLanguage(languageInputArray);

    languageResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tPrimary Language ${document.primaryLanguage.name}`)
    });
}
languageDetection(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Primary Language French
```

---

## <a name="named-entity-recognition-ner"></a>NER(명명된 엔터티 인식)

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

> [!NOTE]
> 버전 `3.1`에서 다음을 수행합니다.
> * 엔터티 연결은 NER과 별개의 요청입니다.

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `recognizeEntities()` 메서드를 호출하고 `RecognizeEntitiesResult` 개체를 가져옵니다. 결과 목록을 반복하고 엔터티 이름, 형식, 하위 유형, 오프셋, 길이 및 점수를 인쇄합니다.

```javascript
async function entityRecognition(client){

    const entityInputs = [
        "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800",
        "La sede principal de Microsoft se encuentra en la ciudad de Redmond, a 21 kilómetros de Seattle."
    ];
    const entityResults = await client.recognizeEntities(entityInputs);

    entityResults.forEach(document => {
        console.log(`Document ID: ${document.id}`);
        document.entities.forEach(entity => {
            console.log(`\tName: ${entity.text} \tCategory: ${entity.category} \tSubcategory: ${entity.subCategory ? entity.subCategory : "N/A"}`);
            console.log(`\tScore: ${entity.confidenceScore}`);
        });
    });
}
entityRecognition(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
Document ID: 0
        Name: Microsoft         Category: Organization  Subcategory: N/A
        Score: 0.29
        Name: Bill Gates        Category: Person        Subcategory: N/A
        Score: 0.78
        Name: Paul Allen        Category: Person        Subcategory: N/A
        Score: 0.82
        Name: April 4, 1975     Category: DateTime      Subcategory: Date
        Score: 0.8
        Name: 8800      Category: Quantity      Subcategory: Number
        Score: 0.8
Document ID: 1
        Name: 21        Category: Quantity      Subcategory: Number
        Score: 0.8
        Name: Seattle   Category: Location      Subcategory: GPE
        Score: 0.25
```

### <a name="entity-linking"></a>엔터티 연결

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `recognizeLinkedEntities()` 메서드를 호출하고 `RecognizeLinkedEntitiesResult` 개체를 가져옵니다. 결과 목록을 반복하고 엔터티 이름, ID, 데이터 원본, url 및 일치 항목을 인쇄합니다. `matches` 배열의 모든 개체에는 해당 일치 항목에 대한 오프셋, 길이 및 점수가 포함됩니다.

```javascript
async function linkedEntityRecognition(client){

    const linkedEntityInput = [
        "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800. During his career at Microsoft, Gates held the positions of chairman, chief executive officer, president and chief software architect, while also being the largest individual shareholder until May 2014."
    ];
    const entityResults = await client.recognizeLinkedEntities(linkedEntityInput);

    entityResults.forEach(document => {
        console.log(`Document ID: ${document.id}`);
        document.entities.forEach(entity => {
            console.log(`\tName: ${entity.name} \tID: ${entity.dataSourceEntityId} \tURL: ${entity.url} \tData Source: ${entity.dataSource}`);
            console.log(`\tMatches:`)
            entity.matches.forEach(match => {
                console.log(`\t\tText: ${match.text} \tScore: ${match.confidenceScore.toFixed(2)}`);
        })
        });
    });
}
linkedEntityRecognition(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
Document ID: 0
        Name: Altair 8800       ID: Altair 8800         URL: https://en.wikipedia.org/wiki/Altair_8800  Data Source: Wikipedia
        Matches:
                Text: Altair 8800       Score: 0.88
        Name: Bill Gates        ID: Bill Gates  URL: https://en.wikipedia.org/wiki/Bill_Gates   Data Source: Wikipedia
        Matches:
                Text: Bill Gates        Score: 0.63
                Text: Gates     Score: 0.63
        Name: Paul Allen        ID: Paul Allen  URL: https://en.wikipedia.org/wiki/Paul_Allen   Data Source: Wikipedia
        Matches:
                Text: Paul Allen        Score: 0.60
        Name: Microsoft         ID: Microsoft   URL: https://en.wikipedia.org/wiki/Microsoft    Data Source: Wikipedia
        Matches:
                Text: Microsoft         Score: 0.55
                Text: Microsoft         Score: 0.55
        Name: April 4   ID: April 4     URL: https://en.wikipedia.org/wiki/April_4      Data Source: Wikipedia
        Matches:
                Text: April 4   Score: 0.32
        Name: BASIC     ID: BASIC       URL: https://en.wikipedia.org/wiki/BASIC        Data Source: Wikipedia
        Matches:
                Text: BASIC     Score: 0.33
```

### <a name="personally-identifying-information-pii-recognition"></a>PII(개인 식별 정보) 인식

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `recognizePiiEntities()` 메서드를 호출하고 `RecognizePIIEntitiesResult` 개체를 가져옵니다. 결과 목록을 반복하고 엔터티 이름, 형식 및 점수를 인쇄합니다.

```javascript
async function piiRecognition(client) {

    const documents = [
        "The employee's phone number is (555) 555-5555."
    ];

    const results = await client.recognizePiiEntities(documents, "en");
    for (const result of results) {
        if (result.error === undefined) {
            console.log("Redacted Text: ", result.redactedText);
            console.log(" -- Recognized PII entities for input", result.id, "--");
            for (const entity of result.entities) {
                console.log(entity.text, ":", entity.category, "(Score:", entity.confidenceScore, ")");
            }
        } else {
            console.error("Encountered an error:", result.error);
        }
    }
}
piiRecognition(textAnalyticsClient)
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
Redacted Text:  The employee's phone number is **************.
 -- Recognized PII entities for input 0 --
(555) 555-5555 : Phone Number (Score: 0.8 )
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

> [!NOTE]
> 버전 `3.0`에서 다음을 수행합니다.
> * 엔터티 연결은 NER과 별개의 요청입니다.

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `recognizeEntities()` 메서드를 호출하고 `RecognizeEntitiesResult` 개체를 가져옵니다. 결과 목록을 반복하고 엔터티 이름, 형식, 하위 유형, 오프셋, 길이 및 점수를 인쇄합니다.

```javascript
async function entityRecognition(client){

    const entityInputs = [
        "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800",
        "La sede principal de Microsoft se encuentra en la ciudad de Redmond, a 21 kilómetros de Seattle."
    ];
    const entityResults = await client.recognizeEntities(entityInputs);

    entityResults.forEach(document => {
        console.log(`Document ID: ${document.id}`);
        document.entities.forEach(entity => {
            console.log(`\tName: ${entity.text} \tCategory: ${entity.category} \tSubcategory: ${entity.subCategory ? entity.subCategory : "N/A"}`);
            console.log(`\tScore: ${entity.confidenceScore}`);
        });
    });
}
entityRecognition(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
Document ID: 0
        Name: Microsoft         Category: Organization  Subcategory: N/A
        Score: 0.29
        Name: Bill Gates        Category: Person        Subcategory: N/A
        Score: 0.78
        Name: Paul Allen        Category: Person        Subcategory: N/A
        Score: 0.82
        Name: April 4, 1975     Category: DateTime      Subcategory: Date
        Score: 0.8
        Name: 8800      Category: Quantity      Subcategory: Number
        Score: 0.8
Document ID: 1
        Name: 21        Category: Quantity      Subcategory: Number
        Score: 0.8
        Name: Seattle   Category: Location      Subcategory: GPE
        Score: 0.25
```

### <a name="entity-linking"></a>엔터티 연결

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `recognizeLinkedEntities()` 메서드를 호출하고 `RecognizeLinkedEntitiesResult` 개체를 가져옵니다. 결과 목록을 반복하고 엔터티 이름, ID, 데이터 원본, url 및 일치 항목을 인쇄합니다. `matches` 배열의 모든 개체에는 해당 일치 항목에 대한 오프셋, 길이 및 점수가 포함됩니다.

```javascript
async function linkedEntityRecognition(client){

    const linkedEntityInput = [
        "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800. During his career at Microsoft, Gates held the positions of chairman, chief executive officer, president and chief software architect, while also being the largest individual shareholder until May 2014."
    ];
    const entityResults = await client.recognizeLinkedEntities(linkedEntityInput);

    entityResults.forEach(document => {
        console.log(`Document ID: ${document.id}`);
        document.entities.forEach(entity => {
            console.log(`\tName: ${entity.name} \tID: ${entity.dataSourceEntityId} \tURL: ${entity.url} \tData Source: ${entity.dataSource}`);
            console.log(`\tMatches:`)
            entity.matches.forEach(match => {
                console.log(`\t\tText: ${match.text} \tScore: ${match.confidenceScore.toFixed(2)}`);
        })
        });
    });
}
linkedEntityRecognition(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
Document ID: 0
        Name: Altair 8800       ID: Altair 8800         URL: https://en.wikipedia.org/wiki/Altair_8800  Data Source: Wikipedia
        Matches:
                Text: Altair 8800       Score: 0.88
        Name: Bill Gates        ID: Bill Gates  URL: https://en.wikipedia.org/wiki/Bill_Gates   Data Source: Wikipedia
        Matches:
                Text: Bill Gates        Score: 0.63
                Text: Gates     Score: 0.63
        Name: Paul Allen        ID: Paul Allen  URL: https://en.wikipedia.org/wiki/Paul_Allen   Data Source: Wikipedia
        Matches:
                Text: Paul Allen        Score: 0.60
        Name: Microsoft         ID: Microsoft   URL: https://en.wikipedia.org/wiki/Microsoft    Data Source: Wikipedia
        Matches:
                Text: Microsoft         Score: 0.55
                Text: Microsoft         Score: 0.55
        Name: April 4   ID: April 4     URL: https://en.wikipedia.org/wiki/April_4      Data Source: Wikipedia
        Matches:
                Text: April 4   Score: 0.32
        Name: BASIC     ID: BASIC       URL: https://en.wikipedia.org/wiki/BASIC        Data Source: Wikipedia
        Matches:
                Text: BASIC     Score: 0.33
```


---

## <a name="key-phrase-extraction"></a>핵심 문구 추출

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `extractKeyPhrases()` 메서드를 호출하고 반환된 `ExtractKeyPhrasesResult` 개체를 가져옵니다. 결과를 반복하고 각 문서의 ID 및 검색된 주요 문구를 인쇄합니다.

```javascript
async function keyPhraseExtraction(client){

    const keyPhrasesInput = [
        "My cat might need to see a veterinarian.",
    ];
    const keyPhraseResult = await client.extractKeyPhrases(keyPhrasesInput);
    
    keyPhraseResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tDocument Key Phrases: ${document.keyPhrases}`);
    });
}
keyPhraseExtraction(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Document Key Phrases: cat,veterinarian
```

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

분석할 문서가 포함된 문자열 배열을 만듭니다. 클라이언트의 `extractKeyPhrases()` 메서드를 호출하고 반환된 `ExtractKeyPhrasesResult` 개체를 가져옵니다. 결과를 반복하고 각 문서의 ID 및 검색된 주요 문구를 인쇄합니다.

```javascript
async function keyPhraseExtraction(client){

    const keyPhrasesInput = [
        "My cat might need to see a veterinarian.",
    ];
    const keyPhraseResult = await client.extractKeyPhrases(keyPhrasesInput);
    
    keyPhraseResult.forEach(document => {
        console.log(`ID: ${document.id}`);
        console.log(`\tDocument Key Phrases: ${document.keyPhrases}`);
    });
}
keyPhraseExtraction(textAnalyticsClient);
```

콘솔 창에서 `node index.js`를 사용하여 코드를 실행합니다.

### <a name="output"></a>출력

```console
ID: 0
        Document Key Phrases: cat,veterinarian
```


---

## <a name="use-the-api-asynchronously-with-the-analyze-operation"></a>Analyze(분석) 작업을 통해 비동기적으로 API 사용

# <a name="version-31-preview"></a>[버전 3.1 미리 보기](#tab/version-3-1)

> [!CAUTION]
> Analyze(분석) 작업을 사용하려면 표준 가격 책정 계층을 사용하는 Text Analytics 리소스를 사용해야 합니다.  

`beginAnalyze()` 함수를 호출하는 `analyze_example()`이라는 새 함수를 만듭니다. 그러면 장기 실행 작업이 실행되고 결과가 폴링됩니다.

```javascript
const documents = [
  "Microsoft was founded by Bill Gates and Paul Allen.",
];

async function analyze_example(client) {
  console.log("== Analyze Sample ==");

  const tasks = {
    entityRecognitionTasks: [{ modelVersion: "latest" }]
  };
  const poller = await client.beginAnalyze(documents, tasks);
  const resultPages = await poller.pollUntilDone();

  for await (const page of resultPages) {
    const entitiesResults = page.entitiesRecognitionResults![0];
    for (const doc of entitiesResults) {
      console.log(`- Document ${doc.id}`);
      if (!doc.error) {
        console.log("\tEntities:");
        for (const entity of doc.entities) {
          console.log(`\t- Entity ${entity.text} of type ${entity.category}`);
        }
      } else {
        console.error("  Error:", doc.error);
      }
    }
  }
}

analyze_example(textAnalyticsClient);
```

### <a name="output"></a>출력

```console
== Analyze Sample ==
- Document 0
        Entities:
        - Entity Microsoft of type Organization
        - Entity Bill Gates of type Person
        - Entity Paul Allen of type Person
```

Analyze(분석) 작업을 사용하여 PII 및 핵심 문구 추출을 검색할 수도 있습니다. GitHub의 [JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics/samples/javascript) 및 [TypeScript](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics/samples/typescript/src) Analyze(분석) 샘플을 참조하세요.

# <a name="version-30"></a>[버전 3.0](#tab/version-3)

이 기능은 버전 3.0에서 사용할 수 없습니다.

---

## <a name="run-the-application"></a>애플리케이션 실행

quickstart 파일의 `node` 명령을 사용하여 애플리케이션을 실행합니다.

```console
node index.js
```
