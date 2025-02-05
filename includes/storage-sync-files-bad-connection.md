---
title: 파일 포함
description: 파일 포함
services: storage
author: roygara
ms.service: storage
ms.topic: include
ms.date: 07/08/2018
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: b26d4af29a92fb0f14c52e76a7eae1d0073a3aa0
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96005332"
---
서버에서 Azure 파일 동기화 서비스에 액세스할 수 없을 때마다 이 오류가 발생할 수 있습니다. 다음 단계를 진행하여 이 오류를 해결할 수 있습니다.

1. Windows 서비스 `FileSyncSvc.exe`가 방화벽에 의해 차단되지 않았는지 확인합니다.
2. 포트 443이 Azure 파일 동기화 서비스로 나가는 연결에 대해 열려 있는지 확인합니다. `Test-NetConnection` cmdlet을 사용하면 됩니다. 아래의 `<azure-file-sync-endpoint>` 자리 표시자에 대한 URL은 [Azure 파일 동기화 프록시 및 방화벽 설정](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall) 문서에서 찾을 수 있습니다. 

    ```powershell
    Test-NetConnection -ComputerName <azure-file-sync-endpoint> -Port 443
    ```

3. 프록시 구성이 예상대로 설정되었는지 확인합니다. `Get-StorageSyncProxyConfiguration` cmdlet으로 할 수 있습니다. Azure 파일 동기화에 대해 프록시를 구성하는 자세한 방법은 [Azure 파일 동기화 프록시 및 방화벽 설정](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#firewall)에서 찾을 수 있습니다.

    ```powershell
    $agentPath = "C:\Program Files\Azure\StorageSyncAgent"
    Import-Module "$agentPath\StorageSync.Management.ServerCmdlets.dll"
    Get-StorageSyncProxyConfiguration
    ```
4. Test-StorageSyncNetworkConnectivity cmdlet을 사용하여 서비스 엔드포인트에 대한 네트워크 연결을 확인합니다. 자세한 내용은 [서비스 엔드포인트에 대한 네트워크 연결 테스트](../articles/storage/files/storage-sync-files-firewall-and-proxy.md#test-network-connectivity-to-service-endpoints)를 참조하세요.    

5. 네트워크 연결 문제와 관련하여 추가적인 도움이 필요하면 네트워크 관리자에게 문의하세요.