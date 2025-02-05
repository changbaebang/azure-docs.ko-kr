---
title: 자습서 - PowerShell을 사용하여 기존 가상 네트워크에 배포 - Azure Dedicated HSM | Microsoft Docs
description: PowerShell을 사용하여 전용 HSM을 기존 가상 네트워크에 배포하는 방법을 보여 주는 자습서입니다.
services: dedicated-hsm
documentationcenter: na
author: msmbaldwin
manager: rkarlin
editor: ''
ms.service: key-vault
ms.topic: tutorial
ms.custom: mvc, seodec18, devx-track-azurepowershell
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2020
ms.author: mbaldwin
ms.openlocfilehash: 52b62e463edc51b3d93d7af69623a88abd9cc6be
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98108605"
---
# <a name="tutorial--deploying-hsms-into-an-existing-virtual-network-using-powershell"></a>자습서 - PowerShell을 사용하여 기존 가상 네트워크에 HSM 배포

Azure Dedicated HSM 서비스는 단일 고객이 사용할 수 있는 완전한 관리 컨트롤과 전체적인 관리 기능을 지원하는 물리적 디바이스를 제공합니다. 물리적 하드웨어를 제공하기 때문에 Microsoft에서 효율적인 용량 관리를 위해 이러한 디바이스의 할당 방식을 제어해야 합니다. 따라서 Azure 구독 내에서 Dedicated HSM 서비스는 일반적으로 리소스 프로비전에 표시되지 않습니다. Dedicated HSM 서비스에 액세스해야 하는 Azure 고객은 먼저 Microsoft 계정 담당자에게 연락하여 Dedicated HSM 서비스에 대한 등록을 요청해야 합니다. 이 프로세스가 성공적으로 완료되어야만 프로비전이 가능해집니다.
이 자습서에서는 다음과 같은 일반적인 프로비전 프로세스를 보여줍니다.

- 고객에게 이미 가상 네트워크가 있음
- 가상 머신이 있음
- 기존 환경에 HSM 리소스를 추가해야 합니다.

일반적인 고가용성의 다중 지역 배포 아키텍처는 다음과 유사합니다.

![다중 지역 배포](media/tutorial-deploy-hsm-powershell/high-availability.png)

이 자습서에서는 기존의 가상 네트워크(위의 VNET 1 참조)로 통합되는 HSM과 필요한 ExpressRoute 게이트웨이(위의 Subnet 1 참조)의 쌍을 중점적으로 살펴봅니다.  다른 모든 리소스는 표준 Azure 리소스입니다. 위의 VNET 3에서 서브넷 4에 있는 HSM에 동일한 통합 프로세스를 사용할 수 있습니다.


[!INCLUDE [updated-for-az](../../includes/updated-for-az.md)]

## <a name="prerequisites"></a>사전 요구 사항

Azure Dedicated HSM은 현재 Azure Portal에서 사용할 수 없으므로 이 서비스와의 모든 상호 작용은 명령줄 또는 PowerShell을 통해 이루어집니다. 이 자습서에서는 Azure Cloud Shell에서 PowerShell을 사용합니다. PowerShell을 처음 사용하는 경우 [Azure PowerShell 시작](/powershell/azure/get-started-azureps)에 있는 시작 지침을 따릅니다.

가정:

- Azure Dedicated HSM 등록 프로세스를 거쳤고 서비스 사용 승인을 받았습니다. 이에 해당되지 않을 경우 Microsoft 계정 담당자에게 자세한 내용을 문의하세요. 
- 이러한 리소스에 대한 리소스 그룹을 만들었으며, 이 자습서에서 배포된 새 리소스가 해당 그룹에 가입됩니다.
- 위의 다이어그램에 따라 필요한 가상 네트워크, 서브넷, 가상 머신을 이미 만들었으며, 이제 해당 배포판에 2개의 HSM을 통합하려고 합니다.

아래의 모든 지침에서는 이미 Azure Portal로 이동했고 Cloud Shell(포털 오른쪽 위에서 “\>\_” 선택)을 열었다고 가정합니다.

## <a name="provisioning-a-dedicated-hsm"></a>Dedicated HSM 프로비전

HSM을 프로비저닝하고 ExpressRoute 게이트웨이를 통해 기존의 가상 네트워크에 통합한 후에는 ssh 명령줄 도구를 통해 유효성 검사를 수행하여 HSM 디바이스의 연결 가능성과 기본 가용성을 확인해야 합니다. 다음 명령은 Resource Manager 템플릿을 사용하여 HSM 리소스 및 관련 네트워킹 리소스를 만듭니다.

### <a name="validating-feature-registration"></a>기능 등록 유효성 검사

위에서 설명한 대로 프로비전 작업을 수행하려면 Dedicated HSM 서비스가 구독에 등록되어 있어야 합니다. 이에 대한 유효성 검사를 수행하려면 Azure Portal Cloud Shell에서 다음 PowerShell 명령을 실행합니다. 

```powershell
Get-AzProviderFeature -ProviderNamespace Microsoft.HardwareSecurityModules -FeatureName AzureDedicatedHsm
```

계속하기 전에 명령은 아래에 표시된 것처럼 “등록됨” 상태를 반환해야 합니다.  이 서비스에 등록되지 않은 경우 Microsoft 계정 담당자에게 문의하세요.

![구독 상태](media/tutorial-deploy-hsm-powershell/subscription-status.png)

### <a name="creating-hsm-resources"></a>HSM 리소스 만들기

고객의 가상 네트워크에 HSM 디바이스가 프로비전되었습니다. 이는 서브넷에 대한 요구 사항을 의미합니다. HSM이 가상 네트워크와 물리적 디바이스 간 통신을 구현하는 데 필요한 종속 항목은 ExpressRoute 게이트웨이이며, 마지막으로 Gemalto 클라이언트 소프트웨어를 사용하여 HSM 디바이스에 액세스하기 위해 가상 머신이 필요합니다. 이러한 리소스는 사용 편의를 위해 해당 매개 변수 파일과 함께 템플릿 파일에 수집되었습니다. 이러한 파일은 Microsoft(HSMrequest@Microsoft.com)에 직접 문의하면 사용 가능합니다.

파일을 확보하면 매개 변수 파일을 편집하여 리소스의 기본 이름을 삽입해야 합니다. 즉, “value”: “”를 사용하여 줄을 편집합니다.

- `namingInfix` HSM 리소스 이름의 접두사
- `ExistingVirtualNetworkName` HSM에 사용하는 가상 네트워크의 이름
- `DedicatedHsmResourceName1` 데이터 센터 스탬프 1에서 HSM 리소스의 이름
- `DedicatedHsmResourceName2` 데이터 센터 스탬프 2에서 HSM 리소스의 이름
- `hsmSubnetRange` HSM의 서브넷 IP 주소 범위
- `ERSubnetRange` VNET 게이트웨이의 서브넷 IP 주소 범위

이러한 변경 사항의 예는 다음과 같습니다.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "namingInfix": {
      "value": "MyHSM"
    },
    "ExistingVirtualNetworkName": {
      "value": "MyHSM-vnet"
    },
    "DedicatedHsmResourceName1": {
      "value": "HSM1"
    },
    "DedicatedHsmResourceName2": {
      "value": "HSM2"
    },
    "hsmSubnetRange": {
      "value": "10.0.2.0/24"
    },
    "ERSubnetRange": {
      "value": "10.0.255.0/26"
    },
  }
}
```

연결된 Resource Manager 템플릿 파일은 이러한 정보로 리소스 6개를 만듭니다.

- 지정된 VNET의 HSM용 서브넷
- 가상 네트워크 게이트웨이용 서브넷 
- HSM 디바이스에 VNET을 연결하는 가상 네트워크 게이트웨이
- 게이트웨이의 공용 IP 주소
- 스탬프 1의 HSM
- 스탬프 2의 HSM

매개 변수 값이 설정되면 파일을 사용하기 위해 Azure Portal Cloud Shell 파일 공유에 업로드해야 합니다. Azure Portal에서 오른쪽 상단에 있는 “\>\_” Cloud Shell 기호를 클릭하면 화면의 하단 부분이 명령 환경이 됩니다. 이에 대한 옵션은 BASH 및 PowerShell이며, 아직 설정되지 않은 경우 BASH를 선택해야 합니다.

명령 셸 도구 모음에는 업로드/다운로드 옵션이 있고, 파일 공유에 템플릿 및 매개 변수 파일을 업로드하려면 이 옵션을 선택해야 합니다.

![파일 공유](media/tutorial-deploy-hsm-powershell/file-share.png)

파일이 업로드되면 리소스를 만들 수 있습니다.
새 HSM을 만들기 전에 반드시 갖추어야 하는 일부 필수 리소스가 있습니다. 컴퓨팅, HSM 및 게이트웨이에 대한 서브넷 범위를 지원하는 가상 네트워크가 있어야 합니다. 다음 명령은 이러한 가상 네트워크를 만드는 요소에 대한 예를 보여줍니다.

```powershell
$compute = New-AzVirtualNetworkSubnetConfig `
  -Name compute `
  -AddressPrefix 10.2.0.0/24
```

```powershell
$delegation = New-AzDelegation `
  -Name "myDelegation" `
  -ServiceName "Microsoft.HardwareSecurityModules/dedicatedHSMs"

```

```powershell
$hsmsubnet = New-AzVirtualNetworkSubnetConfig ` 
  -Name hsmsubnet ` 
  -AddressPrefix 10.2.1.0/24 ` 
  -Delegation $delegation 

```

```powershell

$gwsubnet= New-AzVirtualNetworkSubnetConfig `
  -Name GatewaySubnet `
  -AddressPrefix 10.2.255.0/26

```

```powershell

New-AzVirtualNetwork `
  -Name myHSM-vnet `
  -ResourceGroupName myRG `
  -Location westus `
  -AddressPrefix 10.2.0.0/16 `
  -Subnet $compute, $hsmsubnet, $gwsubnet

```

>[!NOTE]
>가상 네트워크에서 주목해야 할 가장 중요한 구성은 HSM 디바이스의 서브넷에 “Microsoft.HardwareSecurityModules/dedicatedHSMs”로 설정된 위임이 있어야 한다는 사실입니다.  이 항목이 없으면 HSM 프로비전이 작동하지 않습니다.

모든 필수 구성 요소가 준비되면 Resource Manager 템플릿을 사용하여 고유한 이름(최소한 리소스 그룹 이름이라도)으로 값을 업데이트했는지 확인하는 다음 명령을 실행합니다.

```powershell

New-AzResourceGroupDeployment -ResourceGroupName myRG `
     -TemplateFile .\Deploy-2HSM-toVNET-Template.json `
     -TemplateParameterFile .\Deploy-2HSM-toVNET-Params.json `
     -Name HSMdeploy -Verbose

```

이 명령은 완료하는 데 약 20분 정도 소요됩니다. 사용된 “-verbose” 옵션은 상태가 지속적으로 표시되도록 합니다.

![프로비전 상태](media/tutorial-deploy-hsm-powershell/progress-status.png)

성공적으로 완료되면 “provisioningState”: “Succeeded”가 표시되며, 기존 가상 머신에 로그인하고 SSH를 사용하여 HSM 디바이스의 가용성을 확인할 수 있습니다.

## <a name="verifying-the-deployment"></a>배포 확인

디바이스가 프로비전되었는지 확인하고 디바이스 특성을 보려면 다음 명령 집합을 실행합니다. 리소스 그룹이 적절하게 설정되었고 리소스 이름이 매개 변수 파일과 똑같은지 확인합니다.

```powershell

$subid = (Get-AzContext).Subscription.Id
$resourceGroupName = "myRG"
$resourceName = "HSM1"  
Get-AzResource -Resourceid /subscriptions/$subId/resourceGroups/$resourceGroupName/providers/Microsoft.HardwareSecurityModules/dedicatedHSMs/$resourceName

```

![프로비전 상태](media/tutorial-deploy-hsm-powershell/progress-status2.png)

또한 이제 [Azure 리소스 탐색기](https://resources.azure.com/)를 사용하여 리소스를 볼 수 있습니다.   탐색기에서 왼쪽에 있는 “구독”, Dedicated HSM의 특정 구독, “리소스 그룹”, 사용한 리소스 그룹을 차례로 확장하고, 마지막으로 “리소스” 항목을 선택합니다.

## <a name="testing-the-deployment"></a>배포 테스트

배포를 테스트할 경우 HSM에 액세스할 수 있는 가상 머신에 연결한 후 HSM 디바이스에 직접 연결합니다. 이러한 작업은 HSM에 연결할 수 있는지 확인합니다.
ssh 도구를 사용하여 가상 머신에 연결합니다. 이 명령은 다음과 유사하지만 매개 변수에 지정된 관리자 이름과 dns 이름을 사용합니다.

`ssh adminuser@hsmlinuxvm.westus.cloudapp.azure.com`

사용할 암호는 매개 변수 파일의 암호입니다.
Linux VM에 로그온하면 포털에서 리소스 \<prefix>hsm_vnic에 대해 확인된 개인 IP 주소를 사용하여 HSM에 로그인할 수 있습니다.

```powershell

(Get-AzResource -ResourceGroupName myRG -Name HSMdeploy -ExpandProperties).Properties.networkProfile.networkInterfaces.privateIpAddress

```
IP 주소가 확인되면 다음 명령을 실행합니다.

`ssh tenantadmin@<ip address of HSM>`

성공하면 암호를 묻는 메시지가 나타납니다. 기본 암호는 PASSWORD입니다. HSM은 강력한 암호를 설정할 수 있도록 암호를 변경하고, 조직에서 선호하는 메커니즘으로 암호를 저장하여 분실을 방지하라는 메시지를 표시합니다.  

>[!IMPORTANT]
>이 암호를 분실할 경우 HSM을 다시 설정해야 하고, 그러면 키가 분실됩니다.

ssh를 사용하여 HSM에 연결하는 경우 HSM 디바이스가 작동하도록 다음 명령을 실행합니다.

`hsm show`

출력은 아래에 표시된 이미지와 같아야 합니다.

![hsm show 명령의 출력을 보여주는 스크린샷.](media/tutorial-deploy-hsm-powershell/output.png)

이제 고가용성의 두 HSM 배포에 모든 리소스가 할당되고, 액세스 및 작동 상태에 대한 유효성 검사가 완료된 상태여야 합니다. 추가 구성 또는 테스트를 위해서는 HSM 디바이스 자체로 추가 작업을 수행해야 합니다. 이를 위해서는 Gemalto Luna Network HSM 7 Administration Guide 7장의 지침을 따라 HSM을 초기화하고 파티션을 만들어야 합니다. Gemalto 고객 지원 포털에 등록되어 있고 고객 ID가 있으면 모든 설명서 및 소프트웨어를 Gemalto에서 직접 다운로드할 수 있습니다. 모든 필수 구성 요소를 받으려면 클라이언트 소프트웨어 7.2 버전을 다운로드하세요.

## <a name="delete-or-clean-up-resources"></a>리소스 삭제 또는 정리

HSM 디바이스로만 완료한 경우 리소스로 삭제하고 사용 가능 풀로 반환할 수 있습니다. 이 작업을 수행할 때 확실한 문제는 디바이스에 있는 모든 중요한 고객 데이터입니다. 디바이스를 "제로화"하는 가장 좋은 방법은 HSM 관리자 암호를 3번 잘못 가져오는 것입니다(참고: 이는 어플라이언스 관리자가 아니라 실제 HSM 관리자임). 핵심 자료를 보호하는 차원에서 디바이스는 초기화 상태가 될 때까지 Azure 리소스로 간주하며, 삭제할 수 없습니다.

> [!NOTE]
> Gemalto 디바이스 구성과 관련하여 문제가 발생할 경우 [Gemalto 고객 지원팀](https://safenet.gemalto.com/technical-support/)에 연락하시기 바랍니다.

Azure에서 HSM 리소스를 제거하려는 경우 다음 명령을 사용하여 "$" 변수를 고유한 매개 변수로 바꿀 수 있습니다.

```powershell

$subid = (Get-AzContext).Subscription.Id
$resourceGroupName = "myRG" 
$resourceName = "HSMdeploy"  
Remove-AzResource -Resourceid /subscriptions/$subId/resourceGroups/$resourceGroupName/providers/Microsoft.HardwareSecurityModules/dedicatedHSMs/$resourceName 

```

## <a name="next-steps"></a>다음 단계

이 자습서의 단계를 완료하면 Dedicated HSM 리소스가 프로비전되고 가상 네트워크에서 사용할 수 있게 됩니다. 이제 기본 배포 아키텍처에 필요한 만큼 리소스를 추가하여 이러한 배포판을 보완할 수 있습니다. 배포 계획에 도움이 되는 자세한 내용은 개념 문서를 참조하세요. 기본 지역에 있는 HSM 두 개가 랙 수준에서 가용성을 지원하고, 보조 지역에 있는 HSM 두 개가 지역 가용성을 지원하는 디자인이 권장됩니다. 이 자습서에서 사용한 템플릿 파일은 두 HSM 배포에 대한 기준으로 쉽게 사용할 수 있지만 해당 요구 사항에 맞게 매개 변수를 수정해야 합니다.

* [고가용성](high-availability.md)
* [물리적 보안](physical-security.md)
* [네트워킹](networking.md)
* [Monitoring](monitoring.md)
* [지원 가능성](supportability.md)
