---
title: 파일 포함
description: 파일 포함
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 12/14/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: f2d2b655e80f5b9694fb1948b136aac918312ca9
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102244480"
---
## <a name="create-a-service-principal"></a>서비스 주체 만들기

컨테이너 레지스트리에 대한 액세스 권한을 사용하여 서비스 주체를 만들려면 [Azure Cloud Shell](../articles/cloud-shell/overview.md)에서 다음 스크립트를 실행하거나 [Azure CLI](/cli/azure/install-azure-cli)를 로컬로 설치합니다. 스크립트는 Bash 셸에 대해 서식이 지정됩니다.

스크립트를 실행하기 전에 `ACR_NAME` 변수를 컨테이너 레지스트리 이름으로 업데이트합니다. `SERVICE_PRINCIPAL_NAME` 값은 Azure Active Directory 테넌트 내에서 고유해야 합니다. "`'http://acr-service-principal' already exists.`" 오류를 수신하는 경우 서비스 주체에 다른 이름을 지정합니다.

다른 사용 권한을 부여하려는 경우 필요에 따라 [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] 명령에서 `--role` 값을 수정할 수 있습니다. 역할의 전체 목록은 [ACR 역할 및 권한](https://github.com/Azure/acr/blob/master/docs/roles-and-permissions.md)을 참조하세요.

스크립트를 실행한 후 서비스 주체의 **ID** 와 **암호** 를 기록해 둡니다. 자격 증명이 있으면 컨테이너 레지스트리를 서비스 주체로 인증하도록 애플리케이션과 서비스를 구성할 수 있습니다.

<!-- https://github.com/Azure-Samples/azure-cli-samples/blob/master/container-registry/service-principal-create/service-principal-create.sh -->
[!code-azurecli-interactive[acr-sp-create](~/cli_scripts/container-registry/service-principal-create/service-principal-create.sh)]

### <a name="use-an-existing-service-principal"></a>기존 서비스 주체 사용

기존 서비스 주체에 레지스트리 액세스 권한을 부여하려면 서비스 주체에 새 역할을 할당해야 합니다. 새 서비스 주체를 만들 때처럼 풀, 푸시 및 풀, 소유자 액세스 권한을 부여할 수 있습니다.

다음 스크립트는  변수에 지정한 서비스 주체에게 [az role assignment create`SERVICE_PRINCIPAL_ID`][az-role-assignment-create] 명령을 사용하여 *풀* 권한을 부여합니다. 다른 수준의 액세스 권한을 부여하려면 `--role` 값을 조정합니다.


<!-- https://github.com/Azure-Samples/azure-cli-samples/blob/master/container-registry/service-principal-assign-role/service-principal-assign-role.sh -->
[!code-azurecli-interactive[acr-sp-role-assign](~/cli_scripts/container-registry/service-principal-assign-role/service-principal-assign-role.sh)]

<!-- LINKS - Internal -->
[az-ad-sp-create-for-rbac]: /cli/azure/ad/sp#az-ad-sp-create-for-rbac
[az-role-assignment-create]: /cli/azure/role/assignment#az-role-assignment-create
