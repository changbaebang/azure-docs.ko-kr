---
title: '자습서: Appian과 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 Appian 간에 Single Sign-On을 구성하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 11/17/2020
ms.author: jeedes
ms.openlocfilehash: aef8eb429bf772dff4d4b0de629cb1118b140e10
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96180390"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-appian"></a>자습서: Appian과 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Appian을 통합하는 방법에 대해 알아봅니다. Azure AD와 Appian을 통합하면 다음을 수행할 수 있습니다.

* Azure AD에서 Appian에 액세스할 수 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Appian에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Appian SSO(Single Sign-On)를 사용하도록 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Appian에서 **SP 및 IDP** 시작 SSO를 지원합니다.
* Appian에서 **Just-In-Time** 사용자 프로비저닝을 지원합니다.

## <a name="adding-appian-from-the-gallery"></a>갤러리에서 Appian 추가

Appian이 Azure AD에 통합되도록 구성하려면 갤러리의 Appian을 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Appian** 을 입력합니다.
1. 결과 패널에서 **Appian** 을 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.


## <a name="configure-and-test-azure-ad-sso-for-appian"></a>Appian에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Appian에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Appian의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Appian에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Appian SSO 구성](#configure-appian-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Appian 테스트 사용자 만들기](#create-appian-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Appian에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Appian** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾고, **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **IDP** 섹션에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 필드 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 `https://<SUBDOMAIN>.appiancloud.com` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<SUBDOMAIN>.appiancloud.com/suite/saml/AssertionConsumer` 패턴을 사용하여 URL을 입력합니다.

1. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    **로그인 URL** 텍스트 상자에서 `https://<SUBDOMAIN>.appiancloud.com/suite` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 해당 값을 얻으려면 [Appian 클라이언트 지원 팀](mailto:support@appian.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML** 을 찾고, **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

1. **Appian 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 B.Simon에게 Appian에 대한 액세스 권한을 부여하여 해당 사용자가 Azure Single Sign-On을 사용하도록 설정합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Appian** 을 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-appian-sso"></a>Appian SSO 구성

1. 다른 웹 브라우저 창에서 관리자 권한으로 Appian 웹 사이트에 로그인합니다.

1. **관리 콘솔** 로 이동하여 **Enable SAML(SAML 사용)** 을 선택합니다.

1. **Add SAML Identity Provider(SAML ID 공급자 추가)** 를 클릭합니다.

1.  IdP에 대한 **Description(설명)** 을 입력합니다.

1.  **Service Provider Name(서비스 공급자 이름)** 을 입력합니다. 서비스 및 ID 공급자 모두에 대해 고유한 이름이어야 합니다.

1.  IdP 메타데이터를 **Identity Provider Metadata(ID 공급자 메타데이터)** 에 업로드합니다. 

1.  IdP와 일치하는 적절한 **Signature Hashing Algorithm(서명 해시 알고리즘)** 을 선택합니다.

1.  대화 상자의 오른쪽 위에서 **Test This Configuration(이 구성 테스트)** 을 클릭하여 해당 구성이 유효한지 확인합니다.

1. 성공적으로 로그인하면 **Done(완료)** 을 클릭하여 구성 대화 상자를 닫습니다.

1. 새 IdP의 로그인 페이지를 기본값으로 설정하려면 **Default Sign-In Page(기본 로그인 페이지)** 를 적절하게 설정합니다.

1.  대화 상자가 닫히면 **Verify My Access(내 액세스 확인)** 를 클릭하여 Appian에 계속 로그인할 수 있는지 확인합니다. 이번에는 현재 사용자 권한으로 로그인해야 합니다.

1.  계속 로그인할 수 있는지 확인했으면 **Save Changes(변경 내용 저장)** 를 클릭합니다.


### <a name="create-appian-test-user"></a>Appian 테스트 사용자 만들기

이 섹션에서는 Appian에서 Britta Simon이라는 사용자를 만듭니다. Appian은 Just-In-Time 사용자 프로비저닝을 지원하며, 기본적으로 사용하도록 설정되어 있습니다. 이 섹션에 작업 항목이 없습니다. 사용자가 Appian에 아직 없는 경우 인증 후에 새 사용자가 만들어집니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

#### <a name="sp-initiated"></a>SP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Appian 로그온 URL로 리디렉션됩니다.  

* Appian 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

#### <a name="idp-initiated"></a>IDP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 SSO를 설정한 Appian에 자동으로 로그인됩니다. 

Microsoft 액세스 패널을 사용하여 모든 모드에서 애플리케이션을 테스트할 수도 있습니다. 액세스 패널에서 Appian 타일을 클릭하면 SP 모드로 구성된 경우 로그인 흐름을 시작하기 위해 애플리케이션 로그온 페이지로 리디렉션되고, IDP 모드로 구성된 경우 SSO를 설정한 Appian에 자동으로 로그인됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

Appian이 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).