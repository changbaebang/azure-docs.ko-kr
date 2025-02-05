---
title: 파일 포함
description: 포함 파일
services: container-service
author: mlearned
ms.service: container-service
ms.topic: include
ms.date: 11/22/2019
ms.author: mlearned
ms.custom: include file
ms.openlocfilehash: a42bba1b6524825aa571e4c18319b61b97829792
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96584511"
---
| 리소스 | 제한 |
| --- | :--- |
| 구독당 최대 클러스터 수 | 1000 |
| Virtual Machine Availability Sets 및 기본 Load Balancer SKU를 사용하는 클러스터당 최대 노드 수  | 100 |
| Virtual Machine Scale Sets 및 [표준 Load Balancer SKU][standard-load-balancer]를 사용하는 클러스터당 최대 노드 수 | 1000([노드 풀][node-pool]당 100개 노드) |
| 노드당 최대 Pod 수: Kubenet을 사용하는 [기본 네트워킹][basic-networking] | 110 |
| 노드당 최대 Pod 수: Azure Container Networking Interface를 사용하는 [고급 네트워킹][advanced-networking] | Azure CLI 배포: 30<sup>1</sup><br />Azure Resource Manager 템플릿: 30<sup>1</sup><br />포털 배포: 30 |

<sup>1</sup>Azure CLI 또는 Resource Manager 템플릿을 사용하여 AKS(Azure Kubernetes Service) 클러스터를 배포할 때 이 값은 노드당 최대 250개의 Pod로 구성할 수 있습니다. AKS 클러스터를 이미 배포한 후 또는 Azure Portal을 사용하여 클러스터를 배포하는 경우에는 노드당 최대 Pod 수를 구성할 수 없습니다.<br />

<!-- LINKS - Internal -->
[basic-networking]: ../articles/aks/concepts-network.md#kubenet-basic-networking
[advanced-networking]: ../articles/aks/concepts-network.md#azure-cni-advanced-networking
[standard-load-balancer]: ../articles/load-balancer/load-balancer-overview.md
[node-pool]: ../articles/aks/use-multiple-node-pools.md

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest