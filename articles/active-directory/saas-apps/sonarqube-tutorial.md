---
title: '자습서: Sonarqube와 Azure Active Directory SSO(Single Sign-On) 연결 | Microsoft Docs'
description: Azure Active Directory와 Sonarqube 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 09/29/2020
ms.author: jeedes
ms.openlocfilehash: f756e738989775bf9c06b44a03f002c14f42e3ac
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96182352"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-sonarqube"></a>자습서: Sonarqube와 Azure Active Directory SSO(Single Sign-On) 연결

이 자습서에서는 Azure AD(Azure Active Directory)와 Sonarqube를 연결하는 방법에 대해 알아봅니다. Azure AD와 Sonarqube를 연결하면 다음을 수행할 수 있습니다.

* Azure AD에서는 Sonarqube에 대한 액세스 권한이 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Sonarqube에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Sonarqube SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Sonarqube는 **SP** 시작 SSO를 지원합니다.

> [!NOTE]
> 이 애플리케이션의 식별자는 고정 문자열 값이므로 하나의 테넌트에서 하나의 인스턴스만 구성할 수 있습니다.

## <a name="adding-sonarqube-from-the-gallery"></a>갤러리에서 Sonarqube 추가

Sonarqube의 Azure AD 통합을 구성하려면 갤러리의 Sonarqube를 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Sonarqube** 를 입력합니다.
1. 결과 패널에서 **Sonarqube** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-sonarqube"></a>Sonarqube에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Sonarqube에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Sonarqube의 관련 사용자 간에 연결 관계가를 설정해야 합니다.

Sonarqube에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Sonarqube SSO 구성](#configure-sonarqube-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Sonarqube 테스트 사용자 만들기](#create-sonarqube-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Sonarqube에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Sonarqube** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    **로그온 URL** 텍스트 상자에 다음 URL을 입력합니다.

    * **프로덕션 환경의 경우**

        `https://servicessonar.corp.microsoft.com/`

    * **개발 환경의 경우**

        `https://servicescode-dev.westus.cloudapp.azure.com`

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

1. **Sonarqube 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Sonarqube에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Sonarqube** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.

1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-sonarqube-sso"></a>Sonarqube SSO 구성

1. 새 웹 브라우저 창을 열고, Sonarqube 회사 사이트에 관리자 권한으로 로그인합니다.

1. **관리 > 구성 > 보안** 을 클릭하고 **SAML 플러그 인** 으로 이동하여 다음 단계를 수행합니다.

1. IdP 메타데이터에서 다음 세부 정보를 복사하여 SonarQube 플러그 인의 해당 텍스트 필드에 붙여넣습니다.
    1. IdP 엔터티 ID
    2. 로그인 URL
    3. X.509 인증서 
1. 모든 세부 정보를 저장합니다.
    ![saml 플러그 인 IDP](./media/sonarqube-tutorial/sso-idp-metadata.png)

1. **SAML** 페이지에서 다음 단계를 수행합니다.

    ![Sonarqube 구성](./media/sonarqube-tutorial/config01.png)

    a. **사용** 옵션을 **예** 로 설정합니다.

    b. **애플리케이션 ID** 텍스트 상자에서 **sonarqube** 와 같은 이름을 입력합니다.

    다. **공급자 이름** 텍스트 상자에서 **SAML** 과 같은 이름을 입력합니다.

    d. **공급자 ID** 텍스트 상자에 Azure Portal에서 복사한 **Azure AD 식별자** 값을 붙여넣습니다.

    e. Azure Portal에서 복사한 **로그인 URL** 값을 **SAML 로그인 URL** 텍스트 상자에 붙여넣습니다.

    f. 메모장에서 Base64로 인코딩된 인증서를 열고, 해당 콘텐츠를 복사한 다음, **공급자 인증서** 텍스트 상자에 붙여넣습니다.

    g. **SAML 사용자 로그인 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` 값을 입력합니다.

    h. **SAML 사용자 이름 특성** 텍스트 상자에 `http://schemas.microsoft.com/identity/claims/displayname` 값을 입력합니다.

    i. **SAML 사용자 이메일 특성** 텍스트 상자에 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name` 값을 입력합니다.

    j. **저장** 을 클릭합니다.

### <a name="create-sonarqube-test-user"></a>Sonarqube 테스트 사용자 만들기

이 섹션에서는 Sonarqube에 B.Simon이라는 사용자를 만듭니다. [Sonarqube 클라이언트 지원 팀](https://www.sonarsource.com/support/)과 협력하여 Sonarqube 플랫폼에 사용자를 추가합니다. Single Sign-On을 사용하려면 먼저 사용자를 만들고 활성화해야 합니다. 

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

1. Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Sonarqube 로그온 URL로 리디렉션됩니다. 

2. Sonarqube 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

3. Microsoft 액세스 패널을 사용할 수 있습니다. 액세스 패널에서 Sonarqube 타일을 클릭하면 Sonarqube 로그온 URL로 리디렉션됩니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

* Sonarqube를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).