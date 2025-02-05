---
title: '자습서: Cornerstone Single Sign-On과 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 Cornerstone Single Sign-On 간에 Single Sign-On을 구성하는 방법을 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/09/2021
ms.author: jeedes
ms.openlocfilehash: f7167df523ca6f84eacd92fc7af1011e8b3b00b6
ms.sourcegitcommit: ac035293291c3d2962cee270b33fca3628432fac
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/24/2021
ms.locfileid: "104950386"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-cornerstone-single-sign-on"></a>자습서: Cornerstone Single Sign-On과 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Cornerstone Single Sign-On을 통합하는 방법에 대해 알아봅니다. Azure AD와 Cornerstone Single Sign-On을 통합하면 다음을 수행할 수 있습니다.

* Azure AD에서 Cornerstone Single Sign-On에 액세스할 수 있는 사용자를 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Cornerstone Single Sign-On에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Cornerstone Single Sign-On SSO(Single Sign-On)를 사용하도록 설정된 구독

> [!NOTE]
> 이 통합은 Azure AD 미국 정부 클라우드 환경에서도 사용할 수 있습니다. 이 애플리케이션은 Azure AD 미국 정부 클라우드 애플리케이션 갤러리에서 찾을 수 있으며 퍼블릭 클라우드에서와 동일한 방법으로 구성할 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Cornerstone Single Sign-On에서 **SP** 시작 SSO를 지원합니다.
* Cornerstone Single Sign-On에서 [자동화된 사용자 프로비저닝](cornerstone-ondemand-provisioning-tutorial.md)을 지원합니다.


## <a name="adding-cornerstone-single-sign-on-from-the-gallery"></a>갤러리에서 Cornerstone Single Sign-On 추가

Cornerstone Single Sign-On이 Azure AD에 통합되도록 구성하려면 갤러리의 Cornerstone Single Sign-On을 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에서 **Cornerstone Single Sign-On** 을 입력합니다.
1. 결과 패널에서 **Cornerstone Single Sign-On** 을 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-cornerstone-single-sign-on"></a>Cornerstone Single Sign-On에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Cornerstone Single Sign-On에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Cornerstone Single Sign-On의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Cornerstone Single Sign-On에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
2. **[Cornerstone Single Sign-On SSO 구성](#configure-cornerstone-single-sign-on-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[Cornerstone Single Sign-On 테스트 사용자 만들기](#create-cornerstone-single-sign-on-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Cornerstone Single Sign-On에 만듭니다.
3. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Cornerstone Single Sign-On** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾고, **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 단계를 수행합니다.

    a. **식별자** 텍스트 상자에서 `https://<PORTAL_NAME>.csod.com` 패턴을 사용하여 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<PORTAL_NAME>.csod.com/samldefault.aspx?ouid=<OUID>` 패턴을 사용하여 URL을 입력합니다.

    다. **로그온 URL** 텍스트 상자에서 `https://<PORTAL_NAME>.csod.com/samldefault.aspx?ouid=<OUID>` 패턴을 사용하는 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 이러한 값을 실제 회신 URL, 식별자 및 로그온 URL로 업데이트합니다. 이러한 값을 얻으려면 [Cornerstone Single Sign-On 클라이언트 지원 팀](mailto:moreinfo@csod.com)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

4. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **인증서(Base64)** 를 찾은 후 **다운로드** 를 선택하여 인증서를 다운로드하고 본인의 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **Cornerstone Single Sign-On 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 B.Simon에게 Cornerstone Single Sign-On에 대한 액세스 권한을 부여하여 해당 사용자가 Azure Single Sign-On을 사용하도록 설정합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Cornerstone Single Sign-On** 을 클릭합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-cornerstone-single-sign-on-sso"></a>Cornerstone Single Sign-On SSO 구성

1. 관리자 권한으로 Cornerstone Single Sign-On에 로그인합니다.

1. **Admin(관리자) > Tools(도구)** 로 차례로 이동합니다.

    ![Admin(관리자) 페이지에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/admin.png)

1. **Configuration Tools(구성 도구)** 에서 **EDGE** 패널을 선택합니다.

    ![EDGE 패널에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/edge-panel.png)

1. **Integrate(통합)** 섹션에서 Single Sign-On을 선택합니다.

    ![Single Sign-On 옵션에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/single-sign-on.png)

1. **Add SSO(SSO 추가)** 단추를 클릭합니다. 아래 표시된 팝업 창에서 **Inbound SAML(인바운드 SAML)** 을 선택한 다음, **Add(추가)** 를 클릭합니다.

    ![Inbound SAML(인바운드 SAML)에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/inbound.png)

1. 다음 페이지에서 아래 단계를 수행합니다.

    ![Cornerstone의 구성 섹션에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/configuration.png)

    a. **General Properties(일반 속성)** 에서 **Upload File(파일 업로드)** 을 클릭하여 Azure Portal에서 다운로드한  **인증서(Base64)** 파일을 업로드합니다.

    b. **Enable(사용)** 확인란을 선택하고, Azure Portal에서 복사한 **로그인 URL** 값을 **IDP URL** 텍스트 상자에 붙여넣습니다.

    다. **저장** 을 클릭합니다.

### <a name="create-cornerstone-single-sign-on-test-user"></a>Cornerstone Single Sign-On 테스트 사용자 만들기

이 섹션에서는 Cornerstone Single Sign-On에서 B.Simon이라는 사용자를 만듭니다. Cornerstone Single Sign-On은 기본적으로 사용하도록 설정되는 자동 사용자 프로비저닝을 지원합니다. 자동 사용자 프로비전 구성 방법에 대한 자세한 내용은 [여기](./cornerstone-ondemand-provisioning-tutorial.md)에서 제공합니다.

**사용자를 수동으로 만들어야 할 경우 다음 단계를 수행합니다.**

1. 관리자 권한으로 Cornerstone Single Sign-On에 로그인합니다.

1. **Admin(관리자) -> Users(사용자)** 로 차례로 이동하고, 페이지 아래쪽에서 **Add User(사용자 추가)** 를 클릭합니다.

    ![Cornerstone의 테스트 사용자 만들기에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/user-1.png)

1. **Add new user(새 사용자 추가)** 페이지에서 필수 필드를 채우고, **Save(저장)** 를 클릭합니다.

    ![필수 필드가 있는 테스트 사용자 만들기에 대한 스크린샷](./media/cornerstone-ondemand-tutorial/user-2.png)

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Cornerstone Single Sign-On 로그온 URL로 리디렉션됩니다. 

* Cornerstone Single Sign-On 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Cornerstone Single Sign-On 타일을 클릭하면 Cornerstone Single Sign-On 로그온 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

Cornerstone Single Sign-On이 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)