---
title: Azure CLI 스크립트 샘플 - 사용자 지정 항목 구독 | Microsoft Docs
description: 이 문서에서는 사용자 지정 항목에 대한 Event Grid 이벤트를 구독하는 방법을 보여주는 샘플 Azure CLI 스크립트를 제공합니다.
ms.devlang: azurecli
ms.topic: sample
ms.date: 07/08/2020
ms.custom: devx-track-azurecli
ms.openlocfilehash: 80eff2853db1083fa2805cdd719f03a3235fccac
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87499027"
---
# <a name="subscribe-to-events-for-a-custom-topic-with-azure-cli"></a>Azure CLI를 사용하여 사용자 지정 항목에 대한 이벤트 구독

이 스크립트는 사용자 지정 항목에 대한 이벤트에 대한 Event Grid 구독을 만듭니다.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

미리 보기 샘플 스크립트에는 Event Grid 확장이 필요합니다. 설치하려면 `az extension add --name eventgrid`를 실행합니다.

## <a name="sample-script---stable"></a>샘플 스크립트 - 안정적

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-custom-topic/subscribe-to-custom-topic.sh "Subscribe to custom topic")]

## <a name="sample-script---preview-extension"></a>샘플 스크립트 - 미리 보기 확장

[!code-azurecli[main](../../../cli_scripts/event-grid/subscribe-to-custom-topic-preview/subscribe-to-custom-topic-preview.sh "Subscribe to custom topic")]


## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 이벤트 구독을 만듭니다. 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az eventgrid event-subscription create](/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create) | Event Grid 구독을 만듭니다. |
| [az eventgrid event-subscription create](/cli/azure/ext/eventgrid/eventgrid/event-subscription#ext-eventgrid-az-eventgrid-event-subscription-create) - 확장 버전 | Event Grid 구독을 만듭니다. |

## <a name="next-steps"></a>다음 단계

* 구독 쿼리에 대한 정보는 [쿼리 Event Grid 구독](../query-event-subscriptions.md)을 참조하세요.
* Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.
