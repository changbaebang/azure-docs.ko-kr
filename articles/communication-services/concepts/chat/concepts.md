---
title: Azure Communication Services의 채팅 개념
titleSuffix: An Azure Communication Services concept document
description: Communication Services 채팅 개념에 대해 알아봅니다.
author: mikben
manager: jken
services: azure-communication-services
ms.author: mikben
ms.date: 09/30/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: e71917d917491037100b4ee666cbeb030b0a4786
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104656144"
---
# <a name="chat-concepts"></a>채팅 개념 

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]    

Azure Communication Services 채팅 클라이언트 라이브러리를 사용하여 실시간 텍스트 채팅을 애플리케이션에 추가할 수 있습니다. 이 페이지에는 주요 채팅 개념 및 기능이 요약되어 있습니다.    

특정 클라이언트 라이브러리 언어 및 기능에 대해 자세히 알아보려면 [Communication Services 채팅 클라이언트 라이브러리 개요](./sdk-features.md)를 참조하세요.    

## <a name="chat-overview"></a>채팅 개요    

채팅 대화는 채팅 스레드 내에서 발생합니다. 채팅 스레드에는 많은 메시지와 많은 사용자가 포함될 수 있습니다. 모든 메시지는 단일 스레드에 속하며 사용자는 하나 또는 여러 스레드의 일부가 될 수 있습니다. 채팅 스레드의 각 사용자를 참가자라고 합니다. 스레드 참가자만 메시지를 보내고 받을 수 있으며 채팅 스레드에서 다른 사용자를 추가하거나 제거할 수 있습니다. Communication Services는 채팅 스레드나 메시지에서 삭제 작업을 실행할 때까지 또는 채팅 스레드에 참가자가 남아 있지 않을 때까지 채팅 기록을 저장합니다. 이 때 채팅 스레드는 분리되어 삭제 대기 상태가 됩니다. 
    
## <a name="service-limits"></a>서비스 제한   

- 채팅 스레드에 허용되는 최대 참가자 수는 250명입니다.   
- 허용되는 최대 메시지 크기는 약 28KB입니다.  
- 참가자가 20명이 넘는 채팅 스레드의 경우 수신 확인 및 입력 표시기 기능이 지원되지 않습니다.    
- 
## <a name="chat-architecture"></a>채팅 아키텍처    

채팅 아키텍처에는 다음과 같은 두 가지 핵심 부분이 있습니다. 1) 신뢰할 수 있는 서비스 및 2) 클라이언트 애플리케이션.    

:::image type="content" source="../../media/chat-architecture.png" alt-text="Communication Services의 채팅 아키텍처를 보여주는 다이어그램"::: 

 - **신뢰할 수 있는 서비스:** 채팅 세션을 제대로 관리하려면 리소스 연결 문자열을 사용하여 Communication Services에 연결하는 데 도움이 되는 서비스가 필요합니다. 이 서비스는 채팅 스레드를 만들고, 스레드 참가자 목록을 관리하고, 사용자에게 액세스 토큰을 제공하는 작업을 담당합니다. 액세스 토큰에 대한 자세한 내용은 [액세스 토큰](../../quickstarts/access-tokens.md) 빠른 시작을 참조하세요.   
 - **클라이언트 앱:**  클라이언트 애플리케이션은 신뢰할 수 있는 서비스에 연결하고 Communication Services에 직접 연결하는 데 사용되는 액세스 토큰을 받습니다. 이 연결이 설정되면 클라이언트 앱에서 메시지를 보내고 받을 수 있습니다.   
신뢰할 수 있는 서비스 계층을 사용하여 액세스 토큰을 생성하는 것이 좋습니다. 이 시나리오에서 서버 쪽은 사용자를 만들고 관리하며 해당 토큰을 발급하는 일을 담당합니다.   
        
## <a name="message-types"></a>메시지 유형    

Communication Services 채팅은 사용자가 생성한 메시지 뿐만 아니라 **스레드 작업** 이라는 시스템 생성 메시지도 공유합니다. 스레드 작업은 채팅 스레드가 업데이트될 때 생성됩니다. 채팅 스레드에서 `List Messages` 또는 `Get Messages`를 호출하면 사용자가 생성한 텍스트 메시지는 물론 시스템 메시지가 시간 순서대로 결과에 포함됩니다. 이를 통해 참가자가 추가 또는 제거된 시기 또는 채팅 스레드 주제가 업데이트된 시기를 식별할 수 있습니다. 지원되는 메시지 유형은 다음과 같습니다.  
    
 - `Text`: 채팅 대화의 일부로 사용자가 작성하여 보낸 일반 문자 메시지입니다. 
 - `RichText/HTML`: 형식이 지정된 문자 메시지입니다. Communication Services 사용자는 현재 RichText 메시지를 보낼 수 없습니다. 이 메시지 유형은 Teams Interop 시나리오에서 Teams 사용자가 Communication Services 사용자에게 보내는 메시지에서 지원합니다.   
 - `ThreadActivity/ParticipantAdded`: 한 명 이상의 참가자가 채팅 스레드에 추가되었음을 나타내는 시스템 메시지입니다. 다음은 그 예입니다.  


``` 
{   
            "id": "1613589626560",  
            "type": "participantAdded", 
            "sequenceId": "7",  
            "version": "1613589626560", 
            "content":  
            {   
                "participants": 
                [   
                    {   
                        "id": "8:acs:d2a829bc-8523-4404-b727-022345e48ca6_00000008-511c-4df6-f40f-343a0d003226",    
                        "displayName": "Jane",  
                        "shareHistoryTime": "1970-01-01T00:00:00Z"  
                    }   
                ],  
                "initiator": "8:acs:d2a829bc-8523-4404-b727-022345e48ca6_00000008-511c-4ce0-f40f-343a0d003224"  
            },  
            "createdOn": "2021-02-17T19:20:26Z" 
        }   
``` 

- `ThreadActivity/ParticipantRemoved`: 참가자가 채팅 스레드에서 제거되었음을 나타내는 시스템 메시지입니다. 다음은 그 예입니다.   

``` 
{   
            "id": "1613589627603",  
            "type": "participantRemoved",   
            "sequenceId": "8",  
            "version": "1613589627603", 
            "content":  
            {   
                "participants": 
                [   
                    {   
                        "id": "8:acs:d2a829bc-8523-4404-b727-022345e48ca6_00000008-511c-4df6-f40f-343a0d003226",    
                        "displayName": "Jane",  
                        "shareHistoryTime": "1970-01-01T00:00:00Z"  
                    }   
                ],  
                "initiator": "8:acs:d2a829bc-8523-4404-b727-022345e48ca6_00000008-511c-4ce0-f40f-343a0d003224"  
            },  
            "createdOn": "2021-02-17T19:20:27Z" 
        }   
``` 

- `ThreadActivity/TopicUpdate`: 스레드 토픽이 업데이트되었음을 나타내는 시스템 메시지입니다. 다음은 그 예입니다.    
``` 
{   
            "id": "1613589623037",  
            "type": "topicUpdated", 
            "sequenceId": "2",  
            "version": "1613589623037", 
            "content":  
            {   
                "topic": "New topic",   
                "initiator": "8:acs:d2a829bc-8523-4404-b727-022345e48ca6_00000008-511c-4ce0-f40f-343a0d003224"  
            },  
            "createdOn": "2021-02-17T19:20:23Z" 
        }   
``` 

## <a name="real-time-signaling"></a>실시간 신호  

채팅 JavaScript 클라이언트 라이브러리는 실시간 신호를 포함합니다. 이를 통해 클라이언트는 API를 폴링하지 않고도 채팅 스레드에 들어오는 메시지와 실시간 업데이트를 수신 대기할 수 있습니다. 사용 가능한 이벤트는 다음과 같습니다.

 - `ChatMessageReceived` - 새 메시지가 채팅 스레드에 전송될 때. 이 이벤트는 이전 항목에서 언급한 자동 생성 시스템 메시지에 대해서는 전송되지 않습니다.   
 - `ChatMessageEdited` - 채팅 스레드에서 메시지가 편집될 때. 
 - `ChatMessageDeleted` - 채팅 스레드에서 메시지가 삭제될 때.   
 - `TypingIndicatorReceived` - 다른 참가자가 채팅 스레드에 메시지를 입력할 때.   
 - `ReadReceiptReceived` - 다른 참가자가 채팅 스레드에서 보낸 메시지를 읽었을 때.     
 - `ChatThreadCreated` - 통신 사용자가 채팅 스레드를 생성할 때. 
 - `ChatThreadDeleted` - 통신 사용자가 채팅 스레드를 삭제할 때. 
 - `ChatThreadPropertiesUpdated` - 채팅 스레드 속성이 업데이트된 경우 현재 스레드에 대한 항목 업데이트만 지원합니다.   
 - `ParticipantsAdded` - 사용자가 채팅 스레드에 참가자로 추가될 때.  
 - `ParticipantsRemoved` - 기존 참가자가 채팅 스레드에서 제거될 때.


## <a name="chat-events"></a>채팅 이벤트  

실시간 신호를 통해 사용자의 실시간 채팅이 가능합니다. 서비스는 Azure Event Grid를 사용하여 채팅 관련 이벤트를 구독할 수 있습니다. 자세한 내용은 [이벤트 처리 개념](https://docs.microsoft.com/azure/event-grid/event-schema-communication-services?tabs=event-grid-event-schema)을 참조하세요.


## <a name="using-cognitive-services-with-chat-client-library-to-enable-intelligent-features"></a>Cognitive Services를 채팅 클라이언트 라이브러리와 함께 사용하여 인텔리전트 기능 활성화 

[Azure Cognitive API](../../../cognitive-services/index.yml)를 채팅 클라이언트 라이브러리와 함께 사용하여 애플리케이션에 인텔리전트 기능을 추가할 수 있습니다. 예를 들어, 다음을 수행할 수 있습니다.  

- 사용자가 서로 다른 언어로 채팅할 수 있도록 합니다.  
- 고객의 문제 접수에서 부정적인 감정을 감지하여 지원 상담원이 티켓의 우선 순위를 지정하도록 돕습니다.   
- 들어오는 메시지에서 키 감지 및 엔터티 인식을 분석하여 메시지 내용을 기반으로 앱의 사용자에게 관련 정보를 표시합니다.

이러한 기능을 구현하는 한 가지 방법은 신뢰할 수 있는 서비스를 채팅 스레드에서 참가자로 사용하는 것입니다. 언어 번역을 활성화하려는 경우를 가정해 보겠습니다. 이 서비스는 다른 참가자가 서로 주고 받는 메시지를 듣고[1], Cognitive API를 호출하여 콘텐츠를 원하는 언어로 번역하고[2,3] 번역된 결과를 채팅 스레드에 메시지로 보내는[4] 작업을 담당합니다.

이렇게 하면 메시지 기록에 원본 메시지와 번역된 메시지가 모두 포함됩니다. 클라이언트 애플리케이션에서 원래 메시지 또는 번역된 메시지를 표시하는 논리를 추가할 수 있습니다. Cognitive API를 사용하여 텍스트를 다른 언어로 번역하는 방법을 이해하려면 [이 빠른 시작](../../../cognitive-services/translator/quickstart-translator.md)을 참조하세요. 
    
:::image type="content" source="../media/chat/cognitive-services.png" alt-text="Communication Services와 상호 작용하는 Cognitive Services를 보여주는 다이어그램"::: 

## <a name="next-steps"></a>다음 단계   

> [!div class="nextstepaction"] 
> [채팅 시작](../../quickstarts/chat/get-started.md)    

다음 문서는 사용자에게 유용할 수 있습니다.  
- [채팅 클라이언트 라이브러리](sdk-features.md) 숙지