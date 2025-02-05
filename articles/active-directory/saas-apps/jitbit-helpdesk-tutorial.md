---
title: '자습서: Jitbit Helpdesk와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 Jitbit Helpdesk 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/02/2021
ms.author: jeedes
ms.openlocfilehash: b3fbf73ab51092f614a416355477fc552a404fd3
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104581810"
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a>자습서: Jitbit Helpdesk와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Jitbit Helpdesk를 통합하는 방법에 대해 알아봅니다. Azure AD와 Jitbit Helpdesk를 통합하면 다음을 수행할 수 있습니다.

* Jitbit Helpdesk에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 Jitbit Helpdesk에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Jitbit Helpdesk SSO(Single Sign-On)가 설정된 구독.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Jitbit Helpdesk는 **SP** 시작 SSO를 지원합니다.

> [!NOTE]
> 이 애플리케이션의 식별자는 고정 문자열 값이므로 하나의 테넌트에서 하나의 인스턴스만 구성할 수 있습니다.

## <a name="add-jitbit-helpdesk-from-the-gallery"></a>갤러리에서 Jitbit Helpdesk 추가

Jitbit Helpdesk의 Azure AD 통합을 구성하려면 갤러리의 Jitbit Helpdesk를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Jitbit Helpdesk** 를 입력합니다.
1. 결과 패널에서 **Jitbit Helpdesk** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-jitbit-helpdesk"></a>Jitbit Helpdesk에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Jitbit Helpdesk에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Jitbit Helpdesk의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Jitbit Helpdesk에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Jitbit Helpdesk SSO 구성](#configure-jitbit-helpdesk-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Jitbit Helpdesk 테스트 사용자 만들기](#create-jitbit-helpdesk-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Jitbit Helpdesk에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Jitbit Helpdesk** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    a. **로그온 URL** 텍스트 상자에서 다음 패턴을 사용하여 URL 중 하나를 입력합니다.
    | |
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > 이 값은 실제 값이 아닙니다. 이 값을 실제 로그온 URL로 업데이트합니다. 이 값을 얻으려면 [Jitbit Helpdesk 클라이언트 지원 팀](https://www.jitbit.com/support/)에 문의하세요.

    b. **식별자(엔터티 ID)** 텍스트 상자에 `https://www.jitbit.com/web-helpdesk/` URL을 입력합니다.

5. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **Jitbit Helpdesk 설정** 섹션에서 요구 사항에 해당하는 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션에서는 Azure Portal에서 B.Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자**, **모든 사용자** 를 차례로 선택합니다.
1. 화면 위쪽에서 **새 사용자** 를 선택합니다.
1. **사용자** 속성에서 다음 단계를 수행합니다.
   1. **이름** 필드에 `B.Simon`을 입력합니다.  
   1. **사용자 이름** 필드에서 username@companydomain.extension을 입력합니다. 예들 들어 `B.Simon@contoso.com`입니다.
   1. **암호 표시** 확인란을 선택한 다음, **암호** 상자에 표시된 값을 적어둡니다.
   1. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Jitbit Helpdesk에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Jitbit Helpdesk** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-jitbit-helpdesk-sso"></a>Jitbit Helpdesk SSO 구성

1. 다른 웹 브라우저 창에서 Jitbit Helpdesk 회사 사이트에 관리자로 로그인합니다.

1. 위쪽의 도구 모음에서 **관리** 를 클릭합니다.

    ![관리](./media/jitbit-helpdesk-tutorial/settings.png "관리")

1. **일반 설정** 을 클릭합니다.

    ![스크린샷은 일반 설정 링크를 보여줍니다.](./media/jitbit-helpdesk-tutorial/general.png "사용자, 회사 및 사용 권한")

1. **인증 설정** 구성 섹션에서 다음 단계를 수행합니다.

    ![인증 설정](./media/jitbit-helpdesk-tutorial/authentication.png "인증 설정")

    a. **OneLogin** 과 함께 SSO(Single Sign-On)를 사용하여 로그인하려면 **SAML 2.0 Single Sign On 사용** 을 선택합니다.

    b. **엔드포인트 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.

    다. **Base-64** 로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음, **X.509 인증서** 텍스트 상자에 붙여넣습니다.

    d. **변경 내용 저장** 을 클릭합니다.

### <a name="create-jitbit-helpdesk-test-user"></a>Jitbit Helpdesk 테스트 사용자 만들기

Azure AD 사용자가 Jitbit Helpdesk에 로그인할 수 있도록 하려면 Jitbit Helpdesk로 프로비저닝되어야 합니다. Jitbit Helpdesk의 경우 프로비저닝은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. **Jitbit Helpdesk** 테넌트에 로그인합니다.

1. 위쪽의 메뉴에서 **관리** 를 클릭합니다.

    ![관리](./media/jitbit-helpdesk-tutorial/settings.png "관리")

1. **사용자, 회사 및 사용 권한** 을 클릭합니다.

    ![사용자, 회사 및 사용 권한](./media/jitbit-helpdesk-tutorial/users.png "사용자, 회사 및 사용 권한")

1. **사용자 추가** 를 클릭합니다.

    ![사용자 추가](./media/jitbit-helpdesk-tutorial/add.png "사용자 추가")

1. 만들기 섹션에 프로비전하려는 Azure AD 계정의 데이터를 다음과 같이 입력합니다.

    ![만들기](./media/jitbit-helpdesk-tutorial/create-section.png "생성")

   a. **사용자 이름** 텍스트 상자에 사용자의 이름(예: **BrittaSimon**)을 입력합니다.

   b. **메일** 텍스트 상자에 사용자의 메일 주소(예: **BrittaSimon@contoso.com** )를 입력합니다.

   다. **이름** 텍스트 상자에 사용자의 이름(예: **Britta**)을 입력합니다.

   d. **성** 텍스트 상자에 사용자의 성(예: **Simon**)을 입력합니다.

   e. **만들기** 를 클릭합니다.

> [!NOTE]
> 다른 Jitbit Helpdesk 사용자 계정 생성 도구 또는 Jitbit Helpdesk가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Jitbit Helpdesk 로그온 URL로 리디렉션됩니다. 

* Jitbit Helpdesk 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Jitbit Helpdesk 타일을 클릭하면 Jitbit Helpdesk 로그온 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Jitbit Helpdesk가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).