---
title: 파일 포함
description: 포함 파일
services: functions
author: craigshoemaker
manager: gwallace
ms.service: azure-functions
ms.topic: include
ms.date: 01/28/2020
ms.author: cshoe
ms.custom: include file
ms.openlocfilehash: bcc55156ca1d03614a4ff9767d6cf3f2603c06ca
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96025735"
---
다음 방법을 사용하여 선호하는 개발 환경에 지원을 추가합니다.

| 개발 환경  | 애플리케이션 종류      | 지원을 추가하려면 다음을 수행합니다. |
|--------------------------|-----------------------|----------------|
| Visual Studio            | C# 클래스 라이브러리      | [NuGet 패키지 설치](../articles/azure-functions/functions-bindings-register.md#vs) |
| Visual Studio Code       | [핵심 도구](../articles/azure-functions/functions-run-local.md) 기반 | [확장 번들 등록](../articles/azure-functions/functions-bindings-register.md#extension-bundles)<br><br>[Azure Tools 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)을 설치하는 것이 좋습니다. |
| 다른 모든 편집기/IDE     | [핵심 도구](../articles/azure-functions/functions-run-local.md) 기반 | [확장 번들 등록](../articles/azure-functions/functions-bindings-register.md#extension-bundles) |
| Azure Portal             | 포털에서만 온라인 사용 | 바인딩 추가 시 설치<br /><br /> 함수 앱을 다시 게시하지 않고 기존 바인딩 확장을 업데이트하려면 [확장 업데이트](../articles/azure-functions/functions-bindings-register.md)를 참조하세요. |