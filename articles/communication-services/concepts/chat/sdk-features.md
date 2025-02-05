---
title: Azure Communication Services에 대한 채팅 클라이언트 라이브러리 개요
titleSuffix: An Azure Communication Services concept document
description: Azure Communication Services 채팅 클라이언트 라이브러리에 대해 알아봅니다.
author: mikben
manager: jken
services: azure-communication-services
ms.author: mikben
ms.date: 09/30/2020
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: 705bd926c2ac6f414464254969b5c511c88891f0
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104656110"
---
# <a name="chat-client-library-overview"></a>채팅 클라이언트 라이브러리 개요  

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]    

Azure Communication Services 채팅 클라이언트 라이브러리를 사용하여 다양한 실시간 채팅을 애플리케이션에 추가할 수 있습니다.
    
## <a name="chat-client-library-capabilities"></a>채팅 클라이언트 라이브러리 기능 

다음 목록에서는 현재 Communication Services 채팅 클라이언트 라이브러리에서 사용할 수 있는 기능 세트를 보여 줍니다.  

| 기능 그룹 | 기능 | JavaScript  | Java | .NET | Python | iOS | Android |
|-----------------|-------------------|---|-----|----|-----|----|----|
| 핵심 기능 | 2명 이상의 사용자 간 채팅 스레드 만들기(최대 250명의 사용자)                                                       | ✔️   | ✔️  | ✔️    | ✔️   |  ✔️    | ✔️   |    
|                   | 채팅 스레드의 토픽 업데이트                                                                              | ✔️   | ✔️ | ✔️    | ✔️   |  ✔️    | ✔️   |   
|                   | 채팅 스레드에서 참가자 추가 또는 제거                                                                           | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |  
|                   | 추가되는 참가자와 채팅 메시지 기록을 공유할지 여부를 선택합니다.                                   | ✔️   | ✔️   | ✔️    | ✔️  |  ✔️    | ✔️   | 
|                   | 채팅 스레드의 참가자 목록 가져오기                                                                          | ✔️   | ✔️  | ✔️ | ✔️ |  ✔️    | ✔️   | 
|                   | 채팅 스레드 삭제                                                                                              | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |    
|                   | 통신 사용자가 지정되면 사용자가 속한 채팅 스레드 목록을 가져옵니다.                                           | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |   
|                   | 특정 채팅 스레드에 대한 정보 가져오기                                                                              | ✔️   | ✔️  | ✔️ | ✔️ |  ✔️    | ✔️   |   
|                   | 채팅 스레드에서 메시지 보내기 및 받기                                                                            | ✔️   | ✔️   | ✔️    | ✔️  |  ✔️    | ✔️   |   
|                   | 보낸 메시지의 내용 편집                                                                                | ✔️   | ✔️  | ✔️ | ✔️ |  ✔️    | ✔️   |   
|                   | 메시지 삭제                                                                                                       | ✔️   | ✔️  | ✔️ | ✔️ |  ✔️    | ✔️   |   
|                   | 채팅의 다른 참가자가 읽은 메시지에 대한 수신 확인 <br/> *채팅 스레드에 20명 이상의 참가자가가 있는 경우 사용할 수 없음*    | ✔️   | ✔️  | ✔️    | ✔️   |  ✔️    | ✔️   |   
|                   | 참가자가 채팅 스레드에서 메시지를 적극적으로 입력할 때 알림 받기 <br/> *채팅 스레드에 20명 이상의 멤버가 있는 경우 사용할 수 없음*      | ✔️   | ✔️   | ✔️    | ✔️    |  ✔️    | ✔️   | 
|                   | 채팅 스레드에서 모든 메시지 가져오기 <br/>                                                                         | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |  
|                   | 메시지 콘텐츠의 일부로 유니코드 이모지 보내기                                                                            | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |    
|실시간 신호(독점적인 신호 패키지에서 사용하도록 설정**)|  채팅 앱에서 들어오는 메시지 및 기타 작업을 실시간으로 업데이트하려면 구독하세요. 실시간 신호에 대해 지원되는 업데이트 목록을 보려면 [채팅 개념](concepts.md#real-time-signaling)을 참조하세요.                                     | ✔️   | ❌    | ❌  | ❌  | ❌  | ❌  |    
| Event Grid 지원             | Azure Event Grid와의 통합을 사용하고 채팅 활동을 기반으로 비즈니스 논리를 실행하거나 사용자 지정 푸시 알림 서비스를 연결하도록 통신 서비스를 구성합니다.   | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |  
| 모니터링        | Azure Portal에서 내 보낸 API 요청 메트릭을 사용하여 대시보드를 빌드하고, 채팅 앱의 상태를 모니터링하고, 비정상적인 상태을 감지하도록 경고를 설정합니다.      | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |    
|                   | 모니터링 및 진단 목적으로 채팅 작업 로그를 받도록 Communication Services 리소스를 구성합니다.          | ✔️   | ✔️  | ✔️    | ✔️  |  ✔️    | ✔️   |  


**독점적인 신호 패키지는 웹 소켓을 사용하여 구현됩니다. 웹 소켓이 지원되지 않으면 긴 폴링으로 대체됩니다.  

## <a name="javascript-chat-client-library-support-by-os-and-browser"></a>OS 및 브라우저별 JavaScript 채팅 클라이언트 라이브러리 지원 

다음 표에서는 현재 사용할 수 있는 지원되는 브라우저 및 버전의 세트를 나타냅니다.
    
|                                  | Windows          | macOS          | Ubuntu | Linux  | Android | iOS    | iPad OS|
|--------------------------------|----------------|--------------|-------|------|------|------|-------|
| **채팅 클라이언트 라이브러리** | Firefox *, Chrome*, 새 Edge | Firefox *, Chrome*, Safari* | Chrome*  | Chrome* | Chrome* | Safari* | Safari* |

*이전 두 릴리스 외에도 최신 버전이 지원됩니다.<br/>   

## <a name="next-steps"></a>다음 단계   

> [!div class="nextstepaction"] 
> [채팅 시작](../../quickstarts/chat/get-started.md)    

다음 문서는 사용자에게 유용할 수 있습니다.  
- [채팅 개념](../chat/concepts.md) 숙지