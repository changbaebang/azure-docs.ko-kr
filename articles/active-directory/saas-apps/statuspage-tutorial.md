---
title: '자습서: StatusPage와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory 및 StatusPage 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 12/18/2020
ms.author: jeedes
ms.openlocfilehash: cc3ce56ecd17d627001f4925355c055afdc09d22
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99821207"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-statuspage"></a>자습서: StatusPage와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 StatusPage를 통합하는 방법에 대해 알아봅니다.
StatusPage를 Azure AD와 통합하면 다음과 같은 이점이 제공됩니다.

* StatusPage에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 자신의 Azure AD 계정으로 StatusPage에 자동으로 로그인(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

StatusPage와의 Azure AD 통합을 구성하려면 다음 항목이 필요합니다.

* Azure AD 구독 Azure AD 환경이 없으면 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* StatusPage Single Sign-On이 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD Single Sign-On을 구성하고 테스트합니다.

* StatusPage는 **IDP** 시작 SSO를 지원합니다.

## <a name="adding-statuspage-from-the-gallery"></a>갤러리에서 StatusPage 추가

StatusPage의 Azure AD 통합을 구성하려면 갤러리의 StatusPage를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **StatusPage** 를 입력합니다.
1. 결과 패널에서 **StatusPage** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-statuspage"></a>StatusPage에 대한 Azure AD SSO 구성 및 테스트

이 섹션에서는 **Britta Simon** 이라는 테스트 사용자를 기반으로 StatusPage에서 Azure AD Single Sign-On을 구성하고 테스트합니다.
Single Sign-On이 작동하려면 Azure AD 사용자와 StatusPage의 관련 사용자 간에 연결 관계를 설정해야 합니다.

StatusPage에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    1. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - Britta Simon으로 Azure AD Single Sign-On을 테스트하는 데 사용합니다.
    1. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - Britta Simon이 Azure AD Single Sign-on을 사용할 수 있도록 합니다.
1. **[StatusPage SSO 구성](#configure-statuspage-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    1. **[StatusPage 테스트 사용자 만들기](#create-statuspage-test-user)** - Britta Simon의 Azure AD 표현과 연결된 해당 사용자를 StatusPage에 만듭니다.
6. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **AskYourTeam** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **SAML로 Single Sign-On 설정** 페이지에서 다음 단계를 수행합니다.

    a. **식별자** 텍스트 상자에 다음 패턴 중 하나를 사용하여 URL을 입력합니다.

    | ID |
    |--------------|
    | `https://<subdomain>.statuspagestaging.com/` |
    | `https://<subdomain>.statuspage.io/` |
    |

    b. **회신 URL** 텍스트 상자에 다음 패턴을 사용하여 URL을 입력합니다.

     | 회신 URL |
    |--------------|
    | `https://<subdomain>.statuspagestaging.com/sso/saml/consume` |
    | `https://<subdomain>.statuspage.io/sso/saml/consume` |
    |

    > [!NOTE]
    > [SupportTeam@statuspage.io](mailto:SupportTeam@statuspage.io)에서 StatusPage 지원 팀에 문의하여 Single Sign-On을 구성하는 데 필요한 메타데이터를 요청합니다. 
    >
    > a. 메타데이터에서 발급자 값을 복사한 다음 **식별자** 텍스트 상자에 붙여넣습니다.
    >
    > b. 메타데이터에서 회신 URL을 복사한 다음 **회신 URL** 텍스트 상자에 붙여넣습니다.

5. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **인증서(Base64)** 를 다운로드한 다음, 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/certificatebase64.png)

6. **StatusPage 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 Britta Simon에게 StatusPage에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션**, **모든 애플리케이션**, **StatusPage** 를 차례로 선택합니다.

2. 애플리케이션 목록에서 **StatusPage** 를 선택합니다.

3. 왼쪽 메뉴에서 **사용자 및 그룹** 을 선택합니다.

4. **사용자 추가** 단추를 클릭한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

5. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **Britta Simon** 을 선택하고 화면 아래쪽에서 **선택** 단추를 클릭합니다.

6. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.

7. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-statuspage-sso"></a>StatusPage SSO 구성

1. StatusPage 내에서 구성을 자동화하려면 **확장 설치** 를 클릭하여 **내 앱 보안 로그인 브라우저 확장** 을 설치해야 합니다.

    ![내 앱 확장](common/install-myappssecure-extension.png)

2. 브라우저에 확장을 추가한 후 **StatusPage 설정** 을 클릭하면 StatusPage 애플리케이션으로 이동됩니다. 여기서 관리자 자격 증명을 입력하여 StatusPage에 로그인합니다. 브라우저 확장이 애플리케이션을 자동으로 구성하고 3-6단계를 자동으로 수행합니다.

    ![설정 구성](common/setup-sso.png)

3. StatusPage를 수동으로 설정하려면 다른 웹 브라우저 창에서 관리자 권한으로 StatusPage 회사 사이트에 로그인합니다.

1. 주 도구 모음에서 **계정 관리** 를 클릭합니다.

    ![스크린샷은 StatusPage 회사 사이트에서 선택한 계정 관리를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_06.png)

1. **Single Sign-On** 탭을 클릭합니다.

    ![스크린샷은 Single Sign-On 탭을 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_07.png)

1. SSO 설정 페이지에서 다음 단계를 수행합니다.

    ![스크린샷은 설명된 값을 입력할 수 있는 SSO 설정 페이지를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_08.png)

    ![스크린샷은 저장 구성 단추를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_09.png)

    a. **SSO 대상 URL** 텍스트 상자에 Azure Portal에서 복사한 **로그인 URL** 값을 붙여넣습니다.

    b. 다운로드된 인증서를 메모장에서 열고, 내용을 복사한 다음 전체 인증서를 **인증서** 텍스트 상자에 붙여넣습니다.

    다. **구성 저장** 을 클릭합니다.

### <a name="create-statuspage-test-user"></a>StatusPage 테스트 사용자 만들기

이 섹션은 StatusPage에서 Britta Simon이라는 사용자를 만들기 위한 것입니다.

StatusPage는 적시에 프로비전을 지원합니다. 이미 [Azure AD Single Sign-On 구성](#configure-azure-ad-sso)에서 사용하도록 설정했습니다.

**StatusPage에서 Britta Simon이라는 사용자를 만들려면 다음 단계를 수행합니다.**

1. StatusPage 회사 사이트에 관리자 권한으로 로그인합니다.

1. 위쪽 메뉴에서 **계정 관리** 를 클릭합니다.

    ![스크린샷은 StatusPage 회사 사이트에서 선택한 계정 관리를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_06.png)

1. **팀 멤버** 탭을 클릭합니다.
  
    ![스크린샷은 팀 멤버 탭을 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_10.png) 

1. **팀 멤버 추가** 를 클릭합니다.
  
    ![스크린샷은 팀 멤버 추가 단추를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_11.png) 

1. 관련된 텍스트 상자에 프로비저닝할 유효한 사용자의 **이메일 주소**, **이름** 및 **성** 을 입력합니다. 

    ![스크린샷은 설명된 값을 입력할 수 있는 사용자 추가 대화 상자를 보여줍니다.](./media/statuspage-tutorial/tutorial_statuspage_12.png) 

1. **역할** 로 **클라이언트 관리자** 를 선택합니다.

1. **계정 만들기** 를 클릭합니다.

### <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다.

* Azure Portal에서 이 애플리케이션 테스트를 클릭하면 SSO를 설정한 StatusPage에 자동으로 로그인됩니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 StatusPage 타일을 클릭하면 SSO를 설정한 StatusPage에 자동으로 로그인되어야 합니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

StatusPage가 구성되면 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법을 알아봅니다](/cloud-app-security/proxy-deployment-any-app).