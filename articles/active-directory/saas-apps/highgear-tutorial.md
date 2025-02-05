---
title: '자습서: HighGear와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 HighGear 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/16/2019
ms.author: jeedes
ms.openlocfilehash: b3806d768e8335801e2dd097eac7a440b157de38
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92444709"
---
# <a name="tutorial-azure-active-directory-integration-with-highgear"></a>자습서: HighGear와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 HighGear를 통합하는 방법에 대해 알아봅니다.
HighGear를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* HighGear에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 HighGear에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 연결에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>사전 요구 사항

HighGear와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Enterprise 또는 Unlimited 라이선스의 HighGear 시스템

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 알아봅니다.

* HighGear에서 **SP 및 IdP** 시작 SSO를 지원합니다.

## <a name="adding-highgear-from-the-gallery"></a>갤러리에서 HighGear 추가

HighGear의 Azure AD 통합을 구성하려면 갤러리에서 HighGear를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 HighGear를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 패널에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 옵션을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **HighGear** 를 입력하고, 결과 패널에서 **HighGear** 를 선택한 다음, **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

     ![결과 목록의 HighGear](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 HighGear 시스템에서 Azure AD Single Sign-On을 구성하고 테스트하는 방법을 알아봅니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 HighGear 시스템의 관련 사용자 간에 연결 관계를 설정해야 합니다.

HighGear 시스템에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[HighGear Single Sign-On 구성](#configure-highgear-single-sign-on)** - HighGear 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[HighGear 테스트 사용자 만들기](#create-highgear-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 HighGear에 만듭니다. 
6. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정하는 방법을 알아봅니다.

HighGear 시스템에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **HighGear** 애플리케이션 통합 페이지에서 **Single Sign-On** 을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![스크린샷은 식별자, 회신 URL을 입력하고 저장을 선택할 수 있는 기본 SAML 구성을 보여줍니다.](common/idp-intiated.png)

    a. **식별자** 텍스트 상자에 HighGear 시스템의 Single Sign-On 설정 페이지에 있는 **서비스 공급 기업 엔터티 ID** 필드의 값을 붙여넣습니다.

    ![서비스 공급 기업 엔터티 ID 필드](media/highgear-tutorial/service-provider-entity-id-field.png)
    
    > [!NOTE]
    > Single Sign-On 설정 페이지에 액세스하려면 HighGear 시스템에 로그인해야 합니다. 로그인하고 나면 HighGear에서 관리 탭 위로 마우스를 이동한 후 Single Sign-On 설정 메뉴 항목을 클릭합니다.
    
    ![Single Sign-On 설정 메뉴 항목](media/highgear-tutorial/single-sign-on-settings-menu-item.png)

    b. **회신 URL** 텍스트 상자에 HighGear 시스템의 Single Sign-On 설정 페이지에 있는 **ACS(Assertion Consumer Service) URL** 의 값을 붙여넣습니다.

    ![ACS(Assertion Consumer Service) URL 필드](media/highgear-tutorial/assertion-consumer-service-url-field.png)

    다. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

     ![스크린샷은 로그온 URL을 입력할 수 있는 추가 URL 설정을 보여줍니다.](common/metadata-upload-additional-signon.png)

     **로그온 URL** 텍스트 상자에 HighGear 시스템의 Single Sign-On 설정 페이지에 있는 **서비스 공급 기업 엔터티 ID** 필드의 값을 붙여넣습니다. (이 엔터티 ID는 SP 시작 로그온에 사용되는 HighGear 시스템의 기본 URL이기도 합니다.)

    ![서비스 공급 기업 엔터티 ID 필드](media/highgear-tutorial/service-provider-entity-id-field.png)

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 이 값을 HighGear 시스템의 **Single Sign-On 설정** 페이지에 있는 실제 식별자, 회신 URL 및 로그온 URL로 업데이트합니다. 도움이 필요한 경우 [HighGear 지원팀](mailto:support@highgear.com)에 문의하세요.

4. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 **인증서(Base64)** 를 컴퓨터에 다운로드하고 저장합니다. Single Sign-On 구성의 이후 단계에서 필요합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **HighGear 설정** 섹션에서 다음 URL의 위치를 확인하세요.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL. 아래 **HighGear Single Sign-On 구성** 의 2단계에서 이 값이 필요합니다.

    b. Azure AD 식별자. 아래 **HighGear Single Sign-On 구성** 의 3단계에서 이 값이 필요합니다.

    다. 로그아웃 URL. 아래 **HighGear Single Sign-On 구성** 의 4단계에서 이 값이 필요합니다.

### <a name="configure-highgear-single-sign-on"></a>HighGear Single Sign-On 구성

Single Sign-On을 위해 HighGear를 구성하려면 HighGear 시스템에 로그인하세요. 로그인하고 나면 HighGear에서 관리 탭 위로 마우스를 이동한 후 Single Sign-On 설정 메뉴 항목을 클릭합니다.

![Single Sign-On 설정 메뉴 항목](media/highgear-tutorial/single-sign-on-settings-menu-item.png)

1. **ID 공급 기업 이름** 에서 로그인 페이지의 HighGear Single Sign-On 단추에 표시되는 간단한 설명을 입력합니다. 다음은 그 예입니다.  Azure AD

2. HighGear의 **SSO(Single Sign-On) URL** 필드에서 Azure의 **HighGear 설정** 섹션에 있는 **로그인 URL** 필드의 값을 붙여넣습니다.

3. HighGear의 **ID 공급 기업 엔터티 ID** 필드에서 Azure의 **HighGear 설정** 섹션에 있는 **Azure AD 식별자** 필드의 값을 붙여넣습니다.

4. HighGear의 **SLO(단일 로그아웃) URL** 필드에서 Azure의 **HighGear 설정** 섹션에 있는 **로그아웃 URL** 필드의 값을 붙여넣습니다.

5. 메모장을 사용하여 Azure의 **SAML 서명 인증서** 섹션에서 다운로드한 인증서를 엽니다. **인증서(Base64)** 형식을 다운로드해야 합니다. 메모장에서 인증서의 콘텐츠를 복사하고 HighGear의 **ID 공급 기업 인증서** 필드에 붙여넣습니다.

6. HighGear 인증서를 요청하는 이메일을 [HighGear 지원팀](mailto:support@highgear.com)에게 보냅니다. 지원팀으로부터 받은 지침에 따라 **HighGear 인증서** 및 **HighGear 인증서 암호** 필드를 입력합니다.

7. **저장** 단추를 클릭하여 HighGear Single Sign-On 구성을 저장합니다.

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

    다. **암호 표시** 확인란을 선택한 다음, 암호 상자에 표시된 값을 적어둡니다.

    d. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 HighGear에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**, **모든 애플리케이션**, **HighGear** 를 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **HighGear** 를 선택합니다.

    ![애플리케이션 목록의 HighGear 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

    !["사용자 및 그룹" 링크](common/users-groups-blade.png)

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![할당 추가 창](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. SAML 어설션 및 **역할 선택** 대화 상자에서 모든 역할 값이 필요한 경우 목록에서 적절한 사용자 역할을 선택한 다음, 화면 맨 아래에 있는 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-highgear-test-user"></a>HighGear 테스트 사용자 만들기

Single Sign-On 구성을 테스트하기 위해 HighGear 테스트 사용자를 만들려면 HighGear 시스템에 로그인합니다.

1. **새 연락처 만들기** 단추를 클릭합니다.

    ![새 연락처 만들기 단추](media/highgear-tutorial/create-new-contact-button.png)

    만들려는 연락처의 종류를 선택할 수 있는 메뉴가 표시됩니다.

2. **개별** 메뉴 항목을 클릭하여 HighGear 사용자를 만듭니다.

    창이 오른쪽으로 슬라이드 아웃되면 새 사용자에 대한 정보를 입력할 수 있습니다.  
    ![새 연락처 양식](media/highgear-tutorial/new-contact-form.png)

3. **이름** 필드에서 컨테이너의 이름을 입력합니다. 다음은 그 예입니다.  Britta Simon

4. **기타 옵션** 메뉴를 클릭하고 **계정 정보** 메뉴 항목을 선택합니다.

    ![계정 정보 메뉴 항목 클릭](media/highgear-tutorial/account-info-menu-item.png)

5. **로그인 가능** 필드를 예로 설정합니다.

    **Single Sign-On 설정** 필드도 자동으로 예로 설정됩니다.

6. **Single Sign-On 사용자 ID** 필드에서 사용자의 ID를 입력합니다. 예: BrittaSimon@contoso.com

    계정 정보 섹션이 다음과 같이 표시됩니다.  
    ![완료된 계정 정보 섹션](media/highgear-tutorial/finished-account-info-section.png)

7. 연락처를 저장하려면 창 아래쪽에 있는 **저장** 단추를 클릭합니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트 

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 HighGear 타일을 클릭하면 SSO를 설정한 HighGear에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)