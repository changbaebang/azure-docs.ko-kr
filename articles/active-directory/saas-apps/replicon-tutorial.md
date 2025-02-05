---
title: '자습서: Replicon과 Azure Active Directory 통합 | Microsoft Docs'
description: Azure Active Directory 및 Replicon 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 06/10/2019
ms.author: jeedes
ms.openlocfilehash: 8915d780e79fa219428c54bad5458ab5966df6c1
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "101688504"
---
# <a name="tutorial-integrate-replicon-with-azure-active-directory"></a>자습서: Azure Active Directory와 Replicon 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 Replicon을 통합하는 방법에 대해 알아봅니다. Azure AD와 Replicon을 통합하면 다음을 수행할 수 있습니다.

* Replicon에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 해당 Azure AD 계정으로 Replicon에 자동으로 로그인되도록 합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

Azure AD와 SaaS 앱 통합에 대한 자세한 내용은 [Azure Active Directory를 사용한 애플리케이션 액세스 및 Single Sign-On이란 무엇인가요?](../manage-apps/what-is-single-sign-on.md)를 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [여기](https://azure.microsoft.com/pricing/free-trial/)에서 1개월 평가판을 다운로드할 수 있습니다.
* Replicon SSO(Single Sign-On)가 설정된 구독

> [!NOTE]
> 이 통합은 Azure AD 미국 정부 클라우드 환경에서도 사용할 수 있습니다. 이 애플리케이션은 Azure AD 미국 정부 클라우드 애플리케이션 갤러리에서 찾을 수 있으며 퍼블릭 클라우드에서와 동일한 방법으로 구성할 수 있습니다.

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다. Replicon은 **SP** 시작 SSO를 지원합니다.

## <a name="adding-replicon-from-the-gallery"></a>갤러리에서 Replicon 추가

Replicon의 Azure AD 통합을 구성하려면 갤러리의 Replicon을 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. [Azure Portal](https://portal.azure.com)에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Replicon** 을 입력합니다.
1. 결과 패널에서 **Replicon** 을 선택한 후 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Azure AD Single Sign-On 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Replicon에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Replicon의 관련 사용자 간에 연결 관계를 설정해야 합니다.

Replicon에서 Azure AD SSO를 구성하고 테스트하려면 다음 구성 요소를 완료합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
2. **[Replicon SSO 구성](#configure-replicon-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
3. **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
4. **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
5. **[Replicon 테스트 사용자 만들기](#create-replicon-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 Replicon에 만듭니다.
6. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com/)의 **Replicon** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾은 후 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 페이지에서 다음 필드에 대한 값을 입력합니다.

    1. **로그인 URL** 텍스트 상자에서 `https://global.replicon.com/!/saml2/<client name>/sp-sso/post` 패턴을 사용하여 URL을 입력합니다.

    1. **식별자** 텍스트 상자에서 `https://global.replicon.com/!/saml2/<client name>` 패턴을 사용하는 URL을 입력합니다.

    1. **회신 URL** 텍스트 상자에서 `https://global.replicon.com/!/saml2/<client name>/sso/post` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 로그온 URL, 식별자 및 회신 URL로 값을 업데이트합니다. 이러한 값을 얻으려면 [ 클라이언트 지원 팀](https://www.replicon.com/customerzone/contact-support)에 문의하세요. Azure Portal의 **기본 SAML 구성** 섹션에 표시된 패턴을 참조할 수도 있습니다.

1. **SAML 서명 인증서** 의 편집/펜 아이콘을 클릭하여 설정을 편집합니다.

    ![서명 알고리즘](common/signing-algorithm.png)

    1. **서명 옵션** 으로 **SAML 어설션 서명** 을 선택합니다.

    1. **서명 알고리즘** 으로 **SHA-256** 을 선택합니다.

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML** 을 찾고, **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

   ![인증서 다운로드 링크](common/metadataxml.png)

### <a name="configure-replicon-sso"></a>Replicon SSO 구성

1. 다른 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.

2. 다음 단계를 수행하여 SAML 2.0을 구성합니다.

    ![SAML 인증 사용](./media/replicon-tutorial/ic777805.png "SAML 인증 사용")

    a. **EnableSAML Authentication2** 대화 상자를 표시하려면 다음 회사 키 뒤에 URL에 다음을 추가합니다. `/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

    * 전체 URL의 스키마는 다음과 같습니다. `https://na2.replicon.com/<YourCompanyKey>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

   b. **+** 을(를) 클릭하여 **v20Configuration** 섹션을 확장합니다.

   다. **+** 을(를) 클릭하여 **metaDataConfiguration** 섹션을 확장합니다.

   d. xmlSignatureAlgorithm으로 **SHA256** 을 선택합니다.

   e. **파일 선택** 을 클릭하여 ID 공급자 메타데이터 XML 파일을 선택하고 **제출** 을 클릭합니다.

### <a name="create-an-azure-ad-test-user"></a>Azure AD 테스트 사용자 만들기

이 섹션에서는 Azure Portal에서 B.Simon이라는 테스트 사용자를 만듭니다.

1. Azure Portal의 왼쪽 창에서 **Azure Active Directory**, **사용자**, **모든 사용자** 를 차례로 선택합니다.
1. 화면 위쪽에서 **새 사용자** 를 선택합니다.
1. **사용자** 속성에서 다음 단계를 수행합니다.
   1. **이름** 필드에 `B.Simon`을 입력합니다.  
   1. **사용자 이름** 필드에서 username@companydomain.extension을 입력합니다. 예들 들어 `BrittaSimon@contoso.com`입니다.
   1. **암호 표시** 확인란을 선택한 다음, **암호** 상자에 표시된 값을 적어둡니다.
   1. **만들기** 를 클릭합니다.

### <a name="assign-the-azure-ad-test-user"></a>Azure AD 테스트 사용자 할당

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Replicon에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Replicon** 을 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.

   !["사용자 및 그룹" 링크](common/users-groups-blade.png)

1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.

    ![사용자 추가 링크](common/add-assign-user.png)

1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. SAML 어설션에 역할 값이 필요한 경우 **역할 선택** 대화 상자의 목록에서 사용자에 대한 적절한 역할을 선택한 다음, 화면의 아래쪽에 있는 **선택** 단추를 클릭합니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

### <a name="create-replicon-test-user"></a>Replicon 테스트 사용자 만들기

이 섹션은 Replicon에서 B.Simon이라는 사용자를 만들기 위한 것입니다.

**사용자를 수동으로 만들어야 할 경우 다음 단계를 수행합니다.**

1. 웹 브라우저 창에서 Replicon 회사 사이트에 관리자로 로그인합니다.

2. **관리 \> 사용자** 로 이동합니다.

    ![사용자](./media/replicon-tutorial/ic777806.png "사용자")

3. **+사용자 추가** 를 클릭합니다.

    ![사용자 추가](./media/replicon-tutorial/ic777807.png "사용자 추가")

4. **사용자 프로필** 섹션에서 다음 단계를 수행합니다.

    ![사용자 프로필](./media/replicon-tutorial/ic777808.png "사용자 프로필")

    a. **로그인 이름** 텍스트 상자에 프로비저닝하려는 Azure AD 사용자의 Azure AD 이메일 주소를 입력합니다(예: `B.Simon@contoso.com`).

    > [!NOTE]
    > 로그인 이름은 Azure AD의 사용자 이메일 주소와 일치해야 합니다.

    b. **인증 유형** 으로 **SSO** 를 선택합니다.

    다. 인증 ID를 로그인 이름(사용자의 Azure AD 이메일 주소)과 동일한 값으로 설정합니다.

    d. **부서** 텍스트 상자에 사용자의 부서를 입력합니다.

    e. **직원 형식** 으로 **관리자** 를 선택합니다.

    f. **사용자 프로필 저장** 을 클릭합니다.

> [!NOTE]
> 다른 Replicon 사용자 계정 생성 도구 또는 Replicon이 제공한 API를 사용하여 Azure AD 사용자 계정을 프로비전할 수 있습니다.

### <a name="test-sso"></a>SSO 테스트

액세스 패널에서 Replicon 타일을 선택하면 SSO를 설정한 Replicon에 자동으로 로그인되어야 합니다. 액세스 패널에 대한 자세한 내용은 [액세스 패널 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Active Directory와 SaaS Apps를 통합하는 방법에 대한 자습서 목록](./tutorial-list.md)

- [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

- [Azure Active Directory의 조건부 액세스란?](../conditional-access/overview.md)