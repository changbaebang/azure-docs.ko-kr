---
title: '자습서: Envi MMIS와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Envi MMIS 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/06/2019
ms.author: jeedes
ms.openlocfilehash: 6ccf755a73cafa4b855f602aa18246d710e5e1ff
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92454014"
---
# <a name="tutorial-azure-active-directory-integration-with-envi-mmis"></a>자습서: Envi MMIS와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Envi MMIS를 통합하는 방법에 대해 알아봅니다.
Envi MMIS를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* Envi MMIS에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 자신의 Azure AD 계정으로 Envi MMIS에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 연결에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>사전 요구 사항

Envi MMIS와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Envi MMIS Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Envi MMIS에서 **SP** 및 **IDP** 시작 SSO를 지원합니다.

## <a name="adding-envi-mmis-from-the-gallery"></a>갤러리에서 Envi MMIS 추가

Envi MMIS의 Azure AD 통합을 구성하려면 갤러리의 Envi MMIS를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Envi MMIS를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 옵션을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **Envi MMIS** 를 입력하고 결과 패널에서 **Envi MMIS** 를 선택한 후 **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

     ![결과 목록의 Envi MMIS](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 Envi MMIS에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 Envi MMIS의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Envi MMIS에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Envi MMIS Single Sign-On 구성](#configure-envi-mmis-single-sign-on)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Envi MMIS 테스트 사용자 만들기](#create-envi-mmis-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 Envi MMIS에 만듭니다.
6. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

Envi MMIS에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Envi MMIS** 애플리케이션 통합 페이지에서 **Single Sign-On** 을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성 편집](common/edit-urls.png)

4. **IDP** 시작 모드에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    !["식별자", "회신 URL" 및 "저장" 단추가 강조 표시된 "기본 SAML 구성"을 보여주는 스크린샷.](common/idp-intiated.png)

    a. **식별자** 텍스트 상자에서 `https://www.<CUSTOMER DOMAIN>.com/Account` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://www.<CUSTOMER DOMAIN>.com/Account/Acs` 패턴을 사용하여 URL을 입력합니다.

5. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    ![Envi MMIS 도메인 및 URL Single Sign-On 정보](common/metadata-upload-additional-signon.png)

    **로그인 URL** 텍스트 상자에서 `https://www.<CUSTOMER DOMAIN>.com/Account` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 이러한 값을 얻으려면 [Envi MMIS 클라이언트 지원 팀](mailto:support@ioscorp.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

6. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **페더레이션 메타데이터 XML** 을 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

7. **Envi MMIS 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

### <a name="configure-envi-mmis-single-sign-on"></a>Envi MMIS Single Sign-On 구성

1. 다른 웹 브라우저 창에서 Envi MMIS 회사 사이트에 관리자로 로그인합니다.

2. **내 도메인** 탭을 클릭합니다.

    !["내 도메인"이 선택된 "사용자" 메뉴를 보여주는 스크린샷.](./media/envimmis-tutorial/configure1.png)

3. **편집** 을 클릭합니다.

    ![선택된 "편집" 단추를 보여주는 스크린샷.](./media/envimmis-tutorial/configure2.png)

4. **원격 인증 사용** 확인란을 선택한 다음, **인증 형식** 드롭다운에서 **HTTP 리디렉션** 을 선택합니다.

    !["원격 인증 사용" 확인란이 선택되고 "HTTP 리디렉션"이 선택된 "세부 정보" 탭을 보여주는 스크린샷.](./media/envimmis-tutorial/configure3.png)

5. **리소스** 탭을 선택한 다음, **메타데이터 업로드** 를 클릭합니다.

    !["메타데이터 업로드" 작업이 선택된 "리소스" 탭을 보여주는 스크린샷.](./media/envimmis-tutorial/configure4.png)

6. **메타데이터 업로드** 팝업에서 다음 단계를 수행합니다.

    !["파일" 옵션이 선택되고 "파일 선택" 아이콘과 "확인" 단추가 강조 표시된 "메타데이터 업로드" 팝업을 보여주는 스크린샷.](./media/envimmis-tutorial/configure5.png)

    a. **업로드 위치** 드롭다운에서 **파일** 옵션을 선택합니다.

    b. **파일 선택 아이콘** 을 선택하여 Azure Portal에서 다운로드한 메타데이터 파일을 업로드합니다.

    다. **Ok** 를 클릭합니다.

7. 다운로드한 메타데이터 파일을 업로드하면 필드가 자동으로 채워집니다. **업데이트** 를 클릭합니다.

    ![Single Sign-On 구성 저장 단추](./media/envimmis-tutorial/configure6.png)

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Envi MMIS에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**, **모든 애플리케이션**, **Envi MMIS** 를 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **Envi MMIS** 를 선택합니다.

    ![애플리케이션 목록의 Envi MMIS 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

    !["사용자 및 그룹" 링크](common/users-groups-blade.png)

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![할당 추가 창](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. SAML 어설션에서 역할 값이 필요한 경우 **역할 선택** 대화 상자에서 목록에서 사용자에 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-envi-mmis-test-user"></a>Envi MMIS 테스트 사용자 만들기

Azure AD 사용자가 Envi MMIS에 로그인할 수 있도록 하려면 Envi MMIS로 프로비저닝되어야 합니다. Envi MMIS의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. Envi MMIS 회사 사이트에 관리자 권한으로 로그인합니다.

2. **사용자 목록** 탭을 클릭합니다.

    !["사용자 목록"이 선택된 "사용자" 메뉴를 보여주는 스크린샷.](./media/envimmis-tutorial/user1.png)

3. **사용자 추가** 단추를 클릭합니다.

    !["사용자 추가" 단추가 선택된 "사용자" 섹션을 보여주는 스크린샷.](./media/envimmis-tutorial/user2.png)

4. **사용자 추가** 섹션에서 다음 단계를 수행합니다.

    ![직원 추가](./media/envimmis-tutorial/user3.png)

    a. **사용자 이름** 텍스트 상자에 Britta Simon 계정의 사용자 이름(예: **brittasimon\@contoso.com**)을 입력합니다.
    
    b. **이름** 텍스트 상자에 BrittaSimon의 이름(예: **Britta**)을 입력합니다.

    다. **성** 텍스트 상자에 BrittaSimon의 성(예: **Simon**)을 입력합니다.

    d. 텍스트 상자의 **직함** 에 사용자의 직함을 입력합니다.
    
    e. **이메일 주소** 텍스트 상자에 Britta Simon 계정의 이메일 주소(예: **brittasimon\@contoso.com**)를 입력합니다.

    f. **SSO 사용자 이름** 텍스트 상자에 Britta Simon 계정의 사용자 이름(예: **brittasimon\@contoso.com**)을 입력합니다.

    g. **저장** 을 클릭합니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트 

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Envi MMIS 타일을 클릭하면 SSO를 설정한 Envi MMIS에 자동으로 로그인되어야 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)