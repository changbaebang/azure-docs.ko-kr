---
title: '자습서: Tableau Server와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 Tableau Server 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/25/2021
ms.author: jeedes
ms.openlocfilehash: 810f57afceda10c10cf5919a0c50ca6be2950703
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101650589"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-tableau-server"></a>자습서: Tableau Server와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Tableau Server를 통합하는 방법을 알아봅니다. Azure AD와 Tableau Server를 통합하면 다음 작업을 수행할 수 있습니다.

* Tableau Server에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 Tableau Server에 자동으로 로그인되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.


## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Tableau Server SSO(Single Sign-On) 사용 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Tableau Server는 **SP** 시작 SSO를 지원합니다.

## <a name="add-tableau-server-from-the-gallery"></a>갤러리에서 Tableau Server 추가

Tableau Server의 Azure AD 통합을 구성하려면 갤러리의 Tableau Server를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Tableau Server** 를 입력합니다.
1. 결과 패널에서 **Tableau Server** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-tableau-server"></a>Tableau Server에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Tableau Server에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Tableau Server의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Tableau Server에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Tableau Server SSO 구성](#configure-tableau-server-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Tableau Server 테스트 사용자 만들기](#create-tableau-server-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Tableau Server에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Tableau Server** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    a. **로그인 URL** 텍스트 상자에서 `https://azure.<domain name>.link` 패턴을 사용하여 URL을 입력합니다.

    b. **식별자** 텍스트 상자에서 `https://azure.<domain name>.link` 패턴을 사용하는 URL을 입력합니다.

    다. **회신 URL** 텍스트 상자에서 `https://azure.<domain name>.link/wg/saml/SSO/index.html` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 위의 값은 실제 값이 아닙니다. 이 자습서의 뒷부분에서 설명하는 Tableau Server 구성 페이지에서 실제 로그온, 식별자 및 회신 URL로 값을 업데이트합니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML** 을 찾고, **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

1. **Tableau Server 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Tableau Server에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Tableau Server** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-tableau-server-sso"></a>Tableau Server SSO 구성

1. 애플리케이션에 구성된 SSO를 가져오려면 Tableau Server 테넌트에 관리자로 로그인해야 합니다.

2. **구성** 탭에서 **사용자 ID 및 액세스** 를 선택한 다음, **인증** 방법 탭을 선택합니다.

    ![스크린샷은 사용자 ID 및 액세스에서 선택한 인증을 보여줍니다.](./media/tableauserver-tutorial/auth.png)

3. **구성** 페이지에서 다음 단계를 수행합니다.

    ![스크린샷은 설명된 값을 입력할 수 있는 구성 페이지를 보여줍니다.](./media/tableauserver-tutorial/config.png)

    a. **인증 방법** 은 SAML을 선택합니다.

    b. **서버 SAML 인증 가능** 확인란을 선택합니다.

    다. Tableau Server 반환 URL - Tableau Server 사용자가 액세스하는 URL(예: `http://tableau_server`)입니다. `http://localhost`을 사용하는 것은 권장되지 않습니다. 후행 슬래시가 있는 URL(예: `http://tableau_server/`)은 지원되지 않습니다. **Tableau Server 반환 URL** 을 복사하고 Azure Portal의 **기본 SAML 구성** 섹션에 있는 **로그온 URL** 텍스트 상자에 붙여넣습니다.

    d. SAML 엔터티 ID - 엔터티 ID는 IdP에 대한 Tableau Server 설치를 고유하게 식별합니다. 원하는 경우 여기에 Tableau Server URL을 다시 입력할 수 있지만 반드시 Tableau Server URL을 입력해야 하는 것은 아닙니다. **SAML 엔터티 ID** 를 복사하고 Azure Portal의 **기본 SAML 구성** 섹션에 있는 **식별자** 텍스트 상자에 붙여넣습니다.

    e. **XML 메타데이터 파일 다운로드** 를 클릭하고 텍스트 편집기 애플리케이션에서 엽니다. Http Post 및 인덱스 0이 포함된 어설션 소비자 서비스 URL을 찾아서 복사합니다. 이제 Azure Portal의 **기본 SAML 구성** 섹션에 있는 **회신 URL** 텍스트 상자에 붙여넣습니다.

    f. Azure Portal에서 다운로드한 페더레이션 메타데이터 파일을 찾은 다음 **SAML Idp 메타데이터 파일** 에 업로드합니다.

    g. IdP가 사용자 이름, 표시 이름, 이메일 주소를 확보하는 데 사용하는 특성의 이름을 입력합니다.

    h. **저장** 을 클릭합니다.

    > [!NOTE]
    > 고객은 확장명이 .crt인 PEM으로 인코딩된 x509 인증서 파일 및 확장명이 .key인 RSA 또는 DSA 프라이빗 키 파일을 인증서 키 파일로 업로드해야 합니다. 인증서 파일 및 인증서 키 파일에 대한 자세한 내용은 [이](https://help.tableau.com/current/server/en-us/saml_requ.htm) 문서를 참조하세요. Tableau Server에서 SAML을 구성하는 데 도움이 필요한 경우 [Server Wide SAML 구성](https://help.tableau.com/current/server/en-us/config_saml.htm) 문서를 참조하세요.

### <a name="create-tableau-server-test-user"></a>Tableau Server 테스트 사용자 만들기

이 섹션은 Tableau Server에서 B.Simon이라는 사용자를 만들기 위한 것입니다. Tableau Server의 모든 사용자를 프로비전해야 합니다.

사용자의 사용자 이름은 Azure AD에서 구성한 사용자 지정 특성 **username** 의 값과 일치해야 합니다. 올바른 매핑을 사용해야 통합 시 Azure AD Single Sign-On 구성이 작동합니다.

> [!NOTE]
> 사용자를 수동으로 만들어야 하는 경우 조직의 Tableau Server 관리자에게 문의해야 합니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Tableau Server 로그온 URL로 리디렉션됩니다. 

* Tableau Server 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Tableau Server 타일을 클릭하면 Tableau Server 로그온 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Tableau Server를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).