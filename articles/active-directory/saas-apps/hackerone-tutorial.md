---
title: '자습서: HackerOne과 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 HackerOne 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/15/2019
ms.author: jeedes
ms.openlocfilehash: ac8bdc37bc2572b580deebc35931e324ed107d87
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92446576"
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a>자습서:Azure Active Directory와 HackerOne 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 HackerOne을 통합하는 방법에 대해 알아봅니다.
HackerOne을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* HackerOne에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 HackerOne에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 연결에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>사전 요구 사항

HackerOne과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* HackerOne Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* HackerOne에서 **SP** 시작 SSO를 지원합니다.
* HackerOne에서 **Just-In-Time** 사용자 프로비저닝을 지원합니다.

## <a name="adding-hackerone-from-the-gallery"></a>갤러리에서 HackerOne 추가

HackerOne의 Azure AD 통합을 구성하려면 갤러리의 HackerOne을 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 HackerOne을 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 옵션을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **HackerOne** 을 입력하고 결과 패널에서 **HackerOne** 을 선택한 다음, **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

     ![결과 목록의 HackerOne](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 HackerOne에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 HackerOne의 관련 사용자 간에 연결 관계를 설정해야 합니다.

HackerOne에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[HackerOne Single Sign-On 구성](#configure-hackerone-single-sign-on)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[HackerOne 테스트 사용자 만들기](#create-hackerone-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 HackerOne에 만듭니다.
6. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

HackerOne에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **HackerOne** 애플리케이션 통합 페이지에서 **Single Sign-On** 을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![HackerOne 도메인 및 URL Single Sign-On 정보](common/sp-identifier.png)

    a. **로그온 URL** 텍스트 상자에 다음(`https://hackerone.com/users/saml/sign_in?email=<configured domain>`)을 입력합니다.

    b. **식별자(엔터티 ID)** 텍스트 상자에 다음(`hackerone.com`)을 입력합니다.

5. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **HackerOne 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

### <a name="configure-hackerone-single-sign-on"></a>HackerOne Single Sign-On 구성

1. HackerOne 테넌트에 관리자로 로그온합니다.

2. 위쪽 메뉴에서 **설정** 을 클릭합니다.

    ![메뉴에서 선택한 "설정"을 보여주는 스크린샷.](./media/hackerone-tutorial/tutorial_hackerone_001.png)

3. **인증** 으로 이동하여 **SAML 설정 추가** 를 클릭합니다.

    !["SAML 설정 추가" 단추가 선택된 "인증 설정" 페이지를 보여주는 스크린샷.](./media/hackerone-tutorial/tutorial_hackerone_003.png)

4. **SAML 설정** 대화 상자에서 다음 단계를 수행합니다.

    ![Single Sign-on 구성](./media/hackerone-tutorial/tutorial_hackerone_004.png)

    a. **전자 메일 도메인** 텍스트 상자에 등록된 도메인을 입력합니다.

    b. **Single Sign-On URL** 텍스트 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.

    다. Azure Portal에서 다운로드한 **인증서 파일** 을 메모장에서 열고, 내용을 클립보드에 복사한 다음, **X509 인증서** 텍스트 상자에 붙여넣습니다.

    d. **저장** 을 클릭합니다.

5. 인증 설정 대화 상자에서 다음 단계를 수행합니다.

    !["테스트 실행" 단추가 선택된 "인증 설정" 대화 상자를 보여주는 스크린샷.](./media/hackerone-tutorial/tutorial_hackerone_005.png)

    a. **테스트 실행** 을 클릭합니다.

6. 테스트가 성공적으로 완료되고 **상태** 필드에 **마지막 테스트 상태: 성공** 이 표시되면 **요청 확인** 단추를 선택하여 승인을 위해 HackerOne에 제출합니다.

    ![승인을 위해 HackerOne에 제출](./media/hackerone-tutorial/tutorial-hackerone-006.png)

7. HackerOne에서 설정을 승인한 후 **사용자 마이그레이션** 단추를 선택하여 모든 사용자에 대해 SSO 인증을 요구할 수 있습니다.

    ![SAML 사용](./media/hackerone-tutorial/tutorial-hackerone-007.png)

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자** 를 차례로 선택하고 **모든 사용자** 를 선택합니다.

    !["사용자 및 그룹" 및 "모든 사용자" 링크](common/users.png)

2. 화면 위쪽에서 **새 사용자** 를 선택합니다.

    ![새 사용자 단추](common/new-user.png)

3. 사용자 속성에서 다음 단계를 수행합니다.

    ![사용자 대화 상자](common/user-properties.png)

    a. **이름** 필드에 **BrittaSimon** 을 입력합니다.

    b. **사용자 이름** 필드에 **brittasimon\@yourcompanydomain.extension** 을 입력합니다.  
    예를 들어 BrittaSimon@contoso.com

    다. **암호 표시** 확인란을 선택한 다음, [암호] 상자에 표시된 값을 적어둡니다.

    d. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 HackerOne에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택하고 **모든 애플리케이션** 을 선택한 다음, **HackerOne** 을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **HackerOne** 을 선택합니다.

    ![애플리케이션 목록의 HackerOne 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

    !["사용자 및 그룹" 링크](common/users-groups-blade.png)

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![할당 추가 창](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. SAML 어설션 및 **역할 선택** 대화 상자에서 모든 역할 값이 필요한 경우 목록에서 적절한 사용자 역할을 선택한 다음, 화면 맨 아래에 있는 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-hackerone-test-user"></a>HackerOne 테스트 사용자 만들기

이 섹션에서는 HackerOne에서 Britta Simon이라는 사용자를 만듭니다. HackerOne은 기본적으로 사용하도록 설정되는 Just-In-Time 사용자 프로비저닝을 지원합니다. 이 섹션에 작업 항목이 없습니다. HackerOne에 사용자가 아직 없는 경우 인증 후에 새 사용자가 만들어집니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 HackerOne 타일을 클릭하면 SSO를 설정한 HackerOne에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)