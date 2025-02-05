---
title: 파일 포함
description: 포함 파일
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 10/28/2020
ms.author: cherylmc
ms.openlocfilehash: 34986ac80a309bcfd495e5782496ba560f84c5f7
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "93041566"
---
지점 및 사이트 간 연결을 사용하여 VNet에 연결하는 각 클라이언트 컴퓨터에는 클라이언트 인증서가 설치되어 있어야 합니다. 이 인증서는 루트 인증서에서 생성하여 각 클라이언트 컴퓨터에 설치합니다. 유효한 클라이언트 인증서를 설치하지 않으면 클라이언트에서 VNet에 연결하려고 할 때 인증이 실패합니다.

연결할 각 클라이언트에 대해 고유한 인증서를 생성하거나 여러 클라이언트에서 동일한 인증서를 사용할 수 있습니다. 고유한 클라이언트 인증서를 생성하면 단일 인증서를 해지할 수 있는 장점이 있습니다. 그렇지 않으면 여러 클라이언트에서 인증하는 데 동일한 클라이언트 인증서를 사용하지만 이 인증서를 철회하는 경우 해당 인증서를 사용하는 모든 클라이언트에 대해 새 인증서를 생성하여 설치해야 합니다.

클라이언트 인증서는 다음 메서드를 사용하여 생성할 수 있습니다.

* **엔터프라이즈 인증서:**

  * 엔터프라이즈 인증서 솔루션을 사용하는 경우 클라이언트 인증서를 일반적인 이름 값 형식(*name\@yourdomain.com*)으로 생성합니다. *도메인 이름\사용자 이름* 형식 대신 이 형식을 사용합니다.

  * 클라이언트 인증서가 사용자 목록의 첫 번째 항목으로 나열된 *클라이언트 인증* 이 있는 사용자 인증서 템플릿을 기반으로 하는지 확인합니다. 인증서를 두 번 클릭하고 **세부 정보** 탭에서 **확장된 키 사용** 을 확인하여 해당 인증서를 확인합니다.

* **자체 서명된 루트 인증서:** 다음 P2S 인증서 문서 중 하나의 단계에 따라 생성하는 클라이언트 인증서가 P2S 연결과 호환될 수 있도록 합니다.

  자체 서명된 루트 인증서에서 클라이언트 인증서를 생성하는 경우 이를 생성하는 데 사용한 컴퓨터에 자동으로 설치됩니다. 다른 클라이언트 컴퓨터에 클라이언트 인증서를 설치하려면 전체 인증서 체인과 함께 .pfx 파일로 내보냅니다. 이렇게 하면 클라이언트에서 인증하는 데 필요한 루트 인증서 정보가 포함된 .pfx 파일이 만들어집니다.

  이 문서의 단계를 통해 호환되는 클라이언트 인증서를 생성하고 이를 내보내어 배포할 수 있습니다.

  * [Windows 10 PowerShell 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md#clientcert): Windows 10 및 PowerShell에서 인증서를 생성해야 합니다. 생성된 인증서는 지원되는 모든 P2S 클라이언트에 설치할 수 있습니다.

  * [MakeCert 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md): 인증서를 생성할 Windows 10 컴퓨터에 대한 액세스 권한이 없는 경우 MakeCert를 사용합니다. MakeCert는 더 이상 사용되지 않지만, 인증서를 생성하는 데에는 여전히 사용할 수 있습니다. 생성된 인증서는 지원되는 모든 P2S 클라이언트에 설치할 수 있습니다.

  * [Linux 지침](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-linux.md).