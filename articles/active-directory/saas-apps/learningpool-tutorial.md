---
title: '자습서: Learningpool Act와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory와 Learningpool Act 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/25/2019
ms.author: jeedes
ms.openlocfilehash: eb8d0c229ed5f41dcb5999243a57ee19c2b67f74
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92458730"
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a>자습서: Learningpool Act와 Azure Active Directory 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Learningpool Act를 통합하는 방법에 대해 알아봅니다.
Learningpool Act를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* Learningpool Act에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 Learningpool Act에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

Azure AD와의 SaaS 앱 연결에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On](../manage-apps/what-is-single-sign-on.md)을 참조하세요.
Azure 구독이 아직 없는 경우 시작하기 전에 [체험](https://azure.microsoft.com/free/) 계정을 만듭니다.

## <a name="prerequisites"></a>필수 구성 요소

Learningpool Act와 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 구할 수 있습니다.
* Learningpool Act Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* Learningpool Act에서 **SP** 시작 SSO를 지원합니다.

## <a name="adding-learningpool-act-from-the-gallery"></a>갤러리에서 Learningpool Act 추가

Learningpool Act와 Azure AD의 통합을 구성하려면 갤러리의 Learningpool Act를 관리되는 SaaS 앱 목록에 추가해야 합니다.

**갤러리에서 Learningpool Act를 추가하려면 다음 단계를 수행합니다.**

1. **[Azure Portal](https://portal.azure.com)** 의 왼쪽 탐색 창에서 **Azure Active Directory** 아이콘을 클릭합니다.

    ![Azure Active Directory 단추](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 옵션을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 단추를 클릭합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **Learningpool Act** 를 입력하고 결과 패널에서 **Learningpool Act** 를 선택한 다음, **추가** 단추를 클릭하여 애플리케이션을 추가합니다.

     ![결과 목록의 Learningpool Act](common/search-new-app.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 Learningpool Act에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 Learningpool Act의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Learningpool Act에서 Azure AD Single Sign-On을 구성하고 테스트하려면 다음 구성 요소를 완료해야 합니다.

1. **[Azure AD Single Sign-On 구성](#configure-azure-ad-single-sign-on)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Learningpool Act Single Sign-On 구성](#configure-learningpool-act-single-sign-on)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
5. **[Learningpool Act 테스트 사용자 만들기](#create-learningpool-act-test-user)** - Britta Simon의 Azure AD 표현과 연결되는 대응 사용자를 Learningpool Act에 만듭니다.
6. **[Single Sign-On 테스트](#test-single-sign-on)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성

이 섹션에서는 Azure Portal에서 Azure AD Single Sign-On을 사용하도록 설정합니다.

Learningpool Act에서 Azure AD Single Sign-On을 구성하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Learningpool Act** 애플리케이션 통합 페이지에서 **Single Sign-On** 을 선택합니다.

    ![Single Sign-On 구성 링크](common/select-sso.png)

2. **Single Sign-On 방법 선택** 대화 상자에서 **SAML/WS-Fed** 모드를 선택하여 Single Sign-On을 사용하도록 설정합니다.

    ![Single Sign-On 선택 모드](common/select-saml-option.png)

3. **SAML로 Single Sign-On 설정** 페이지에서 **편집** 아이콘을 클릭하여 **기본 SAML 구성** 대화 상자를 엽니다.

    ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    ![Learningpool Act 도메인 및 URL Single Sign-On 정보](common/sp-identifier.png)

    a. **로그온 URL** 텍스트 상자에 `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php` URL을 입력합니다.

    b. **식별자(엔터티 ID)** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다.
    
    ```http
    https://<subdomain>.Learningpool.com/shibboleth
    https://<subdomain>.preview.Learningpool.com/shibboleth
    ```

    > [!NOTE]
    > 식별자 값은 실제 값이 아닙니다. 실제 식별자로 이 값을 업데이트하세요. 이러한 값을 얻으려면 [Learningpool Act 클라이언트 지원 팀](https://www.learningpool.com/support)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

5. Learningpool Act 애플리케이션은 특정 서식에서 SAML 어설션을 예상하며, 이는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다. **편집** 아이콘을 클릭하여 사용자 특성 대화 상자를 엽니다.

    ![스크린샷은 편집 아이콘이 선택된 사용자 특성을 보여줍니다.](common/edit-attribute.png)

6. 위의 이미지와 같이 SAML 토큰 특성을 구성하기 위해 **사용자 특성** 대화 상자의 **사용자 클레임** 섹션에서 **편집 아이콘** 을 사용하여 클레임을 편집하거나 **새 클레임 추가** 를 사용하여 클레임을 추가하고, 다음 단계를 수행합니다. 

    | 속성 | 원본 특성|
    | ------------------- | -------------------- |
    | urn:oid:1.2.840.113556.1.4.221 | user.userprincipalname |
    | urn:oid:2.5.4.42 | user.givenname |
    | urn:oid:0.9.2342.19200300.100.1.3 | user.mail |
    | urn:oid:2.5.4.4 | user.surname |
    | | |

    a. **새 클레임 추가** 를 클릭하여 **사용자 클레임 관리** 대화 상자를 엽니다.

    ![스크린샷은 새 클레임을 추가하는 옵션이 있는 사용자 클레임을 보여줍니다.](common/new-save-attribute.png)

    ![스크린샷은 설명된 값을 입력할 수 있는 사용자 클레임 관리 대화 상자를 보여줍니다.](common/new-attribute-details.png)

    b. **이름** 텍스트 상자에서 해당 행에 표시된 특성 이름을 입력합니다.

    다. **네임스페이스** 를 비워 둡니다.

    d. 원본을 **특성** 으로 선택합니다.

    e. **원본 특성** 목록에서 해당 행에 표시된 특성 값을 입력합니다.

    f. **확인** 을 클릭합니다.

    g. **저장** 을 클릭합니다.

7. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **페더레이션 메타데이터 XML** 을 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

8. **Learningpool Act 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

    ![구성 URL 복사](common/copy-configuration-urls.png)

    a. 로그인 URL

    b. Azure AD 식별자

    다. 로그아웃 URL

### <a name="configure-learningpool-act-single-sign-on"></a>Learningpool Act Single sign On 구성

**Learningpool Act** 쪽에서 Single Sign-On을 구성하려면 Azure Portal에서 다운로드한 **페더레이션 메타데이터 XML** 과 적절히 복사한 URL을 [Learningpool Act 지원 팀](https://www.learningpool.com/support)으로 보내야 합니다. 이렇게 설정하면 SAML SSO 연결이 양쪽에서 제대로 설정됩니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 Learningpool Act에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**, **모든 애플리케이션**, **Learningpool Act** 를 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **Learningpool Act** 를 선택합니다.

    ![애플리케이션 목록의 Learningpool Act 링크](common/all-applications.png)

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

    !["사용자 및 그룹" 링크](common/users-groups-blade.png)

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![할당 추가 창](common/add-assign-user.png)

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. SAML 어설션 및 **역할 선택** 대화 상자에서 모든 역할 값이 필요한 경우 목록에서 적절한 사용자 역할을 선택한 다음, 화면 맨 아래에 있는 **선택** 단추를 클릭합니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-learningpool-act-test-user"></a>Learningpool Act 테스트 사용자 만들기

Learningpool Act에 프로비전된 Azure AD 사용자만이 Learningpool Act에 로그인할 수 있습니다.

Learningpool Act에 대한 사용자 프로비저닝을 구성할 작업 항목이 없습니다.  
[Learningpool Act 지원 팀](https://www.Learningpool.com/support)에서 사용자를 만들어야 합니다.

> [!NOTE]
> 다른 Learningpool Act 사용자 계정 생성 도구 또는 Learningpool Act가 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비저닝할 수 있습니다.

### <a name="test-single-sign-on"></a>Single Sign-On 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 Learningpool Act 타일을 클릭하면 SSO를 설정한 Learningpool Act에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)