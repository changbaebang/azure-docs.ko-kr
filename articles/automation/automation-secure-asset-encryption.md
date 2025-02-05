---
title: Azure Automation의 보안 자산 암호화
description: 이 문서에서는 암호화를 사용하도록 Automation 계정을 구성하는 개념을 제공합니다.
services: automation
ms.service: automation
ms.subservice: process-automation
author: snehithm
ms.author: snmuvva
ms.date: 01/11/2020
ms.topic: conceptual
manager: kmadnani
ms.openlocfilehash: b46cf3a742158a3347b43a1e9bc6d62d0b2160d4
ms.sourcegitcommit: 2c1b93301174fccea00798df08e08872f53f669c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104773694"
---
# <a name="encryption-of-secure-assets-in-azure-automation"></a>Azure Automation의 보안 자산 암호화

Azure Automation의 안전한 자산에는 자격 증명, 인증서, 연결, 암호화된 변수 등이 있습니다. 이러한 자산은 여러 수준의 암호화를 사용하여 Azure Automation에서 보호됩니다. 암호화에 사용되는 최상위 키에 따라 암호화에는 두 가지 모델이 있습니다.

- Microsoft 관리형 키 사용
- 관리하는 키 사용

## <a name="microsoft-managed-keys"></a>Microsoft 관리형 키

기본적으로 Azure Automation 계정은 Microsoft 관리형 키를 사용합니다.

각 보안 자산은 각 Automation 계정에 대해 생성되는 고유 키(데이터 암호화 키)를 사용하여 암호화되고 Azure Automation에 저장됩니다. 이러한 키 자체는 AEK(계정 암호화 키)라고 하는 각 계정에 대해 생성된 다른 고유 키를 사용하여 Azure Automation에서 암호화되고 저장됩니다. 이러한 계정 암호화 키는 Microsoft 관리형 키를 사용하여 Azure Automation에서 암호화되고 저장됩니다. 

## <a name="keys-that-you-manage-with-key-vault-preview"></a>Key Vault를 사용하여 관리하는 키(미리 보기)

사용자 고유의 키를 사용하여 Automation 계정에 대한 보안 자산의 암호화를 관리할 수 있습니다. Automation 계정 수준에서 고객 관리형 키를 지정하는 경우 이 키는 Automation 계정의 계정 암호화 키에 대한 액세스를 보호하고 제어하는 데 사용됩니다. 그런 후 모든 보안 자산을 암호화하고 암호를 해독하는 데 사용됩니다. 고객 관리형 키를 사용하면 훨씬 더 유연하게 액세스 제어를 만들고, 순환하고, 사용하지 않도록 설정하고, 철회할 수 있습니다. 보안 자산을 보호하는 데 사용되는 암호화 키를 감사할 수도 있습니다.

Azure Key Vault를 사용하여 고객 관리형 키를 저장 합니다. 사용자 고유의 키를 만들어 키 자격 증명 모음에 저장할 수도 있고, Azure Key Vault API를 사용하여 키를 생성할 수도 있습니다.  Azure Key Vault에 대한 자세한 내용은 [Azure Key Vault란?](../key-vault/general/overview.md)

## <a name="use-of-customer-managed-keys-for-an-automation-account"></a>Automation 계정에 대해 고객 관리형 키 사용

Automation 계정에 대해 고객 관리형 키를 사용하여 암호화를 사용하는 경우 Azure Automation은 연결된 Key Vault에서 고객 관리형 키를 사용하여 계정 암호화 키를 래핑합니다. 고객 관리형 키를 사용하도록 설정해도 성능에 영향을 주지 않으며, 계정이 지연 없이 새 키로 즉시 암호화됩니다.

새 Automation 계정은 항상 Microsoft 관리형 키를 사용하여 암호화됩니다. 계정을 만들 때는 고객 관리형 키를 사용하도록 설정할 수 없습니다. 고객 관리형 키는 Azure Key Vault에 저장되며, Key Vault는 Automation 계정과 연결된 관리 ID에 대한 키 권한을 부여하는 액세스 정책을 사용하여 프로비저닝되어야 합니다. 관리 ID는 스토리지 계정이 만들어진 후에만 사용할 수 있습니다.

Azure Automation 보안 자산 암호화에 사용되는 키를 수정할 때 고객 관리 키를 사용하거나 사용하지 않도록 설정하거나, 키 버전을 업데이트하거나, 다른 키를 지정하여 계정 암호화 키의 암호화가 변경되지만 Azure Automation 계정의 보안 자산은 다시 암호화할 필요가 없습니다.

> [!NOTE] 
> 고객 관리형 키를 사용하도록 설정하려면 API 버전 2020-01-13-preview를 사용하여 Azure Automation REST API를 호출해야 합니다.

### <a name="prerequisites-for-using-customer-managed-keys-in-azure-automation"></a>Azure Automation에서 고객 관리형 키를 사용하기 위한 필수 조건

Automation 계정에 대해 고객 관리형 키를 사용하도록 설정하기 전에 다음 필수 조건이 충족되는지 확인해야 합니다.

 - 고객 관리형 키가 Azure Key Vault에 저장됩니다. 
 - Key Vault에서 **일시 삭제** 및 **제거 안 함** 속성을 둘 다 사용하도록 설정합니다. 이러한 기능은 실수로 삭제하는 경우 키 복구를 허용하는 데 필요합니다.
 - Azure Automation 암호화에서는 RSA 키만 지원됩니다. 키에 대한 자세한 내용은 [Azure Key Vault 키, 비밀 및 인증서 정보](../key-vault/general/about-keys-secrets-certificates.md)를 참조하세요.
- Automation 계정과 Key Vault는 서로 다른 구독에 있을 수 있지만 동일한 Azure Active Directory 테넌트에 있어야 합니다.

### <a name="assignment-of-an-identity-to-the-automation-account"></a>Automation 계정에 ID 할당

Automation 계정에서 고객 관리형 키를 사용하려면 Automation 계정이 고객 관리형 키를 저장하는 Key Vault에 대해 인증을 받아야 합니다. Azure Automation은 시스템 할당 관리 ID를 사용하여 Azure Key Vault 계정을 인증합니다. 관리 ID에 대한 자세한 내용은 [Azure 리소스용 관리 ID란?](../active-directory/managed-identities-azure-resources/overview.md)을 참조하세요.

다음 REST API 호출을 사용하여 시스템 할당 관리 ID를 Automation 계정으로 구성합니다.

```http
PATCH https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resource-group-name/providers/Microsoft.Automation/automationAccounts/automation-account-name?api-version=2020-01-13-preview
```

본문 요청:

```json
{ 
 "identity": 
 { 
  "type": "SystemAssigned" 
  } 
}
```

Automation 계정에 대한 시스템 할당 ID는 다음과 비슷한 응답으로 반환됩니다.

```json
{
 "name": "automation-account-name",
 "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resource-group-name/providers/Microsoft.Automation/automationAccounts/automation-account-name",
 ..
 "identity": {
    "type": "SystemAssigned",
    "principalId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
    "tenantId": "bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb"
 },
..
}
```

### <a name="configuration-of-the-key-vault-access-policy"></a>Key Vault 액세스 정책 구성

관리 ID가 Automation 계정에 할당되면 고객 관리형 키를 저장하는 Key Vault에 대한 액세스를 구성합니다. Azure Automation를 사용하려면 고객 관리형 키에 대해 **get**, **recover**, **wrapKey**, **UnwrapKey** 가 필요합니다.

이러한 액세스 정책은 다음 REST API 호출을 사용하여 설정할 수 있습니다.

```http
PUT https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/sample-group/providers/Microsoft.KeyVault/vaults/sample-vault/accessPolicies/add?api-version=2018-02-14
```

본문 요청:

```json
{
  "properties": {
    "accessPolicies": [
      {
        "tenantId": "bbbbbbbb-bbbb-bbbb-bbbb-bbbbbbbbbbbb",
        "objectId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
        "permissions": {
          "keys": [
            "get",
            "recover",
            "wrapKey",
            "unwrapKey"
          ],
          "secrets": [],
          "certificates": []
        }
      }
    ]
  }
}
```

> [!NOTE]
> **tenantId** 및 **objectId** 필드는 Automation 계정의 관리 ID 응답에서 각각 **identity.tenantId** 및 **identity.principalId** 값과 함께 제공되어야 합니다.

### <a name="change-the-configuration-of-automation-account-to-use-customer-managed-key"></a>고객 관리형 키를 사용하도록 Automation 계정 구성 변경

마지막으로 다음 REST API 호출을 사용하여 자동화 계정을 Microsoft 관리형 키에서 고객 관리형 키로 전환할 수 있습니다.

```http
PATCH https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resource-group-name/providers/Microsoft.Automation/automationAccounts/automation-account-name?api-version=2020-01-13-preview
```

본문 요청:

```json
{
    "identity": {
    "type": "SystemAssigned"
    },
    "properties": {
        "encryption": {
            "keySource": "Microsoft.Keyvault",
            "keyvaultProperties": {
                "keyName": "sample-vault-key",
                "keyvaultUri": "https://sample-vault-key12.vault.azure.net",
                "keyVersion": "7c73556c521340209371eaf623cc099d"
            }
        }
    }
}
```

샘플 응답

```json
{
  "name": "automation-account-name",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resource-group-name/providers/Microsoft.Automation/automationAccounts/automation-account-name",
  ..
  "properties": {
    ..
    "encryption": {
      "keyvaultProperties": {
         "keyName": "sample-vault-key",
          "keyvaultUri": "https://sample-vault-key12.vault.azure.net",
          "keyVersion": "7c73556c521340209371eaf623cc099d"
      },
      "keySource": "Microsoft.Keyvault"
    },
    ..
  }
}
```

## <a name="rotation-of-a-customer-managed-key"></a>고객 관리형 키 순환

규정 준수 정책에 따라 Azure Key Vault에서 고객 관리형 키를 순환할 수 있습니다. 키를 순환하는 경우 새 키 URI를 사용하도록 Automation 계정을 업데이트해야 합니다.

키를 순환해도 Automation 계정에서 보안 자산의 재암호화가 트리거되지 않습니다. 추가 작업은 필요하지 않습니다.

## <a name="revocation-of-access-to-a-customer-managed-key"></a>고객 관리형 키에 대한 액세스 해지

고객 관리형 키에 대한 액세스를 취소하려면 PowerShell 또는 Azure CLI를 사용합니다. 자세한 내용은 [Azure Key Vault PowerShell](/powershell/module/az.keyvault/) 또는 [Azure Key Vault CLI](/cli/azure/keyvault)를 참조하세요. 액세스를 취소하면 Azure Automation에서 암호화 키에 액세스할 수 없으므로 Automation 계정의 모든 보안 자산에 대한 액세스가 효과적으로 차단됩니다.

## <a name="next-steps"></a>다음 단계

- Azure Key Vault를 이해하려면 [Azure Key Vault란?](../key-vault/general/overview.md)을 참조하세요.
- 인증서를 사용하려면 [Azure Automation에서 인증서 관리](shared-resources/certificates.md)를 참조하세요.
- 자격 증명을 처리하려면 [Azure Automation에서 자격 증명 관리](shared-resources/credentials.md)를 참조하세요.
- Automation 변수를 사용하려면 [Azure Automation의 변수 관리](shared-resources/variables.md)를 참조하세요.
- 연결 작업에 대한 도움말은 [Azure Automation에서 연결 관리](automation-connections.md)를 참조하세요.
