---
title: '자습서: Azure Active Directory와 Infogix Data3Sixty Govern 통합 | Microsoft Docs'
description: Azure Active Directory와 Infogix Data3Sixty Govern 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/14/2019
ms.author: jeedes
ms.openlocfilehash: 7ca566c554c02d20d21bd7eba87dfbcbf1f746da
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "97606490"
---
# <a name="tutorial-azure-active-directory-integration-with-infogix-data3sixty-govern"></a>자습서: Azure Active Directory와 Infogix Data3Sixty Govern 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Infogix Data3Sixty Govern을 통합하는 방법에 대해 알아봅니다.
Infogix Data3Sixty Govern을 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* Infogix Data3Sixty Govern에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 자신의 Azure AD 계정으로 자동으로 Infogix Data3Sixty Govern에 로그온(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 연결에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>사전 요구 사항

Infogix Data3Sixty Govern과 Azure AD의 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Infogix Data3Sixty Govern Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Infogix Data3Sixty Govern은 **SP 및 IDP** 시작 SSO를 지원합니다.
* Infogix Data3Sixty Govern은 **Just In Time** 프로비저닝을 지원합니다.

## <a name="adding-infogix-data3sixty-govern-from-the-gallery"></a>갤러리에서 Infogix Data3Sixty Govern 추가

Infogix Data3Sixty Govern과 Azure AD의 통합을 구성하려면 갤러리의 Infogix Data3Sixty Govern을 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Infogix Data3Sixty Govern을 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 옵션을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **Infogix Data3Sixty Govern** 을 입력하고 결과 패널에서 **Infogix Data3Sixty Govern** 을 선택한 후 **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

    ![결과 목록의 Infogix Data3Sixty Govern](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 Infogix Data3Sixty Govern에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 Infogix Data3Sixty Govern의 관련 사용자 간에 연결이 형성되어야 합니다.

Infogix Data3Sixty Govern에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Infogix Data3Sixty Govern Single Sign-On 구성](#configure-infogix-data3sixty-govern-single-sign-on)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Infogix Data3Sixty Govern 테스트 사용자 만들기](#create-infogix-data3sixty-govern-test-user)** - Azure AD의 Britta Simon과 연결된 Britta Simon에 해당하는 사용자를 Infogix Data3Sixty Govern에 만듭니다.
6. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

Infogix Data3Sixty Govern에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Infogix Data3Sixty Govern** 애플리케이션 통합 페이지에서 **Single Sign-On** 을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성 편집](common/edit-urls.png)

4. **IDP** 시작 모드에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![스크린샷은 식별자, 회신 URL을 입력하고 저장을 선택할 수 있는 기본 SAML 구성을 보여줍니다.](common/idp-intiated.png)

    a. **식별자** 텍스트 상자에 URL을 입력합니다. `https://data3sixty.com/ui`

    b. **회신 URL** 텍스트 상자에서 `https://<subdomain>.data3sixty.com/sso/acs` 패턴을 사용하여 URL을 입력합니다.

5. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    ![스크린샷은 로그온 URL을 입력할 수 있는 추가 URL 설정을 보여줍니다.](common/metadata-upload-additional-signon.png)

    **로그인 URL** 텍스트 상자에서 `https://<subdomain>.data3sixty.com` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 이 값을 얻으려면 [Infogix Data3Sixty Govern 클라이언트 지원 팀](mailto:data3sixtysupport@infogix.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

6. Infogix Data3Sixty Govern 애플리케이션은 특정 형식의 SAML 어설션이 필요합니다. 이 애플리케이션에 대해 다음 클레임을 구성합니다. 애플리케이션 통합 페이지의 **사용자 특성** 섹션에서 이러한 특성의 값을 관리할 수 있습니다. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 단추를 클릭하여 **사용자 특성** 대화 상자를 엽니다.

    ![스크린샷은 편집 아이콘이 선택된 사용자 특성을 보여줍니다.](common/edit-attribute.png)

7. 위의 이미지와 같이 SAML 토큰 특성을 구성하기 위해 **사용자 특성** 대화 상자의 **사용자 클레임** 섹션에서 **편집 아이콘** 을 사용하여 클레임을 편집하거나 **새 클레임 추가** 를 사용하여 클레임을 추가하고, 다음 단계를 수행합니다.

    | 속성 | 원본 특성|
    | -----------| -------------- |
    | firstname  | user.givenname |
    | lastname | user.surname |
    | 사용자 이름 | user.mail |

    a. **새 클레임 추가** 를 클릭하여 **사용자 클레임 관리** 대화 상자를 엽니다.

    ![스크린샷은 새 클레임을 추가하는 옵션이 있는 사용자 클레임을 보여줍니다.](common/new-save-attribute.png)

    ![스크린샷은 설명된 값을 입력할 수 있는 사용자 클레임 관리 대화 상자를 보여줍니다.](common/new-attribute-details.png)

    b. **이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.

    다. **네임스페이스** 를 비워 둡니다.

    d. 원본을 **특성** 으로 선택합니다.

    e. **원본 특성** 목록에서 해당 행에 표시된 특성 값을 입력합니다.

    f. **확인** 을 클릭합니다.

    g. **저장** 을 클릭합니다.

8. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(원시)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificateraw.png)

9. **Infogix Data3Sixty Govern 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

### <a name="configure-infogix-data3sixty-govern-single-sign-on"></a>Infogix Data3Sixty Govern Single Sign-On 구성

**Infogix Data3Sixty Govern** 쪽에서 Single Sign-On을 구성하려면 Azure Portal에서 다운로드한 **인증서(원시)** 및 적절히 복사한 URL을 [Infogix Data3Sixty Govern 지원 팀](mailto:data3sixtysupport@infogix.com)으로 보내야 합니다. 이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기 

이 섹션의 목적은 Azure Portal에서 Britta Simon이라는 테스트 사용자를 만드는 것입니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자** 를 차례로 선택하고 **모든 사용자** 를 선택합니다.

    !["사용자 및 그룹" 및 "모든 사용자" 링크](common/users.png)

2. 화면 위쪽에서 **새 사용자** 를 선택합니다.

    ![새 사용자 단추](common/new-user.png)

3. 사용자 속성에서 다음 단계를 수행합니다.

    ![사용자 대화 상자](common/user-properties.png)

    a. **이름** 필드에 **BrittaSimon** 을 입력합니다.

    b. **사용자 이름** 필드에 **brittasimon@yourcompanydomain.extension** 을 입력합니다.  
    예를 들어 BrittaSimon@contoso.com

    다. **암호 표시** 확인란을 선택한 다음, [암호] 상자에 표시된 값을 적어둡니다.

    d. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Infogix Data3Sixty Govern에 대한 액세스 권한을 부여하여 Britta Simon이 Azure Single Sign-On을 사용할 수 있도록 합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**, **모든 애플리케이션**, **Infogix Data3Sixty Govern** 을 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **Infogix Data3Sixty Govern** 를 선택합니다.

    ![애플리케이션 목록의 Infogix Data3Sixty Govern 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

    !["사용자 및 그룹" 링크](common/users-groups-blade.png)

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![할당 추가 창](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. SAML 어설션 및 **역할 선택** 대화 상자에서 모든 역할 값이 필요한 경우 목록에서 적절한 사용자 역할을 선택한 다음, 화면 맨 아래에 있는 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-infogix-data3sixty-govern-test-user"></a>Infogix Data3Sixty Govern 테스트 사용자 만들기

이 섹션에서는 Infogix Data3Sixty Govern에서 Britta Simon이라는 사용자를 만듭니다. Infogix Data3Sixty Govern은 Just-In-Time 프로비저닝을 지원하며, 기본적으로 사용하도록 설정되어 있습니다. 이 섹션에 작업 항목이 없습니다. Infogix Data3Sixty Govern에 사용자가 아직 없는 경우 인증 후에 새 사용자가 만들어집니다.

> [!Note]
> 사용자를 수동으로 만들어야 하는 경우 [Infogix Data3Sixty Govern 지원 팀](mailto:data3sixtysupport@infogix.com)에 문의하세요.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Infogix Data3Sixty Govern 타일을 클릭하면 SSO를 설정한 Infogix Data3Sixty Govern에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)