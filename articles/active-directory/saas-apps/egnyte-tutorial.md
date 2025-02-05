---
title: '자습서: Egnyte와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 Egnyte 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/27/2020
ms.author: jeedes
ms.openlocfilehash: 3d102b492326971ef186ba50a557ad8d1df5b6ec
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92454201"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-egnyte"></a>자습서: Egnyte와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Egnyte를 통합하는 방법에 대해 알아봅니다. Egnyte를 Azure AD와 통합하면 다음을 수행할 수 있습니다.

* Azure AD에서 Egnyte에 대한 액세스 권한이 있는 사용자를 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 Egnyte에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Egnyte SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Egnyte에서 **SP** 시작 SSO를 지원합니다.
* Egnyte를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)

> [!NOTE]
> 이 애플리케이션의 식별자는 고정 문자열 값이므로 하나의 테넌트에서 하나의 인스턴스만 구성할 수 있습니다.

## <a name="adding-egnyte-from-the-gallery"></a>갤러리에서 Egnyte 추가

Egnyte의 Azure AD 통합을 구성하려면 갤러리의 Egnyte를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Egnyte** 를 입력합니다.
1. 결과 패널에서 **Egnyte** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso"></a>Azure AD SSO 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 Egnyte에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 Egnyte의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Egnyte에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

Egnyte에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Egnyte SSO 구성](#configure-egnyte-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Egnyte 테스트 사용자 만들기](#create-egnyte-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Egnyte에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Egnyte** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![Egnyte 도메인 및 URL Single Sign-On 정보](common/sp-signonurl.png)

    a. **로그인 URL** 텍스트 상자에서 `https://<companyname>.egnyte.com` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<companyname>.egnyte.com/samlconsumer/AzureAD` 패턴을 사용하여 URL을 입력합니다.
    
    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 로그온 URL 및 회신 URL로 값을 업데이트합니다. 이 값을 얻으려면 [Egnyte 클라이언트 지원 팀](https://www.egnyte.com/corp/contact_egnyte.html)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

4. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

5. **Egnyte 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Egnyte에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Egnyte** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-egnyte-sso"></a>Egnyte SSO 구성

1. 다른 웹 브라우저 창에서 Egnyte 회사 사이트에 관리자로 로그인합니다.

2. **설정** 을 클릭합니다.
   
    ![설정 1](./media/egnyte-tutorial/ic787819.png "설정")

3. 메뉴에서 **설정** 을 클릭합니다.

    ![설정](./media/egnyte-tutorial/ic787820.png "설정")

4. **구성** 탭을 클릭한 다음 **보안** 을 클릭합니다.

    ![보안](./media/egnyte-tutorial/ic787821.png "보안")

5. **Single Sign-On 인증** 섹션에서 다음 단계를 수행합니다.

    ![Single Sign On 인증](./media/egnyte-tutorial/ic787822.png "Single Sign On 인증")   
    
    a. **Single Sign-On 인증** 으로 **SAML 2.0** 을 선택합니다.
   
    b. **ID 공급자** 로 **AzureAD** 를 선택합니다.
   
    다. Azure Portal에서 복사한 **로그인 URL** 을 **ID 공급자 로그인 URL** 텍스트 상자에 붙여 넣습니다.
   
    d. Azure Portal에서 복사한 **Azure AD 식별자** 를 **ID 공급자 엔터티 ID** 텍스트 상자에 붙여 넣습니다.
      
    e. Azure Portal에서 다운로드한 base-64로 인코딩된 인증서를 메모장에서 열고, 콘텐츠를 클립보드에 복사한 다음, **ID 공급자 인증서** 텍스트 상자에 붙여넣습니다.
   
    f. **기본 사용자 매핑** 으로 **전자 메일 주소** 를 선택합니다.
   
    g. **도메인별 발급자 값 사용** 으로 **사용 안 함** 을 선택합니다.
   
    h. **저장** 을 클릭합니다.

### <a name="create-egnyte-test-user"></a>Egnyte 테스트 사용자 만들기

Azure AD 사용자가 Egnyte에 로그인할 수 있도록 하려면 Egnyte로 프로비저닝되어야 합니다. Egnyte의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비저닝하려면 다음 단계를 수행합니다.**

1. **Egnyte** 회사 사이트에 관리자 권한으로 로그인합니다.

2. **설정 \> 사용자 및 그룹** 으로 이동합니다.

3. **새 사용자 추가** 를 클릭한 다음 추가할 사용자의 유형을 선택합니다.
   
    ![사용자](./media/egnyte-tutorial/ic787824.png "사용자")

4. **새 고급 사용자** 섹션에서 다음 단계를 수행합니다.
    
    ![새 표준 사용자](./media/egnyte-tutorial/ic787825.png "새 표준 사용자")   

    a. **이메일** 텍스트 상자에 사용자의 이메일 주소(예: **Brittasimon\@contoso.com**)를 입력합니다.

    b. **사용자 이름** 텍스트 상자에 사용자 이름(예: **Brittasimon**)을 입력합니다.

    다. **인증 유형** 으로 **Single Sign On** 을 선택합니다.
   
    d. **저장** 을 클릭합니다.
    
    >[!NOTE]
    >Azure Active Directory 계정 소유자는 알림 전자 메일을 받습니다.
    >

>[!NOTE]
>다른 Egnyte 사용자 계정 생성 도구 또는 Egnyte가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비저닝할 수 있습니다.
>

### <a name="test-sso"></a>SSO 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Egnyte 타일을 클릭하면 SSO를 설정한 Egnyte에 자동으로 로그인되어야 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)

- [Microsoft Cloud App Security의 세션 제어란?](/cloud-app-security/proxy-intro-aad)