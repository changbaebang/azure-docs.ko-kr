---
title: 자습서 - Azure App Service에서 안전한 웹앱 빌드 | Azure
description: 이 자습서에서는 Azure App Service를 사용하여 웹앱을 빌드하고, 인증을 사용하도록 설정하고, Azure Storage를 호출하고, Microsoft Graph를 호출하는 방법을 알아봅니다.
services: active-directory, app-service-web, storage, microsoft-graph
author: rwike77
manager: CelesteDG
ms.service: app-service-web
ms.topic: tutorial
ms.workload: identity
ms.date: 11/09/2020
ms.author: ryanwi
ms.reviewer: stsoneff
ms.custom: azureday1
ms.openlocfilehash: 17931ee92072059d94cd950e9ce8ef6588f7e891
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96905505"
---
# <a name="tutorial-enable-authentication-in-app-service-and-access-storage-and-microsoft-graph"></a>자습서: App Service에서 인증을 사용하도록 설정하고 스토리지 및 Microsoft Graph에 액세스

이 자습서에서는 다음을 수행하는 방법을 학습할 수 있는 일반적인 애플리케이션 시나리오를 설명합니다.

- [웹앱에 대한 인증을 구성](scenario-secure-app-authentication-app-service.md)하고 조직의 사용자에 대한 액세스를 제한합니다. 다이어그램에서 A를 참조하세요.
- 관리 ID를 사용하여 웹 애플리케이션용 [Azure Storage에 안전하게 액세스](scenario-secure-app-access-storage.md)합니다. 다이어그램에서 B를 참조하세요.
- 관리 ID를 사용하여 [로그인한 사용자의 경우](scenario-secure-app-access-microsoft-graph-as-user.md) 또는 [웹 애플리케이션의 경우](scenario-secure-app-access-microsoft-graph-as-app.md) Microsoft Graph의 데이터에 액세스합니다. 다이어그램에서 C를 참조하세요.
- 이 자습서를 위해 만든 [리소스를 정리](scenario-secure-app-clean-up-resources.md)합니다.

:::image type="content" source="./media/scenario-secure-app-overview/web-app.svg" alt-text="Microsoft ID 플랫폼의 애플리케이션 시나리오를 보여주는 다이어그램." border="false":::

시작하려면 웹앱에 대한 인증을 사용하도록 설정하는 방법을 알아봅니다.

> [!div class="nextstepaction"]
> [웹앱에 대한 인증 구성](scenario-secure-app-authentication-app-service.md)
