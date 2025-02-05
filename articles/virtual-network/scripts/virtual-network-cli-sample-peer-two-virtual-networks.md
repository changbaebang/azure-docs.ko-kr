---
title: 두 개 가상 네트워크 피어링 - Azure CLI 스크립트 샘플
description: Azure CLI 스크립트 샘플을 사용하여 Azure 네트워크를 통해 동일한 지역에서 두 가상 네트워크를 만들고 연결합니다.
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: mtillman
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: ''
ms.workload: infrastructure
ms.date: 03/20/2018
ms.author: kumud
ms.custom: devx-track-azurecli
ms.openlocfilehash: 902d6643420ff6bdafcf52278f3a1c0df28647ae
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98217539"
---
# <a name="peer-two-virtual-networks-with-an-azure-cli-script-sample"></a>Azure CLI 스크립트 샘플로 두 개의 가상 네트워크 피어링

이 스크립트 샘플은 Azure 네트워크를 통해 동일한 지역에서 두 가상 네트워크를 만들고 연결합니다. 스크립트를 실행한 후에는 두 개의 가상 네트워크 간에 피어링이 설정됩니다.

Azure [Cloud Shell](https://shell.azure.com/bash) 또는 로컬 Azure CLI 설치에서 스크립트를 실행할 수 있습니다. CLI를 로컬로 사용하는 경우 이 스크립트는 2.0.28 이상 버전을 실행해야 합니다. 설치되어 있는 버전을 확인하려면 `az --version`을 실행합니다. 설치 또는 업그레이드가 필요한 경우, [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요. 또한 CLI를 로컬로 실행하는 경우 `az login`를 실행하여 Azure와 연결해야 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a>배포 정리 

다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트는 다음 명령을 사용하여 리소스 그룹, 가상 컴퓨터 및 모든 관련된 리소스를 만듭니다. 다음 표에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.

| 명령 | 메모 |
|---|---|
| [az group create](/cli/azure/group) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az network vnet create](/cli/azure/network/vnet) | Azure Virtual Network 및 서브넷을 만듭니다. |
| [az network vnet peering create](/cli/azure/network/vnet/peering) | 두 가상 네트워크 간에 피어링을 만듭니다.  |
| [az group delete](/cli/azure/vm/extension) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure)를 참조하세요.

추가 가상 네트워크 CLI 스크립트 샘플은 [가상 네트워크 CLI 샘플](../cli-samples.md)에 나와 있습니다.