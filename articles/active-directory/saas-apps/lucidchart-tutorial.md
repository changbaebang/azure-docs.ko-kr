---
title: '자습서: Lucidchart와 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Lucidchart 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 01/15/2021
ms.author: jeedes
ms.openlocfilehash: 5d5b07e761d5ed38cb2083054708265189bdd72f
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "101651582"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-lucidchart"></a>자습서: Lucidchart와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Lucidchart를 통합하는 방법에 대해 알아봅니다. Azure AD와 Lucidchart를 통합하면 다음을 수행할 수 있습니다.

* Lucidchart에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 Lucidchart에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Lucidchart SSO(Single Sign-on)이 설정된 구독입니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Lucidchart에서 **SP** 시작 SSO를 지원합니다.
* Lucidchart에서 **Just In Time** 사용자 프로비전을 지원합니다.

## <a name="add-lucidchart-from-the-gallery"></a>갤러리에서 Lucidchart 추가

Lucidchart의 Azure AD 통합을 구성하려면 갤러리의 Lucidchart를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Lucidchart** 를 입력합니다.
1. 결과 패널에서 **Lucidchart** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.


## <a name="configure-and-test-azure-ad-sso-for-lucidchart"></a>Lucidchart에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Lucidchart에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Lucidchart의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Lucidchart에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[Lucidchart SSO 구성](#configure-lucidchart-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[Lucidchart 테스트 사용자 만들기](#create-lucidchart-test-user)** - B.Simon의 Azure AD 표현과 연결되는 대응 사용자를 Lucidchart에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Lucidchart** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 연필 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

   **로그온 URL** 텍스트 상자에 URL `https://chart2.office.lucidchart.com/saml/sso/azure`를 입력합니다.

5. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **다운로드** 를 클릭하여 요구 사항에 따라 제공된 옵션에서 **페더레이션 메타데이터 XML** 을 다운로드하고 컴퓨터에 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

6. **Lucidchart 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Lucidchart에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Lucidchart** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-lucidchart-sso"></a>Lucidchart SSO 구성

1. 다른 웹 브라우저 창에서 Lucidchart 회사 사이트에 관리자로 로그인합니다.

2. 상단 메뉴에서 **팀** 을 클릭합니다.

    ![팀](./media/lucidchart-tutorial/ic791190.png "팀")

3. **애플리케이션 \> SAML 관리** 를 클릭합니다.

    ![SAML 관리](./media/lucidchart-tutorial/ic791191.png "SAML 관리")

4. **SAML 인증 설정** 대화 상자 페이지에서 다음 단계를 수행합니다.

    a. **SAML 인증 사용** 을 선택하고 **선택 사항** 을 클릭합니다.

    ![SAML 인증 설정](./media/lucidchart-tutorial/ic791192.png "SAML 인증 설정")

    b. **도메인** 텍스트 상자에 도메인을 입력하고 **인증서 변경** 을 클릭합니다.

    ![인증서 변경](./media/lucidchart-tutorial/ic791193.png "인증서 변경")

    다. 다운로드한 메타데이터 파일을 열고 내용을 복사한 다음 **메타데이터 업로드** 텍스트 상자에 붙여넣습니다.

    ![메타데이터 업로드](./media/lucidchart-tutorial/ic791194.png "메타데이터 업로드")

    d. **신규 사용자를 자동으로 팀에 추가** 를 선택한 다음 **변경 내용 저장** 을 클릭합니다.

    ![변경 내용 저장](./media/lucidchart-tutorial/ic791195.png "변경 내용 저장")

### <a name="create-lucidchart-test-user"></a>Lucidchart 테스트 사용자 만들기

Lucidchart를 프로비전하는 사용자를 구성할 작업 항목이 없습니다.  할당된 사용자가 액세스 패널을 사용하여 Lucidchart에 로그인하려는 경우 Lucidchart는 사용자가 존재하는지를 확인합니다.  

사용할 수 있는 사용자 계정이 없으면 자동으로 Lucidchart에 의해 생성됩니다.

## <a name="test-sso"></a>SSO 테스트 

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Lucidchart 로그온 URL로 리디렉션됩니다. 

* Lucidchart 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Lucidchart 타일을 클릭하면 SSO를 설정한 Lucidchart에 자동으로 로그인되어야 합니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

 Lucidchart를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)