---
title: '자습서: SumoLogic과 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory 및 SumoLogic 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/03/2020
ms.author: jeedes
ms.openlocfilehash: 2dcc52688cabebaa6eb813e3240150ea8774e716
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "92521899"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-sumologic"></a>자습서: SumoLogic과 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 SumoLogic을 통합하는 방법에 대해 알아봅니다. Azure AD와 SumoLogic을 통합하는 경우 다음을 수행할 수 있습니다.

* SumoLogic에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 해당 Azure AD 계정으로 SumoLogic에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* SumoLogic SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* SumoLogic은 **IDP** 시작 SSO를 지원합니다.

## <a name="adding-sumologic-from-the-gallery"></a>갤러리에서 SumoLogic 추가

SumoLogic의 Azure AD 통합을 구성하려면 갤러리의 SumoLogic을 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **SumoLogic** 을 입력합니다.
1. 결과 패널에서 **SumoLogic** 을 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-single-sign-on-for-sumologic"></a>SumoLogic용 Azure AD Single Sign-On 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 SumoLogic에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 SumoLogic의 관련 사용자 간에 연결 관계를 설정해야 합니다.

SumoLogic에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[SumoLogic SSO 구성](#configure-sumologic-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[SumoLogic 테스트 사용자 만들기](#create-sumologic-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 SumoLogic에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **SumoLogic** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾은 후 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **SAML로 Single Sign-On 설정** 페이지에서 다음 필드에 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 다음 패턴을 사용하여 URL을 입력합니다.

    - `https://service.sumologic.com`
    - `https://<tenantname>.us2.sumologic.com`
    - `https://<tenantname>.us4.sumologic.com`
    - `https://<tenantname>.eu.sumologic.com`
    - `https://<tenantname>.jp.sumologic.com`
    - `https://<tenantname>.de.sumologic.com`
    - `https://<tenantname>.ca.sumologic.com`

    b. **회신 URL** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다.

    - `https://service.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.us2.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.us4.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.eu.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.jp.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.de.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.ca.sumologic.com/sumo/saml/consume/<tenantname>`
    - `https://service.au.sumologic.com/sumo/saml/consume/<tenantname>`

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자 및 회신 URL로 해당 값을 업데이트합니다. 이러한 값을 얻으려면 [SumoLogic 클라이언트 지원 팀](https://www.sumologic.com/contact-us/)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. SumoLogic 애플리케이션은 특정 서식에서 SAML 어설션을 예상하며, SAML 토큰 특성 구성에 사용자 할당 특성 매핑을 추가해야 합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다.

    ![이미지](common/default-attributes.png)

1. 위에서 언급한 특성 외에도 SumoLogic 애플리케이션에는 아래에 표시된 SAML 응답에서 다시 전달되어야 하는 몇 가지 특성이 추가로 필요합니다. 이러한 특성도 미리 채워져 있지만 요구 사항에 따라 검토할 수 있습니다.

    |  Name | 원본 특성 |
    | ---------------| --------------- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | 역할 | user.assignedroles |

    > [!NOTE]
    > [여기](../develop/active-directory-enterprise-app-role-management.md)를 클릭하여 Azure AD에서 **역할** 을 구성하는 방법을 알아봅니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. **SumoLogic 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 SumoLogic에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **SumoLogic** 을 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-sumologic-sso"></a>SumoLogic SSO 구성

1. 다른 웹 브라우저 창에서 SumoLogic 회사 사이트에 관리자로 로그인합니다.

1. **관리 \> 보안** 으로 이동합니다.

    ![관리](./media/sumologic-tutorial/ic778556.png "관리")

1. **SAML** 을 클릭합니다.

    ![글로벌 보안 설정](./media/sumologic-tutorial/ic778557.png "전역 보안 설정")

1. **구성 선택 또는 새로 만들기** 목록에서 **Azure AD** 를 선택하고 **구성** 을 클릭합니다.

    ![스크린샷은 Azure AD를 선택할 수 있는 SAML 2.0 구성을 보여줍니다.](./media/sumologic-tutorial/ic778558.png "SAML 2.0 구성")

1. **SAML 2.0 구성** 대화 상자에서 다음 단계를 수행합니다.

    ![스크린샷은 설명된 값을 입력할 수 있는 SAML 2.0 구성 대화 상자를 보여줍니다.](./media/sumologic-tutorial/ic778559.png "SAML 2.0 구성")

    a. **구성 이름** 텍스트 상자에 **Azure AD** 를 입력합니다.

    b. **디버그 모드** 를 선택합니다.

    다. **발급자** 텍스트 상자에 Azure Portal에서 복사한 **Azure AD 식별자** 값을 붙여넣습니다.

    d. Azure Portal에서 복사한 **로그인 URL** 값을 **인증 요청 URL** 텍스트 상자에 붙여넣습니다.

    e. Base 64로 인코딩된 인증서를 메모장에서 열고, 내용을 클립보드에 복사한 다음 전체 인증서를 **X.509 인증서** 텍스트 상자에 붙여 넣습니다.

    f. **이메일 속성** 에서는 **SAML 제목 사용** 을 선택합니다.  

    g. **SP 시작 로그인 구성** 을 선택합니다.

    h. **로그인 경로** 텍스트 상자에 **Azure** 를 입력하고 **저장** 을 클릭합니다.

### <a name="create-sumologic-test-user"></a>SumoLogic 테스트 사용자 만들기

Azure AD 사용자가 SumoLogic에 로그인할 수 있도록 하려면 SumoLogic으로 프로비저닝되어야 합니다. SumoLogic의 경우 프로비전은 수동 작업입니다.

**사용자 계정을 프로비전하려면 다음 단계를 수행합니다.**

1. 자신의 **SumoLogic** 테넌트에 로그인합니다.

1. **\> 사용자 관리** 로 이동합니다.

    ![스크린샷은 관리 메뉴에서 선택한 사용자를 보여 줍니다.](./media/sumologic-tutorial/ic778561.png "사용자")

1. **추가** 를 클릭합니다.

    ![스크린샷은 사용자에 대한 추가 단추를 보여줍니다.](./media/sumologic-tutorial/ic778562.png "사용자")

1. **새 사용자** 대화 상자에서 다음 단계를 수행합니다.

    ![새 사용자](./media/sumologic-tutorial/ic778563.png "새 사용자")

    a. 프로비전하려는 Azure AD 계정의 관련 정보를 **이름**, **성** 및 **전자 메일** 텍스트 상자에 입력합니다.
  
    b. 원하는 역할을 선택합니다.
  
    다. **상태** 는 **활성** 을 선택합니다.
  
    d. **저장** 을 클릭합니다.

> [!NOTE]
> 다른 SumoLogic 사용자 계정 생성 도구 또는 SumoLogic이 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비저닝할 수 있습니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 액세스 패널을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

액세스 패널에서 SumoLogic 타일을 클릭하면, SSO를 설정한 SumoLogic에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS 앱을 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란?](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)

- [Azure AD로 SumoLogic 사용해보기](https://aad.portal.azure.com/)