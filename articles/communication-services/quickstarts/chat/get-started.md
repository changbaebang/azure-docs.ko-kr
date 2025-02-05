---
title: 빠른 시작 - 앱에 채팅 추가
titleSuffix: An Azure Communication Services quickstart
description: 이 빠른 시작에서는 앱에 Communication Services 채팅을 추가하는 방법을 보여줍니다.
author: fanche
manager: phans
services: azure-communication-services
ms.author: mikben
ms.date: 03/10/2021
ms.topic: quickstart
ms.service: azure-communication-services
zone_pivot_groups: acs-js-csharp-java-python-swift-android
ms.openlocfilehash: a62c25aa5fd9d25b7330dde89c8544e79785b9d0
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "103495454"
---
# <a name="quickstart-add-chat-to-your-app"></a>빠른 시작: 앱에 채팅 추가

[!INCLUDE [Public Preview Notice](../../includes/public-preview-include.md)]


Communication Services Chat 클라이언트 라이브러리를 사용하여 애플리케이션에 실시간 채팅을 추가하여 Azure Communication Services를 시작하세요. 이 빠른 시작에서는 채팅 클라이언트 라이브러리를 사용하여 사용자가 서로 대화할 수 있는 채팅 스레드를 만듭니다. 채팅 개념에 대해 자세히 알아보려면 [채팅 개념 설명서](../../concepts/chat/concepts.md)를 참조하세요.

::: zone pivot="programming-language-javascript"
[!INCLUDE [Chat with JavaScript client library](./includes/chat-js.md)]
::: zone-end

::: zone pivot="programming-language-python"
[!INCLUDE [Chat with Python client library](./includes/chat-python.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Chat with Java client library](./includes/chat-java.md)]
::: zone-end

::: zone pivot="programming-language-android"
[!INCLUDE [Chat with Android client library](./includes/chat-android.md)]
::: zone-end

::: zone pivot="programming-language-csharp"
[!INCLUDE [Chat with C# client library](./includes/chat-csharp.md)]
::: zone-end

::: zone pivot="programming-language-swift"
[!INCLUDE [Chat with iOS client library](./includes/chat-swift.md)]
::: zone-end

## <a name="clean-up-resources"></a>리소스 정리

Communication Services 구독을 정리하고 제거하려면 리소스 또는 리소스 그룹을 삭제하면 됩니다. 리소스 그룹을 삭제하면 해당 리소스 그룹에 연결된 다른 모든 리소스가 함께 삭제됩니다. [리소스 정리](../create-communication-resource.md#clean-up-resources)에 대해 자세히 알아보세요.

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서는 다음을 수행하는 방법을 알아보았습니다.

> [!div class="checklist"]
> * 채팅 클라이언트 만들기
> * 두 명의 사용자가 있는 스레드 만들기
> * 스레드에 메시지 보내기
> * 스레드에서 메시지 받기
> * 스레드에서 사용자 제거

> [!div class="nextstepaction"]
> [채팅 영웅 앱 사용해 보기](../../samples/chat-hero-sample.md)

다음을 수행할 수도 있습니다.

 - [채팅 개념](../../concepts/chat/concepts.md)에 대한 자세한 정보
 - [채팅 클라이언트 라이브러리](../../concepts/chat/sdk-features.md) 숙지
