---
title: Azure Communication Services 통화 클라이언트 라이브러리 개요
titleSuffix: An Azure Communication Services concept document
description: 통화 클라이언트 라이브러리에 대한 개요를 제공합니다.
author: mikben
manager: jken
services: azure-communication-services
ms.author: mikben
ms.date: 03/10/2021
ms.topic: overview
ms.service: azure-communication-services
ms.openlocfilehash: e154e43f9e9378d6cccd23e2e5892f2a8ccf9a1e
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104598884"
---
# <a name="calling-client-library-overview"></a>통화 클라이언트 라이브러리 개요

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]


*클라이언트* 및 *서비스* 에 대한 두 가지 별도의 통화 클라이언트 라이브러리 제품군이 있습니다. 현재 사용할 수 있는 클라이언트 라이브러리는 최종 사용자 환경(웹 사이트 및 네이티브 앱)을 위한 것입니다.

서비스 클라이언트 라이브러리는 아직 사용할 수 없으며, 봇 및 기타 서비스와의 통합에 적합한 원시 음성 및 비디오 데이터 평면에 대한 액세스를 제공합니다.

## <a name="calling-client-library-capabilities"></a>통화 클라이언트 라이브러리 기능

다음 목록에서는 현재 Azure Communication Services 통화 클라이언트 라이브러리에서 사용할 수 있는 기능 세트를 보여 줍니다.

| 기능 그룹 | 기능                                                                                                          | JS  | Java(Android) | Objective-C(iOS)
| ----------------- | ------------------------------------------------------------------------------------------------------------------- | ---  | -------------- | -------------
| 핵심 기능 | 두 사용자 간에 일 대 일 호출 배치                                                                           | ✔️   | ✔️            | ✔️
|                   | 세 명 이상의 사용자를 포함하는 그룹 통화(최대 350 사용자) 배치                                                       | ✔️   | ✔️            | ✔️
|                   | 세 명 이상의 사용자가 있는 그룹 호출로 일 대 일 호출 승격                                 | ✔️   | ✔️            | ✔️
|                   | 시작된 후 그룹 호출 조인                                                                              | ✔️   | ✔️            | ✔️
|                   | 진행 중인 그룹 호출에 참가하기 위해 다른 VoIP 참가자 초대                                                       | ✔️   | ✔️            | ✔️
|  중간 호출 컨트롤 | 비디오 켜기/끄기                                                                                              | ✔️   | ✔️            | ✔️ 
|                   | 마이크 음소거/음소거 해제                                                                                                     | ✔️   | ✔️            | ✔️         
|                   | 카메라 간 전환                                                                                              | ✔️   | ✔️            | ✔️           
|                   | 로컬 보류/유지 취소                                                                                                  | ✔️   | ✔️            | ✔️           
|                   | 활성 스피커                                                                                                      | ✔️   | ✔️            | ✔️           
|                   | 호출용 스피커 선택                                                                                            | ✔️   | ✔️            | ✔️           
|                   | 통화에 대한 마이크 선택                                                                                         | ✔️   | ✔️            | ✔️           
|                   | 참가자의 상태 표시<br/>*유휴, 초기 미디어, 연결, 연결됨, 보류 중, 로비 내, 연결 끊김*         | ✔️   | ✔️            | ✔️           
|                   | 호출 상태 표시<br/>*초기 미디어, 수신, 연결 중, 울림, 연결됨, 보류 중, 연결 끊기, 연결 끊어짐* | ✔️   | ✔️            | ✔️           
|                   | 참가자가 음소거되어 있는지 여부 표시                                                                                      | ✔️   | ✔️            | ✔️           
|                   | 참가자가 전화를 끊은 이유 표시                                                                       | ✔️   | ✔️            | ✔️     
| 화면 공유    | 애플리케이션 내에서 전체 화면 공유                                                                 | ✔️   | ❌            | ❌           
|                   | 특정 애플리케이션 공유(실행 중인 애플리케이션 목록에서)                                                | ✔️   | ❌            | ❌           
|                   | 열려 있는 탭 목록에서 웹 브라우저 탭 공유                                                                  | ✔️   | ❌            | ❌           
|                   | 참가자가 원격 화면 공유를 볼 수 있음                                                                            | ✔️   | ✔️            | ✔️         
| 명단            | 참가자 리스트                                                                                                   | ✔️   | ✔️            | ✔️           
|                   | 참가자 제거                                                                                                | ✔️   | ✔️            | ✔️         
| PSTN              | PSTN 참가자를 사용하여 일 대 일 호출 배치                                                                     | ✔️   | ✔️            | ✔️   
|                   | PSTN 참가자를 사용하여 그룹 호출 배치                                                                           | ✔️   | ✔️            | ✔️
|                   | PSTN 참가자를 사용하여 일 대 일 호출을 그룹 호출로 승격                                                 | ✔️   | ✔️            | ✔️
|                   | 그룹 호출에서 PSTN 참가자로 전화 걸기                                                                    | ✔️   | ✔️            | ✔️   
| 일반           | 오디오 테스트 서비스를 사용하여 마이크, 스피커 및 카메라 테스트(8:echo123을 호출하여 사용 가능)                   | ✔️   | ✔️            | ✔️ 
| 디바이스 관리 | 오디오 및/또는 비디오 사용 권한 요청                                                                       | ✔️   | ✔️            | ✔️
|                   | 카메라 목록 가져오기                                                                                                     | ✔️   | ✔️            | ✔️ 
|                   | 카메라 설정                                                                                                          | ✔️   | ✔️            | ✔️
|                   | 선택한 카메라 가져오기                                                                                                 | ✔️   | ✔️            | ✔️
|                   | 마이크 목록 가져오기                                                                                                 | ✔️   | ✔️            | ✔️
|                   | 마이크 설정                                                                                                      | ✔️   | ✔️            | ✔️
|                   | 선택한 마이크 가져오기                                                                                             | ✔️   | ✔️            | ✔️
|                   | 스피커 목록 가져오기                                                                                                   | ✔️   | ✔️            | ✔️
|                   | 스피커 설정                                                                                                         | ✔️   | ✔️            | ✔️
|                   | 선택한 스피커 가져오기                                                                                                | ✔️   | ✔️            | ✔️
| 비디오 렌더링   | 여러 위치에서 단일 비디오 렌더링(로컬 카메라 또는 원격 스트림)                                                  | ✔️   | ✔️            | ✔️
|                   | 크기 조정 모드 설정/업데이트                                                                                           | ✔️   | ✔️            | ✔️ 
|                   | 원격 비디오 스트림 렌더링                                                                                          | ✔️   | ✔️            | ✔️



## <a name="javascript-calling-client-library-support-by-os-and-browser"></a>OS 및 브라우저별 JavaScript 호출 클라이언트 라이브러리 지원

다음 표에서는 현재 사용 가능한 지원되는 브라우저 세트를 나타냅니다. 달리 명시하지 않는 한 가장 최근의 세 가지 버전의 브라우저가 지원됩니다.

|                                  | Chrome | Safari*  | Edge(Chromium) | 
| -------------------------------- | -------| ------  | --------------  |
| Android                          |  ✔️    | ❌     | ❌             |
| iOS                              |  ❌    | ✔️**** | ❌             |
| macOS***                         |  ✔️    | ✔️**   | ❌             |
| Windows***                       |  ✔️    | ❌     | ✔️             |
| Ubuntu/Linux                     |  ✔️    | ❌     | ❌             |

*Safari 버전 13.1 이상이 지원됩니다. 1:1 호출은 Safari에서 지원되지 않습니다. 

**발신 비디오 지원에 Safari 14+/macOS 11+가 필요합니다. 

***발신 화면 공유는 브라우저 버전에 관계없이 데스크톱 플랫폼(Windows, macOS 및 Linux)에서만 지원되며 모바일 플랫폼(Android, iOS, iPad 및 태블릿)에서는 지원되지 않습니다.

****Safari의 iOS 앱은 마이크 및 스피커 디바이스(예: Bluetooth)를 열거/선택할 수 없습니다. 이는 OS의 제한 사항이며 항상 하나의 디바이스만 있습니다.


## <a name="calling-client---browser-security-model"></a>클라이언트 - 브라우저 보안 모델 호출

### <a name="user-webrtc-over-https"></a>HTTPS를 통한 사용자 WebRTC

`getUserMedia`와 같은 WebRTC API에서는 이러한 API를 호출하는 앱이 HTTPS를 통해 제공되어야 합니다.

로컬 개발의 경우 `http://localhost`를 사용할 수 있습니다.

### <a name="embed-the-communication-services-calling-sdk-in-an-iframe"></a>Communication Service 호출 SDK를 iframe에 포함

다양한 브라우저에서 새 [권한 정책(기능 정책이라고도 함)](https://www.w3.org/TR/permissions-policy-1/#iframe-allow-attribute)을 채택하고 있습니다. 이 정책은 애플리케이션이 원본 간 iframe 요소를 통해 디바이스의 카메라 및 마이크에 액세스할 수 있는 방법을 제어하여 호출 시나리오에 영향을 줍니다.

Iframe을 사용하여 다른 도메인에서 앱의 일부를 호스팅하려면 iframe에 올바른 값이 포함된 `allow` 특성을 추가해야 합니다.

예를 들어 이 iframe은 카메라와 마이크 액세스를 모두 허용합니다.

```html
<iframe allow="camera *; microphone *">
```

## <a name="calling-client-library-streaming-support"></a>통화 클라이언트 라이브러리 스트리밍 지원
Communication Services 통화 클라이언트 라이브러리는 다음과 같은 스트리밍 구성을 지원합니다.

|           |웹 | Android/iOS|
|-----------|----|------------|
|**# 동시에 보낼 수 있는 나가는 스트림 수** |비디오 1개 또는 화면 공유 1개 | 비디오 1개 + 화면 공유 1개|
|**# 동시에 렌더링할 수 있는 들어오는 스트림 수** |비디오 1개 또는 화면 공유 1개| 비디오 6개 + 화면 공유 1개 |


## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [통화 시작](../../quickstarts/voice-video-calling/getting-started-with-calling.md)

자세한 내용은 다음 항목을 참조하세요.
- 일반적인 [통화 흐름](../call-flows.md) 숙지
- [통화 형식](../voice-video-calling/about-call-types.md)에 대한 자세한 정보
- [PSTN 솔루션 계획](../telephony-sms/plan-solution.md)
