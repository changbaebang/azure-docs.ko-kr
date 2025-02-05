---
title: Azure Logic Apps에서 Salesforce에 연결
description: Azure Logic Apps를 사용하여 Salesforce 레코드를 모니터링하고 관리하는 작업 및 워크플로 자동화
services: logic-apps
ms.suite: integration
ms.reviewer: klam, logicappspm
ms.topic: article
ms.date: 08/24/2018
tags: connectors
ms.openlocfilehash: 9950951ab5189c8c7b72de78bca9465ec5f22748
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87290596"
---
# <a name="monitor-create-and-manage-salesforce-resources-by-using-azure-logic-apps"></a>Azure Logic Apps를 사용하여 Salesforce 리소스 모니터링, 만들기 및 관리

Azure Logic Apps 및 Salesforce 커넥터를 사용하여 레코드, 작업 및 개체 같은 Salesforce 리소스에 대한 자동화된 작업 및 워크플로를 만들 수 있습니다. 예를 들어:

* 레코드를 만들거나 변경할 때 모니터링합니다. 
* 삽입, 업데이트 및 삭제 작업을 포함하여 작업 및 레코드를 만들고 가져오고 관리합니다.

Salesforce 트리거를 사용하여 Salesforce에서 응답을 가져오고 출력을 다른 작업에 사용하게 할 수 있습니다. 논리 앱에서 작업을 사용하여 Salesforce 리소스로 다양한 작업을 수행할 수 있습니다. 논리 앱을 처음 접하는 경우 [Azure Logic Apps란?](../logic-apps/logic-apps-overview.md)을 검토합니다.

## <a name="prerequisites"></a>사전 요구 사항

* Azure 구독 Azure 구독이 없는 경우 [체험 Azure 계정에 등록](https://azure.microsoft.com/free/)합니다. 

* [Salesforce 계정](https://salesforce.com/)

* [논리 앱 만드는 방법](../logic-apps/quickstart-create-first-logic-app-workflow.md)에 관한 기본 지식

* Salesforce 계정에 액세스하려는 논리 앱입니다. Salesforce 트리거를 시작하려면 [빈 논리 앱을 만듭니다](../logic-apps/quickstart-create-first-logic-app-workflow.md). Salesforce 동작을 사용하려면, 예를 들어 **되풀이** 트리거와 같은 다른 트리거를 통해 논리 앱을 시작합니다.

## <a name="connect-to-salesforce"></a>Salesforce에 연결

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. [Azure Portal](https://portal.azure.com)에 로그인하고, 아직 열리지 않은 경우 Logic App Designer에서 논리 앱을 엽니다.

1. 경로를 선택합니다. 

   * 빈 논리 앱의 경우 검색 상자에서 필터로 "salesforce"를 입력합니다. 
   트리거 목록에서 원하는 트리거를 선택합니다. 

     또는

   * 기존 논리 앱의 경우 작업을 추가하려는 단계에서 **새 단계** 를 선택합니다. 검색 상자에 필터로 "salesforce"를 입력합니다. 작업 목록에서 원하는 작업을 선택합니다.

1. Salesforce에 로그인하라는 메시지가 표시되면 로그인하고 액세스를 허용합니다.

   자격 증명을 통해 Salesforce에 대한 연결을 만들고 데이터에 액세스하는 권한이 논리 앱에 부여됩니다.

1. 선택한 트리거 또는 작업에 대해 필요한 세부 정보를 제공하고 논리 앱의 워크플로를 계속 빌드합니다.

## <a name="connector-reference"></a>커넥터 참조

커넥터의 OpenAPI(이전의 Swagger) 설명서에 설명된 트리거, 작업 및 제한에 대한 기술 정보는 커넥터의 [참조 페이지](/connectors/salesforce/)를 검토하세요.

## <a name="get-support"></a>지원 받기

* 질문이 있는 경우 [Azure Logic Apps에 대한 Microsoft Q&A 질문 페이지](/answers/topics/azure-logic-apps.html)를 방문하세요.
* 기능 아이디어를 제출하거나 투표하려면 [Logic Apps 사용자 의견 사이트](https://aka.ms/logicapps-wish)를 방문하세요.

## <a name="next-steps"></a>다음 단계

* 다른 [Logic Apps 커넥터](../connectors/apis-list.md)에 대해 알아봅니다.
