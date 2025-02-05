---
title: '자습서: Pipedrive와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 Pipedrive 간에 Single Sign-On을 구성하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/05/2021
ms.author: jeedes
ms.openlocfilehash: 96abe2209d4298f23c47c62fec970430f69cbaf6
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101654428"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-pipedrive"></a>자습서: Pipedrive와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Pipedrive를 통합하는 방법에 대해 알아봅니다. Azure AD와 Pipedrive를 통합하면 다음을 수행할 수 있습니다.

* Azure AD에서 Pipedrive에 액세스할 수 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Pipedrive에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Pipedrive SSO(Single Sign-On)를 사용하도록 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Pipedrive에서 **SP 및 IDP** 시작 SSO를 지원합니다.

## <a name="add-pipedrive-from-the-gallery"></a>갤러리에서 Pipedrive 추가

Pipedrive가 Azure AD에 통합되도록 구성하려면 갤러리의 Pipedrive를 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Pipedrive** 를 입력합니다.
1. 결과 패널에서 **Pipedrive** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-pipedrive"></a>Pipedrive에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Pipedrive에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Pipedrive의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Pipedrive에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Pipedrive SSO 구성](#configure-pipedrive-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[Pipedrive 테스트 사용자 만들기](#create-pipedrive-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Pipedrive에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Pipedrive** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **IDP** 섹션에서 애플리케이션을 구성하려면 **기본 SAML 구성** 섹션에서 다음 필드 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 `https://<COMPANY-NAME>.pipedrive.com/sso/auth/samlp/metadata.xml` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<COMPANY-NAME>.pipedrive.com/sso/auth/samlp` 패턴을 사용하여 URL을 입력합니다.

1. **SP** 시작 모드에서 애플리케이션을 구성하려면 **추가 URL 설정** 를 클릭하고 다음 단계를 수행합니다.

    **로그인 URL** 텍스트 상자에서 `https://<COMPANY-NAME>.pipedrive.com/` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 해당 값을 얻으려면 [Pipedrive 클라이언트 지원 팀](mailto:support@pipedrive.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. Pipedrive 애플리케이션에는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 하는 특정 형식의 SAML 어설션이 필요합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다.

    ![이미지](common/default-attributes.png)

1. 위에서 언급한 특성 외에도 Pipedrive 애플리케이션에는 아래에 표시된 SAML 응답에서 다시 전달되어야 하는 몇 가지 특성이 추가로 필요합니다. 이러한 특성도 미리 채워져 있지만 요구 사항에 따라 검토할 수 있습니다.

    | Name | 원본 특성|
    | ------------ | --------- |
    | 이메일 | user.mail |

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾고, **다운로드** 를 선택하여 인증서를 다운로드하고 컴퓨터에 저장하고, **앱 페더레이션 메타데이터 URL** 도 복사하여 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](./media/pipedrive-tutorial/certificate-data.png)

1. **Pipedrive 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Pipedrive에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Pipedrive** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-pipedrive-sso"></a>Pipedrive SSO 구성

1. 다른 브라우저 창에서 관리자 권한으로 Pipedrive 웹 사이트에 로그온합니다.

1. **User Profile(사용자 프로필)** 을 클릭하고 **Settings(설정)** 를 선택합니다.

    !["사용자 프로필" 메뉴에서 선택한 "설정"을 보여주는 스크린샷.](./media/pipedrive-tutorial/configure-1.png)

1. 보안 센터까지 아래로 스크롤하고, **Single sign-on** 을 클릭합니다.

    !["Security Center"에서 선택한 "Single Sign-On"을 보여주는 스크린샷.](./media/pipedrive-tutorial/configure-2.png)

1. **SAML configuration for pipedrive(Pipedrive에 대한 SAML 구성)** 섹션에서 다음 단계를 수행합니다.

    ![모든 텍스트 상자가 강조 표시된 "Pipedrive에 대한 SAML 구성" 섹션을 보여주는 스크린샷.](./media/pipedrive-tutorial/configure-3.png)

    a. Azure Portal에서 복사한 **앱 페더레이션 메타데이터 URL** 값을 **Issuer(발급자)** 텍스트 상자에 붙여넣습니다.

    b. Azure Portal에서 복사한 **로그인 URL** 값을 **Single Sign On(SSO) url** 텍스트 상자에 붙여넣습니다.

    다. Azure Portal에서 복사한 **로그아웃 URL** 값을 **Single Log Out(SLO) url** 텍스트 상자에 붙여넣습니다.

    d. **x.509 인증서** 텍스트 상자의 경우 Azure Portal에서 다운로드한 **인증서(Base64)** 파일을 메모장에 열고, 내용을 복사하여 **x.509 인증서** 텍스트 상자에 붙여넣고 변경 내용을 저장합니다.

### <a name="create-pipedrive-test-user"></a>Pipedrive 테스트 사용자 만들기

1. 다른 브라우저 창에서 관리자 권한으로 Pipedrive 웹 사이트에 로그온합니다.

1. 회사까지 아래로 스크롤하고, **manage users(사용자 관리)** 를 선택합니다.

    !["회사" 메뉴에서 선택한 "사용자 관리"를 보여주는 스크린샷.](./media/pipedrive-tutorial/user-1.png)

1. **Add users(사용자 추가)** 를 클릭합니다.
    
    ![오른쪽에 "사용자 추가" 단추가 선택된 "사용자 관리" 페이지를 보여주는 스크린샷.](./media/pipedrive-tutorial/user-2.png)

1. **Manage users(사용자 관리)** 섹션에서 다음 단계를 수행합니다.

    ![Pipedrive 구성](./media/pipedrive-tutorial/user-3.png)

    a. **이메일** 텍스트 상자에 사용자의 이메일 주소(예: `B.Simon@contoso.com`)를 입력합니다.

    b. **First name(이름)** 텍스트 상자에서 사용자의 이름을 입력합니다.

    다. **Last name(성)** 텍스트 상자에서 사용자의 성을 입력합니다.

    d. **Confirm and invite users(사용자 확인 및 초대)** 를 클릭합니다.

## <a name="test-sso"></a>SSO 테스트 


이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

#### <a name="sp-initiated"></a>SP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Pipedrive 로그온 URL로 리디렉션됩니다.  

* Pipedrive 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

#### <a name="idp-initiated"></a>IDP 시작:

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭하면 SSO를 설정한 Pipedrive에 자동으로 로그인됩니다. 

Microsoft 내 앱을 사용하여 모든 모드에서 애플리케이션을 테스트할 수도 있습니다. 내 앱에서 Pipedrive 타일을 클릭하면 SP 모드로 구성된 경우 로그인 흐름을 시작하기 위해 애플리케이션 로그온 페이지로 리디렉션되고, IDP 모드로 구성된 경우에는 SSO를 설정한 Pipedrive에 자동으로 로그인됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Pipedrive가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).