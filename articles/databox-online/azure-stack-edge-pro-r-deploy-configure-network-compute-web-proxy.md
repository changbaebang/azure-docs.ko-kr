---
title: Azure Portal에서 Azure Stack Edge Pro R 디바이스에 대한 네트워크 설정을 구성하는 자습서 | Microsoft Docs
description: Azure Stack Edge Pro R을 배포하기 위한 자습서에서는 물리적 디바이스에 대한 네트워크, 컴퓨팅 네트워크 및 웹 프록시 설정의 구성을 안내합니다.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: tutorial
ms.date: 02/04/2021
ms.author: alkohli
Customer intent: As an IT admin, I need to understand how to connect and activate Azure Stack Edge Pro R so I can use it to transfer data to Azure.
ms.openlocfilehash: 11c1d76b5784587f234455f81595778897569eb1
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99822471"
---
# <a name="tutorial-configure-network-for-azure-stack-edge-pro-r"></a>자습서: Azure Stack Edge Pro R에 대한 네트워크 구성

이 자습서에서는 로컬 웹 UI를 사용하여 Azure Stack Edge Pro R 디바이스에 대한 네트워크를 구성하는 방법을 설명합니다.

연결 프로세스를 완료하는 데 20분 정도가 소요됩니다.

이 자습서에서는 다음에 대해 알아봅니다.

> [!div class="checklist"]
>
> * 필수 조건
> * 네트워크 구성
> * 컴퓨팅 네트워크 사용
> * 웹 프록시 구성


## <a name="prerequisites"></a>필수 조건

Azure Stack Edge Pro R 디바이스를 구성하고 설정하기 전에 다음 사항을 확인합니다.

* [Azure Stack Edge Pro R 설치](azure-stack-edge-gpu-deploy-install.md)에서 설명한 대로 물리적 디바이스를 설치했습니다.
* [Azure Stack Edge Pro R에 연결](azure-stack-edge-gpu-deploy-connect.md)에 자세히 설명된 대로 디바이스의 로컬 웹 UI에 연결했습니다.


## <a name="configure-network"></a>네트워크 구성

**시작** 페이지에는 물리적 디바이스를 구성하고 Azure Stack Edge 서비스에 등록하는 데 필요한 다양한 설정이 표시됩니다. 

다음 단계에 따라 디바이스에 대한 네트워크를 구성합니다.

1. 디바이스의 로컬 웹 UI에서 **시작** 페이지로 이동합니다. 

2. **네트워크** 타일에서 **구성** 을 선택하여 **네트워크** 페이지로 이동합니다. 
    
    <!--![Local web UI "Network settings" tile](./media/azure-stack-edge-gpu-deploy-configure-network-compute-web-proxy/network-1.png)-->

    물리적 디바이스에는 네 개의 네트워크 인터페이스가 있습니다. 포트 1 및 포트 2는 1Gbps 네트워크 인터페이스입니다. 포트 3 및 포트 4는 모두 10/25Gbps 네트워크 인터페이스입니다. 포트 1은 관리 전용 포트로 자동으로 구성되고, 포트 2~포트 4는 모두 데이터 포트입니다. **네트워크** 페이지는 다음과 같습니다.
    
    ![로컬 웹 UI "네트워크 설정" 페이지](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-2.png)

   
3. 네트워크 설정을 변경하려면 포트를 선택하고 표시된 오른쪽 창에서 IP 주소, 서브넷, 게이트웨이, 기본 DNS 및 보조 DNS를 수정합니다. 

    - 포트 1을 선택하면 정적으로 미리 구성된 것을 볼 수 있습니다. 

        ![로컬 웹 UI “포트 1 네트워크 설정”](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-3.png)

    - 포트 2, 포트 3 또는 포트 4를 선택하면 기본적으로 이러한 모든 포트가 DHCP로 구성됩니다.

        ![로컬 웹 UI “포트 3 네트워크 설정”](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-4.png)

    네트워크 설정을 구성할 때 다음에 유의합니다.

   * 환경에서 DHCP를 사용하도록 설정하면 네트워크 인터페이스가 자동으로 구성됩니다. IP 주소, 서브넷, 게이트웨이 및 DNS가 자동으로 할당됩니다.
   * DHCP를 사용하지 않는 경우 필요에 따라 고정 IP를 할당할 수 있습니다.
   * 네트워크 인터페이스를 IPv4로 구성할 수 있습니다.
   * NIC(네트워크 인터페이스 카드) 팀 구성 또는 링크 집계는 Azure Stack Edge에서 지원되지 않습니다.
   * 모든 포트에 대한 일련 번호는 노드 일련 번호에 해당합니다.
    <!--* On the 25-Gbps interfaces, you can set the RDMA (Remote Direct Access Memory) mode to iWarp or RoCE (RDMA over Converged Ethernet). Where low latencies are the primary requirement and scalability is not a concern, use RoCE. When latency is a key requirement, but ease-of-use and scalability are also high priorities, iWARP is the best candidate.-->
    디바이스 네트워크를 구성하면 아래와 같이 페이지가 업데이트됩니다.

    ![로컬 웹 UI "네트워크 설정" 페이지 2](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/network-2a.png)<!--change-->


     >[!NOTE]
     >
     > * 디바이스에 연결할 다른 IP 주소가 없으면 네트워크 인터페이스의 로컬 IP 주소를 고정에서 DCHP로 전환하지 않는 것이 좋습니다. 하나의 네트워크 인터페이스를 사용하며 DHCP로 전환하는 경우 DHCP 주소를 확인할 방법이 없습니다. DHCP 주소로 변경하려는 경우 디바이스가 서비스에 활성화될 때까지 기다렸다가 변경합니다. 그러면 서비스에 대한 Azure Portal의 **디바이스 속성** 에서 모든 어댑터의 IP를 볼 수 있습니다.


    네트워크 설정을 구성하고 적용한 후 **다음: 컴퓨팅** 을 선택하여 컴퓨팅 네트워크를 구성합니다.

## <a name="enable-compute-network"></a>컴퓨팅 네트워크 사용

다음 단계를 수행하여 컴퓨팅을 사용하도록 설정하고 컴퓨팅 네트워크를 구성합니다. 

1. **컴퓨팅** 페이지에서 컴퓨팅을 사용하도록 설정하려는 네트워크 인터페이스를 선택합니다. 

    ![로컬 UI의 컴퓨팅 페이지 2](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-2.png)

1. **네트워크 설정** 대화 상자에서 **사용** 을 선택합니다. 컴퓨팅을 사용하도록 설정하면 해당 네트워크 인터페이스의 디바이스에서 가상 스위치가 생성됩니다. 가상 스위치는 디바이스의 컴퓨팅 인프라에 사용됩니다. 
    
1. **Kubernetes 노드 IP** 를 할당합니다. 이러한 고정 IP 주소는 컴퓨팅 VM에 대한 것입니다.  

    *n*-노드 디바이스의 경우 시작 및 종료 IP 주소를 사용하여 컴퓨팅 VM에 대한 최소 *n+1* IPv4 주소의 연속 범위가 제공됩니다. Azure Stack Edge가 1-노드 디바이스인 경우에는 최소 2개의 연속 IPv4 주소가 제공됩니다. 이러한 IP 주소는 컴퓨팅을 사용하도록 설정하고 가상 스위치가 생성된 동일한 네트워크에 있어야 합니다.

    > [!IMPORTANT]
    > Azure Stack Edge의 Kubernetes는 pod에 172.27.0.0/16 서브넷을 사용하고 서비스에 172.28.0.0/16 서브넷을 사용합니다. 네트워크에서 사용 중이 아닌지 확인합니다. 이러한 서브넷이 네트워크에서 이미 사용 중인 경우에는 디바이스의 PowerShell 인터페이스에서 `Set-HcsKubeClusterNetworkInfo` cmdlet을 실행하여 이러한 서브넷을 변경할 수 있습니다. 자세한 내용은 [Kubernetes pod 및 서비스 서브넷](azure-stack-edge-gpu-connect-powershell-interface.md#change-kubernetes-pod-and-service-subnets)을 참조하세요.


1. **Kubernetes 외부 서비스 IP** 를 할당합니다. 이는 부하 분산 IP 주소이기도 합니다. 이러한 연속 IP 주소는 Kubernetes 클러스터 외부에 노출하려는 서비스에 대한 것이며, 노출되는 서비스의 수에 따라 고정 IP 범위를 지정합니다. 
    
    > [!IMPORTANT]
    > 컴퓨팅 모듈에 액세스하려면 Azure Stack Edge Pro R Hub 서비스에 대해 최소 1개의 IP 주소를 지정하는 것이 좋습니다. 그런 다음, 필요에 따라 클러스터 외부에서 액세스해야 하는 다른 서비스/IoT Edge 모듈(서비스/모듈당 1개)에 대한 추가 IP 주소를 지정할 수 있습니다. 서비스 IP 주소는 나중에 업데이트될 수 있습니다. 
    
1. **적용** 을 선택합니다.

    ![로컬 UI의 컴퓨팅 페이지 3](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-3.png)

1. 구성을 적용하는 데 몇 분 정도 걸리며, 브라우저를 새로 고쳐야 할 수도 있습니다. 지정한 포트가 컴퓨팅에 사용하도록 설정된 것을 볼 수 있습니다. 
 
    ![로컬 UI의 컴퓨팅 페이지 4](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/compute-network-4.png)

    완료되면 **다음: 웹 프록시** 를 선택하여 웹 프록시를 구성합니다.  

  
## <a name="configure-web-proxy"></a>웹 프록시 구성

이는 선택적 구성입니다.

> [!IMPORTANT]
> * Azure Stack Edge Pro R 디바이스에서 IoT Edge 모듈을 컴퓨팅하고 사용하도록 설정하는 경우 웹 프록시 인증을 **없음** 으로 설정하는 것이 좋습니다. NTLM은 지원되지 않습니다.
>* PAC(프록시 자동 구성) 파일은 지원되지 않습니다. PAC 파일은 웹 브라우저 및 다른 사용자 에이전트가 지정된 URL을 가져오는 데 적절한 프록시 서버(액세스 방법)를 자동으로 선택하는 방법을 정의합니다. 프록시의 인증서를 신뢰할 수 없기 때문에 모든 트래픽을 가로채고 읽는(그런 다음, 자체 인증을 사용하여 모든 항목을 다시 서명함) 프록시는 호환되지 않습니다. 일반적으로 투명 프록시는 Azure Stack Edge Pro R에서 잘 작동합니다. 투명하지 않은 웹 프록시는 지원되지 않습니다.


1. **웹 프록시 설정** 페이지에서 다음 단계를 수행합니다.

    1. **웹 프록시 URL** 상자에 `http://host-IP address or FQDN:Port number` 형식으로 URL을 입력합니다. HTTPS URL은 지원되지 않습니다.

    2. **인증** 아래에서 **없음** 또는 **NTLM** 을 선택합니다. Azure Stack Edge Pro R 디바이스에서 IoT Edge 모듈을 컴퓨팅하고 사용하도록 설정하는 경우 웹 프록시 인증을 **없음** 으로 설정하는 것이 좋습니다. **NTLM** 은 지원되지 않습니다.

    3. 인증을 사용하는 경우 사용자 이름과 암호를 입력합니다.

    4. 구성한 웹 프록시 설정의 유효성을 검사하고 적용하려면 **적용** 을 선택합니다.
    
   ![로컬 웹 UI "웹 프록시 설정" 페이지 2](./media/azure-stack-edge-pro-r-deploy-configure-network-compute-web-proxy/web-proxy-2.png)

2. 설정이 적용된 후 **다음: 디바이스** 를 입력하고 선택합니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음에 대해 알아보았습니다.

> [!div class="checklist"]
> * 필수 조건
> * 네트워크 구성
> * 컴퓨팅 네트워크 사용
> * 웹 프록시 구성


Azure Stack Edge Pro R 디바이스를 설정하는 방법을 알아보려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [디바이스 설정 구성](./azure-stack-edge-pro-r-deploy-set-up-device-update-time.md)
