---
title: Azure PowerShell 스크립트 샘플 - 리소스 그룹 구독 | Microsoft Docs
description: 이 문서에서는 리소스 그룹에 대한 Event Grid 이벤트를 구독하는 방법을 보여주는 샘플 Azure PowerShell 스크립트를 제공합니다.
ms.devlang: powershell
ms.topic: sample
ms.date: 07/08/2020
ms.openlocfilehash: c8e84fe12cf239e7dbb0e6a15088efda793ddec9
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "87460748"
---
# <a name="subscribe-to-events-for-a-resource-group-with-powershell"></a>PowerShell을 사용하여 리소스 그룹에 대한 이벤트 구독

이 스크립트는 리소스 그룹에 대한 이벤트에 대한 Event Grid 구독을 만듭니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

미리 보기 샘플 스크립트에는 Event Grid 모듈이 필요합니다. 설치하려면 `Install-Module -Name AzureRM.EventGrid -AllowPrerelease -Force -Repository PSGallery`를 실행합니다.

## <a name="sample-script---stable"></a>샘플 스크립트 - 안정적

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

[!code-powershell[main](../../../powershell_scripts/event-grid/subscribe-to-resource-group/subscribe-to-resource-group.ps1 "Subscribe to resource group")]

## <a name="sample-script---preview-module"></a>샘플 스크립트 - 미리 보기 모듈

[!INCLUDE [requires-azurerm](../../../includes/requires-azurerm.md)]

[!code-powershell[main](../../../powershell_scripts/event-grid/subscribe-to-resource-group-preview/subscribe-to-resource-group-preview.ps1 "Subscribe to resource group")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 이벤트 구독을 만듭니다. 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [New-AzEventGridSubscription](/powershell/module/az.eventgrid/new-azeventgridsubscription) | Event Grid 구독을 만듭니다. |

## <a name="next-steps"></a>다음 단계

* 관리되는 애플리케이션에 대한 소개는 [Azure Managed Application 개요](../overview.md)를 참조하세요.
* PowerShell에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/get-started-azureps)를 참조하세요.
