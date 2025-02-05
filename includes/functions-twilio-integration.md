---
author: ggailey777
ms.service: azure-functions
ms.topic: include
ms.date: 09/04/2018
ms.author: glenga
ms.openlocfilehash: b4a1891eadf2e36bcb94b9f605d91f227fa83a3f
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96026079"
---
이 샘플에서는 [Twilio](https://www.twilio.com/) 서비스를 사용하여 SMS 메시지를 휴대폰으로 보냅니다. Azure Functions는 이미 [Twilio 바인딩](../articles/azure-functions/functions-bindings-twilio.md)을 통해 Twilio를 지원하며, 샘플에서 이 기능을 사용합니다.

가장 먼저 필요한 것은 Twilio 계정입니다. https://www.twilio.com/try-twilio에서 무료로 만들 수 있습니다. 계정이 있으면 다음 세 가지 **앱 설정** 을 함수 앱에 추가합니다.

| 앱 설정 이름 | 값 설명 |
| - | - |
| **TwilioAccountSid**  | Twilio 계정의 SID |
| **TwilioAuthToken**   | Twilio 계정의 인증 토큰 |
| **TwilioPhoneNumber** | Twilio 계정과 연결되는 전화 번호이며, SMS 메시지를 보내는 데 사용됩니다. |