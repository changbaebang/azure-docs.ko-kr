---
author: cephalin
ms.service: app-service-web
ms.topic: include
ms.date: 11/03/2016
ms.author: cephalin
ms.openlocfilehash: 2f490a5b12484a91e963d068810b292d7761521a
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "95986563"
---
> [!NOTE]
> Azure DNS를 사용하여 Azure App Service에 대한 사용자 지정 DNS 이름을 구성할 수 있습니다. 자세한 내용은 [Azure DNS를 사용하여 Azure 서비스에 대해 사용자 지정 도메인 설정 제공](../articles/dns/dns-custom-domain.md#app-service-web-apps)을 참조하세요.
>
>

1. 도메인 공급자의 웹 사이트에 로그인합니다.

1. DNS 레코드를 관리하기 위한 페이지를 찾습니다. 각 도메인 공급자마다 고유한 DNS 레코드 인터페이스가 있으므로 공급자의 설명서를 참조하세요. **도메인 이름**, **DNS** 또는 **이름 서버 관리** 라는 레이블이 지정된 사이트 영역을 찾습니다.

   종종 계정 정보를 확인한 다음, **내 도메인** 과 같은 링크를 검색하여 DNS 레코드 페이지를 찾을 수 있습니다. 해당 페이지로 이동한 다음, **영역 파일**, **DNS 레코드** 또는 **고급 구성** 과 같이 이름이 지정된 링크를 찾습니다.

   다음 스크린샷은 DNS 레코드 페이지의 예입니다.

   ![예제 DNS 레코드 페이지를 보여주는 스크린샷.](./media/app-service-web-access-dns-records-no-h/example-record-ui.png)

1. 예제 스크린샷에서 **추가** 를 선택하여 레코드를 만듭니다. 일부 공급자에는 다른 레코드 형식을 추가하는 다양한 링크가 있습니다. 다시 한 번 공급자의 설명서를 참조하세요.

> [!NOTE]
> GoDaddy와 같은 특정 공급자의 경우 먼저 별도의 **변경 내용 저장** 링크를 클릭해야 DNS 레코드의 변경 내용이 적용됩니다.
