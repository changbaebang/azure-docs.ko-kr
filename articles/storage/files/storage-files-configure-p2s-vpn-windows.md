---
title: Azure Files에서 사용하기 위한 Windows의 P2S(지점 및 사이트 간) VPN 구성 | Microsoft Docs
description: Azure Files에서 사용하기 위한 Windows의 P2S(지점 및 사이트 간) VPN 구성 방법
author: roygara
ms.service: storage
ms.topic: how-to
ms.date: 10/19/2019
ms.author: rogarana
ms.subservice: files
ms.openlocfilehash: 6253deb53229172cd499a6aa14b8d8f19bc07b63
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94629260"
---
# <a name="configure-a-point-to-site-p2s-vpn-on-windows-for-use-with-azure-files"></a>Azure Files에서 사용하기 위한 Windows의 P2S(지점 및 사이트 간) VPN 구성
P2S(지점 및 사이트 간) VPN 연결을 사용하여 포트 445을 열지 않고 Azure 외부에서 SMB를 통해 Azure 파일 공유를 탑재할 수 있습니다. 지점 및 사이트 간 VPN 연결은 Azure와 개별 클라이언트 간의 VPN 연결입니다. Azure Files에서 P2S VPN 연결을 사용하려면 연결하려는 각 클라이언트에 대해 P2S VPN 연결을 구성해야 합니다. 온-프레미스 네트워크에서 Azure 파일 공유에 연결해야 하는 클라이언트가 많은 경우에는 각 클라이언트에 대해 지점 및 사이트 간 연결 대신 S2S(사이트 간) VPN 연결을 사용할 수 있습니다. 자세한 내용은 [Azure Files에서 사용하기 위한 사이트 간 VPN 구성](storage-files-configure-s2s-vpn.md)을 참조하세요.

Azure Files에 사용할 수 있는 네트워킹 옵션에 대해 자세히 알아보려면 이 방법 문서를 계속하기 전에 먼저 [직접 Azure 파일 공유 액세스에 대한 네트워킹 고려 사항](storage-files-networking-overview.md)을 읽어볼 것을 강력하게 권장합니다.

이 문서에서는 Azure 파일 공유를 온-프레미스에 직접 탑재하도록 Windows(Windows 클라이언트 및 Windows Server)에서 지점 및 사이트 간 VPN을 구성하는 단계를 자세히 설명합니다. VPN을 통해 Azure 파일 동기화 트래픽을 라우팅하는 경우 [Azure 파일 동기화 프록시 및 방화벽 설정 구성](storage-sync-files-firewall-and-proxy.md)을 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소
- 최신 버전의 Azure PowerShell 모듈. Azure PowerShell을 설치하는 방법에 대한 자세한 내용은 [Azure PowerShell 모듈 설치](/powershell/azure/install-az-ps)를 참조하고 해당 운영 체제를 선택합니다. Windows에서 Azure CLI를 사용하고 싶은 분들은 그렇게 해도 되지만, 아래 지침은 Azure PowerShell에 대한 지침입니다.

- 온-프레미스에 탑재하려는 Azure 파일 공유. Azure 파일 공유는 저장소 계정 내에 배포 됩니다. 저장소 계정에는 blob 컨테이너 또는 큐와 같은 다른 저장소 리소스 뿐만 아니라 여러 파일 공유를 배포할 수 있는 저장소의 공유 풀을 나타내는 관리 구문도 있습니다. Azure 파일 공유 및 저장소 계정을 배포 하는 방법에 대 한 자세한 내용은 [azure 파일 공유 만들기](storage-how-to-create-file-share.md)를 통해 확인할 수 있습니다.

- 온-프레미스에 탑재 하려는 Azure 파일 공유가 포함 된 저장소 계정의 개인 끝점입니다. 개인 끝점을 만드는 방법에 대 한 자세한 내용은 [Azure Files 네트워크 끝점 구성](storage-files-networking-endpoints.md?tabs=azure-powershell)을 참조 하세요. 

## <a name="deploy-a-virtual-network"></a>가상 네트워크 배포
지점 및 사이트 간 VPN을 통해 온-프레미스에서 Azure 파일 공유 및 기타 Azure 리소스에 액세스하려면 VNet(가상 네트워크)을 만들어야 합니다. 자동으로 생성되는 P2S VPN 연결은 온-프레미스 Windows 머신과 이 Azure 가상 네트워크 간의 브리지입니다.

다음 PowerShell은 세 개의 서브넷을 사용하여 Azure 가상 네트워크를 만듭니다. 하나는 스토리지 계정의 서비스 엔드포인트를 위한 것이고, 다른 하나는 변경될 수 있는 스토리지 계정의 공용 IP에 대한 사용자 지정 라우팅을 생성하지 않고 온-프레미스에서 스토리지 계정에 액세스해야 하는 스토리지 계정의 프라이빗 엔드포인트입니다. 마지막은 VPN 서비스를 제공하는 가상 네트워크 게이트웨이를 위한 것입니다. 

`<region>`, `<resource-group>` 및 `<desired-vnet-name>`을 사용자 환경에 적합한 값으로 바꿔야 합니다.

```PowerShell
$region = "<region>"
$resourceGroupName = "<resource-group>" 
$virtualNetworkName = "<desired-vnet-name>"

$virtualNetwork = New-AzVirtualNetwork `
    -ResourceGroupName $resourceGroupName `
    -Name $virtualNetworkName `
    -Location $region `
    -AddressPrefix "192.168.0.0/16"

Add-AzVirtualNetworkSubnetConfig `
    -Name "ServiceEndpointSubnet" `
    -AddressPrefix "192.168.0.0/24" `
    -VirtualNetwork $virtualNetwork `
    -ServiceEndpoint "Microsoft.Storage" `
    -WarningAction SilentlyContinue | Out-Null

Add-AzVirtualNetworkSubnetConfig `
    -Name "PrivateEndpointSubnet" `
    -AddressPrefix "192.168.1.0/24" `
    -VirtualNetwork $virtualNetwork `
    -WarningAction SilentlyContinue | Out-Null

Add-AzVirtualNetworkSubnetConfig `
    -Name "GatewaySubnet" `
    -AddressPrefix "192.168.2.0/24" `
    -VirtualNetwork $virtualNetwork `
    -WarningAction SilentlyContinue | Out-Null

$virtualNetwork | Set-AzVirtualNetwork | Out-Null
$virtualNetwork = Get-AzVirtualNetwork `
    -ResourceGroupName $resourceGroupName `
    -Name $virtualNetworkName

$serviceEndpointSubnet = $virtualNetwork.Subnets | `
    Where-Object { $_.Name -eq "ServiceEndpointSubnet" }
$privateEndpointSubnet = $virtualNetwork.Subnets | `
    Where-Object { $_.Name -eq "PrivateEndpointSubnet" }
$gatewaySubnet = $virtualNetwork.Subnets | ` 
    Where-Object { $_.Name -eq "GatewaySubnet" }
```

## <a name="create-root-certificate-for-vpn-authentication"></a>VPN 인증에 사용할 루트 인증서 만들기
온-프레미스 Windows 머신에서 VPN 연결을 인증하여 가상 네트워크에 액세스할 수 있도록 하려면 두 개의 인증서를 만들어야 합니다. 하나는 가상 머신 게이트웨이에 제공되는 루트 인증서이고, 다른 하나는 루트 인증서로 서명되는 클라이언트 인증서입니다. 다음 PowerShell은 루트 인증서를 만듭니다. 클라이언트 인증서는 게이트웨이의 정보를 사용하여 Azure 가상 네트워크 게이트웨이를 만든 후에 만들어집니다. 

```PowerShell
$rootcertname = "CN=P2SRootCert"
$certLocation = "Cert:\CurrentUser\My"
$vpnTemp = "C:\vpn-temp\"
$exportedencodedrootcertpath = $vpnTemp + "P2SRootCertencoded.cer"
$exportedrootcertpath = $vpnTemp + "P2SRootCert.cer"

if (-Not (Test-Path $vpnTemp)) {
    New-Item -ItemType Directory -Force -Path $vpnTemp | Out-Null
}

if ($PSVersionTable.PSVersion -ge [System.Version]::new(6, 0)) {
    Install-Module WindowsCompatibility
    Import-WinModule PKI
}

$rootcert = New-SelfSignedCertificate `
    -Type Custom `
    -KeySpec Signature `
    -Subject $rootcertname `
    -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 `
    -KeyLength 2048 `
    -CertStoreLocation $certLocation `
    -KeyUsageProperty Sign `
    -KeyUsage CertSign

Export-Certificate `
    -Cert $rootcert `
    -FilePath $exportedencodedrootcertpath `
    -NoClobber | Out-Null

certutil -encode $exportedencodedrootcertpath $exportedrootcertpath | Out-Null

$rawRootCertificate = Get-Content -Path $exportedrootcertpath

[System.String]$rootCertificate = ""
foreach($line in $rawRootCertificate) { 
    if ($line -notlike "*Certificate*") { 
        $rootCertificate += $line 
    } 
}
```

## <a name="deploy-virtual-network-gateway"></a>가상 네트워크 게이트웨이 배포
Azure 가상 네트워크 게이트웨이는 온-프레미스 Windows 머신에서 연결할 서비스입니다. 이 서비스를 배포하려면 두 가지 기본 구성 요소가 필요합니다. 즉, 전 세계에 있는 클라이언트에 대한 게이트웨이를 식별하는 공용 IP와 클라이언트를 인증하는 데 사용되는 이전에 만든 루트 인증서가 필요합니다.

`<desired-vpn-name-here>`를 이러한 리소스에 사용할 이름으로 바꿔야 합니다.

> [!Note]  
> Azure 가상 네트워크 게이트웨이를 배포하는 데 최대 45분이 걸릴 수 있습니다. 이 리소스가 배포되는 동안 이 PowerShell 스크립트는 배포가 완료될 때까지 차단됩니다. 예상된 동작입니다.

```PowerShell
$vpnName = "<desired-vpn-name-here>" 
$publicIpAddressName = "$vpnName-PublicIP"

$publicIPAddress = New-AzPublicIpAddress `
    -ResourceGroupName $resourceGroupName `
    -Name $publicIpAddressName `
    -Location $region `
    -Sku Basic `
    -AllocationMethod Dynamic

$gatewayIpConfig = New-AzVirtualNetworkGatewayIpConfig `
    -Name "vnetGatewayConfig" `
    -SubnetId $gatewaySubnet.Id `
    -PublicIpAddressId $publicIPAddress.Id

$azRootCertificate = New-AzVpnClientRootCertificate `
    -Name "P2SRootCert" `
    -PublicCertData $rootCertificate

$vpn = New-AzVirtualNetworkGateway `
    -ResourceGroupName $resourceGroupName `
    -Name $vpnName `
    -Location $region `
    -GatewaySku VpnGw1 `
    -GatewayType Vpn `
    -VpnType RouteBased `
    -IpConfigurations $gatewayIpConfig `
    -VpnClientAddressPool "172.16.201.0/24" `
    -VpnClientProtocol IkeV2 `
    -VpnClientRootCertificates $azRootCertificate
```

## <a name="create-client-certificate"></a>클라이언트 인증서 만들기
클라이언트 인증서는 가상 네트워크 게이트웨이의 URI를 사용하여 생성됩니다. 이 인증서는 이전에 만든 루트 인증서를 사용하여 서명됩니다.

```PowerShell
$clientcertpassword = "1234"

$vpnClientConfiguration = New-AzVpnClientConfiguration `
    -ResourceGroupName $resourceGroupName `
    -Name $vpnName `
    -AuthenticationMethod EAPTLS

Invoke-WebRequest `
    -Uri $vpnClientConfiguration.VpnProfileSASUrl `
    -OutFile "$vpnTemp\vpnclientconfiguration.zip"

Expand-Archive `
    -Path "$vpnTemp\vpnclientconfiguration.zip" `
    -DestinationPath "$vpnTemp\vpnclientconfiguration"

$vpnGeneric = "$vpnTemp\vpnclientconfiguration\Generic"
$vpnProfile = ([xml](Get-Content -Path "$vpnGeneric\VpnSettings.xml")).VpnProfile

$exportedclientcertpath = $vpnTemp + "P2SClientCert.pfx"
$clientcertname = "CN=" + $vpnProfile.VpnServer

$clientcert = New-SelfSignedCertificate `
    -Type Custom `
    -DnsName $vpnProfile.VpnServer `
    -KeySpec Signature `
    -Subject $clientcertname `
    -KeyExportPolicy Exportable `
    -HashAlgorithm sha256 `
    -KeyLength 2048 `
    -CertStoreLocation $certLocation `
    -Signer $rootcert `
    -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")

$mypwd = ConvertTo-SecureString -String $clientcertpassword -Force -AsPlainText

Export-PfxCertificate `
    -FilePath $exportedclientcertpath `
    -Password $mypwd `
    -Cert $clientcert | Out-Null
```

## <a name="configure-the-vpn-client"></a>VPN 클라이언트 구성
Azure 가상 네트워크 게이트웨이는 온-프레미스 Windows 머신에서 VPN 연결을 초기화하는 데 필요한 구성 파일이 포함된 다운로드 가능한 패키지를 만듭니다. Windows 10/Windows Server 2016 이상의 [Always On VPN](/windows-server/remote/remote-access/vpn/always-on-vpn/) 기능을 사용하여 VPN 연결을 구성하겠습니다. 이 패키지에는 원하는 경우 레거시 Windows VPN 클라이언트를 구성할 수 있는 실행 가능 패키지도 포함되어 있습니다. 이 가이드에서는 레거시 Windows VPN 클라이언트가 아닌 Always On VPN을 사용합니다. Always On VPN 클라이언트는 최종 사용자가 머신에 대한 관리자 권한이 없어도 Azure VPN에서 연결/연결 해제할 수 있기 때문입니다. 

다음 스크립트는 가상 네트워크 게이트웨이에 대한 인증에 필요한 클라이언트 인증서를 설치하고, VPN 패키지를 다운로드하여 설치합니다. 잊지 말고 `<computer1>` 및 `<computer2>`를 적절한 정보로 바꿔야 합니다. `$sessions` 배열에 PowerShell 세션을 더 추가하여 원하는 수의 머신에서 이 스크립트를 실행할 수 있습니다. 사용 계정은 이러한 각 머신의 관리자여야 합니다. 이러한 머신 중 하나가 스크립트를 실행하는 로컬 머신이면 관리자 권한 PowerShell 세션에서 스크립트를 실행해야 합니다. 

```PowerShell
$sessions = [System.Management.Automation.Runspaces.PSSession[]]@()
$sessions += New-PSSession -ComputerName "<computer1>"
$sessions += New-PSSession -ComputerName "<computer2>"

foreach ($session in $sessions) {
    Invoke-Command -Session $session -ArgumentList $vpnTemp -ScriptBlock { 
        $vpnTemp = $args[0]
        if (-Not (Test-Path $vpnTemp)) {
            New-Item `
                -ItemType Directory `
                -Force `
                -Path "C:\vpn-temp" | Out-Null
        }
    }

    Copy-Item `
        -Path $exportedclientcertpath, $exportedrootcertpath, "$vpnTemp\vpnclientconfiguration.zip" `
        -Destination $vpnTemp `
        -ToSession $session

    Invoke-Command `
        -Session $session `
        -ArgumentList `
            $mypwd, `
            $vpnTemp, `
            $virtualNetworkName `
        -ScriptBlock { 
            $mypwd = $args[0] 
            $vpnTemp = $args[1]
            $virtualNetworkName = $args[2]

            Import-PfxCertificate `
                -Exportable `
                -Password $mypwd `
                -CertStoreLocation "Cert:\LocalMachine\My" `
                -FilePath "$vpnTemp\P2SClientCert.pfx" | Out-Null

            Import-Certificate `
                -FilePath "$vpnTemp\P2SRootCert.cer" `
                -CertStoreLocation "Cert:\LocalMachine\Root" | Out-Null

            Expand-Archive `
                -Path "$vpnTemp\vpnclientconfiguration.zip" `
                -DestinationPath "$vpnTemp\vpnclientconfiguration"
            $vpnGeneric = "$vpnTemp\vpnclientconfiguration\Generic"

            $vpnProfile = ([xml](Get-Content -Path "$vpnGeneric\VpnSettings.xml")).VpnProfile

            Add-VpnConnection `
                -Name $virtualNetworkName `
                -ServerAddress $vpnProfile.VpnServer `
                -TunnelType Ikev2 `
                -EncryptionLevel Required `
                -AuthenticationMethod MachineCertificate `
                -SplitTunneling `
                -AllUserConnection

            Add-VpnConnectionRoute `
                -Name $virtualNetworkName `
                -DestinationPrefix $vpnProfile.Routes `
                -AllUserConnection

            Add-VpnConnectionRoute `
                -Name $virtualNetworkName `
                -DestinationPrefix $vpnProfile.VpnClientAddressPool `
                -AllUserConnection

            rasdial $virtualNetworkName
        }
}

Remove-Item -Path $vpnTemp -Recurse
```

## <a name="mount-azure-file-share"></a>Azure 파일 공유 탑재
지점 및 사이트 간 VPN을 설정했으므로, PowerShell을 통해 설정한 컴퓨터에서 Azure 파일 공유를 탑재하는 데 사용할 수 있습니다. 다음 예제는 공유를 탑재하고, 공유가 실제로 탑재되었는지 증명하기 위해 공유의 루트 디렉터리를 나열하고, 공유를 탑재 해제합니다. 아쉽게도 PowerShell 원격을 통해 영구적으로 공유를 탑재할 수는 없습니다. 영구적으로 탑재하려면 [Windows에서 Azure 파일 공유 사용](storage-how-to-use-files-windows.md)을 참조하세요. 

```PowerShell
$myShareToMount = "<file-share>"

$storageAccountKeys = Get-AzStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $storageAccountName
$storageAccountKey = ConvertTo-SecureString `
    -String $storageAccountKeys[0].Value `
    -AsPlainText `
    -Force

$nic = Get-AzNetworkInterface -ResourceId $privateEndpoint.NetworkInterfaces[0].Id
$storageAccountPrivateIP = $nic.IpConfigurations[0].PrivateIpAddress

Invoke-Command `
    -Session $sessions `
    -ArgumentList  `
        $storageAccountName, `
        $storageAccountKey, `
        $storageAccountPrivateIP, `
        $myShareToMount `
    -ScriptBlock {
        $storageAccountName = $args[0]
        $storageAccountKey = $args[1]
        $storageAccountPrivateIP = $args[2]
        $myShareToMount = $args[3]

        $credential = [System.Management.Automation.PSCredential]::new(
            "AZURE\$storageAccountName", 
            $storageAccountKey)

        New-PSDrive `
            -Name Z `
            -PSProvider FileSystem `
            -Root "\\$storageAccountPrivateIP\$myShareToMount" `
            -Credential $credential `
            -Persist | Out-Null
        Get-ChildItem -Path Z:\
        Remove-PSDrive -Name Z
    }
```

## <a name="see-also"></a>참고 항목
- [직접 Azure 파일 공유 액세스를 위한 네트워킹 고려 사항](storage-files-networking-overview.md)
- [Azure Files에서 사용할 P2S(지점 및 사이트 간) VPN을 Linux에 구성](storage-files-configure-p2s-vpn-linux.md)
- [Azure Files에서 사용할 S2S(사이트 간) VPN 구성](storage-files-configure-s2s-vpn.md)