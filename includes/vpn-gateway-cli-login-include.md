---
title: 파일 포함
description: 파일 포함
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: 74d7bd087df4b00c0bafb5ec33fbbdfa5c57b379
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92755623"
---
[az login](/cli/azure/) 명령을 사용하여 Azure 구독에 로그인하고 화면의 지시를 따릅니다. 로그인에 대한 자세한 내용은 [Azure CLI 시작](/cli/azure/get-started-with-azure-cli)을 참조하세요.

```azurecli
az login
```

Azure 구독이 두 개 이상인 경우 계정의 구독을 나열합니다.

```azurecli
az account list --all
```

사용할 구독을 지정합니다.

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```
