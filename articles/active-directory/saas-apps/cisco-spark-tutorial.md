---
title: '자습서: Cisco Webex와 Azure Active Directory SSO(Single Sign-On) 연결 | Microsoft Docs'
description: Azure Active Directory 및 Cisco Webex 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 02/17/2021
ms.author: jeedes
ms.openlocfilehash: ad6d5308638b112afe2b51c4e149f876651e429d
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104592526"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-cisco-webex"></a>자습서: Cisco Webex와 Azure Active Directory SSO(Single Sign-On) 연결

이 자습서에서는 Azure AD(Azure Active Directory)와 Cisco Webex를 통합하는 방법에 대해 알아봅니다. Azure AD와 Cisco Webex를 통합하는 경우 다음을 수행할 수 있습니다.

* Cisco Webex에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어할 수 있습니다.
* 사용자가 해당 Azure AD 계정으로 Cisco Webex에 자동으로 로그온(Single Sign-On)되도록 설정할 수 있습니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* Cisco Webex SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* Cisco Webex에서 **SP** 시작 SSO를 지원합니다.
* Cisco Webex에서 [**자동 사용자 프로비저닝**](./cisco-webex-provisioning-tutorial.md)을 지원합니다.

## <a name="adding-cisco-webex-from-the-gallery"></a>갤러리에서 Cisco Webex 추가

Cisco Webex의 Azure AD 통합을 구성하려면 갤러리의 Cisco Webex를 관리되는 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **Cisco Webex** 를 입력합니다.
1. 결과 패널에서 **Cisco Webex** 를 선택한 다음, 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-cisco-webex"></a>Cisco Webex에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 Cisco Webex에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 Cisco Webex의 관련 사용자 간에 연결이 형성되어야 합니다.

Cisco Webex에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. 사용자가 이 기능을 사용할 수 있도록 **[Azure AD SSO를 구성](#configure-azure-ad-sso)** 합니다.
    1. **[Azure AD 테스트 사용자를 생성](#create-an-azure-ad-test-user)** 하여 B.Simon으로 Azure AD Single Sign-On을 테스트합니다.
    1. **[Azure AD 테스트 사용자를 할당](#assign-the-azure-ad-test-user)** 하여 B.Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
2. **[Cisco Webex 구성](#configure-cisco-webex)** - 애플리케이션 쪽에서 SSO 설정을 구성합니다.
    1. **[Cisco Webex 테스트 사용자 만들기](#create-cisco-webex-test-user)** - Azure AD 표현과 연결된 B.Simon에 해당하는 사용자를 Cisco Webex에 만듭니다.
3. **[SSO를 테스트](#test-sso)** 하여 구성이 작동하는지 여부를 확인합니다.

### <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **Cisco Webex** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

4. **기본 SAML 구성** 섹션에서 다음 단계를 수행하여 다운로드한 **서비스 공급자 메타데이터 파일** 을 업로드하고 애플리케이션을 구성합니다.

    >[!Note]
    >서비스 공급 기업 메타데이터 파일은 이 자습서의 뒷부분에 설명되어 있는 **Cisco Webex 구성** 섹션에서 구할 수 있습니다. 

    a. **메타데이터 파일 업로드** 를 클릭합니다.

    b. **폴더 로고** 를 클릭하여 메타데이터 파일을 선택하고 **업로드** 를 클릭합니다.

    다. 서비스 공급자 메타데이터 파일이 성공적으로 업로드되면 **기본 SAML 구성** 섹션에 **식별자** 및 **회신 URL** 값이 자동으로 채워집니다.

    **로그온 URL** 텍스트 상자에 SP 메타데이터 파일 업로드로 자동 입력되는 **회신 URL** 의 값을 붙여넣습니다.

1. Cisco Webex 애플리케이션은 특정 서식에서 SAML 어설션이 필요합니다. 이를 위해서는 SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다.

    ![이미지](common/default-attributes.png)

1. 위에서 언급한 특성 외에도 Cisco Webex 애플리케이션에는 아래에서 표시된 SAML 응답에서 다시 전달되어야 하는 몇 가지 특성이 추가로 필요합니다. 이러한 특성도 미리 채워져 있지만 요구 사항에 따라 검토할 수 있습니다.
  
    | Name |  원본 특성|
    | ---------------|--------- |
    | uid | user.userprincipalname |

    > [!NOTE]
    >  원본 특성 값은 기본적으로 userpricipalname에 매핑됩니다. 이는 Webex의 설정에 따라 user.mail, user.onpremiseuserprincipalname 또는 다른 값으로 변경할 수 있습니다.


1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML** 을 찾고, **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

   ![인증서 다운로드 링크](common/metadataxml.png)

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 Cisco Webex에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **Cisco Webex** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-cisco-webex"></a>Cisco Webex 구성

1. 관리자 자격 증명을 사용하여 Cisco Webex에 로그인합니다.

1. **조직 설정** 을 선택하고 **인증** 섹션 아래에서 **수정** 을 클릭합니다.

    ![스크린샷은 수정을 선택할 수 있는 인증 설정을 보여줍니다.](./media/cisco-spark-tutorial/organization-settings.png)
  
1. **타사 ID 공급자 통합 (고급)** 을 선택하고 **다음** 을 클릭합니다.

    ![스크린샷은 타사 ID 공급자 통합을 보여줍니다.](./media/cisco-spark-tutorial/enterprise-settings.png)

1. **메타데이터 파일 다운로드** 를 클릭하여 **서비스 공급자 메타데이터 파일** 을 다운로드하여 컴퓨터에 저장하고 **다음** 을 클릭합니다.

    ![스크린샷은 서비스 공급자 메타데이터 파일을 보여줍니다.](./media/cisco-spark-tutorial/sp-metadata.png)

1. **파일 브라우저** 옵션을 클릭하여 Azure AD 메타데이터 파일을 찾아 업로드합니다. 그런 다음 **메타데이터에서 인증 기관이 서명한 인증서 필요(더 안전)** 를 선택하고 **다음** 을 클릭합니다.

    ![스크린샷은 IdP 메타데이터 가져오기 페이지를 보여줍니다.](./media/cisco-spark-tutorial/idp-metadata.png)

1. **SSO 연결 테스트** 를 선택하고 새 브라우저 탭이 열리면 로그인하여 Azure AD로 인증합니다.

1. **Cisco Cloud Collaboration Management** 브라우저 탭으로 돌아갑니다. 테스트에 성공하면 **이 테스트에 성공했습니다. Single Sign-On 사용 옵션** 을 선택하고 **다음** 을 클릭합니다.

1. **저장** 을 클릭합니다.

> [!NOTE]
> Cisco Webex를 구성하는 방법에 대한 자세한 내용은 [이](https://help.webex.com/WBX000022701/How-Do-I-Configure-Microsoft-Azure-Active-Directory-Integration-with-Cisco-Webex-Through-Site-Administration#:~:text=In%20the%20Azure%20portal%2C%20select,in%20the%20Add%20Assignment%20dialog) 페이지를 참조하세요.

### <a name="create-cisco-webex-test-user"></a>Cisco Webex 테스트 사용자 만들기

이 섹션에서는 Cisco Webex에서 B.Simon이라는 사용자를 만듭니다. 이 애플리케이션은 비즈니스 규칙에 따라 자동 사용자 프로비저닝 및 프로비저닝 해제를 활성화하는 자동 사용자 프로비저닝을 지원합니다.  Microsoft는 가능하면 자동 프로비저닝을 사용할 것을 권장합니다. [Cisco Webex](./cisco-webex-provisioning-tutorial.md)에 대해 자동 프로비저닝을 사용하도록 설정하는 방법을 참조하세요.

사용자를 수동으로 만들어야 할 경우 다음 단계를 수행합니다.

1. 관리자 자격 증명을 사용하여 Cisco Webex에 로그인합니다.

2. **사용자**, **사용자 관리** 를 차례로 클릭합니다.
   
    ![스크린샷은 사용자를 관리할 수 있는 사용자 페이지를 보여줍니다.](./media/cisco-spark-tutorial/user-1.png) 

3. **사용자 관리** 창에서 **수동으로 사용자 추가 또는 수정** 을 선택합니다.

    ![스크린샷은 사용자를 관리하고 [수동으로 사용자 추가 또는 수정]을 선택할 수 있는 사용자 페이지를 보여줍니다.](./media/cisco-spark-tutorial/user-2.png)

4. **이름 및 전자 메일 주소** 를 선택합니다. 그런 다음 아래와 같이 텍스트 상자에 내용을 입력합니다.

    ![스크린샷은 사용자를 수동으로 추가하거나 수정할 수 있는 사용자 관리 대화 상자를 보여줍니다.](./media/cisco-spark-tutorial/user-3.png) 

    a. **이름** 텍스트 상자에서 사용자의 이름(예: **B**)을 입력합니다.

    b. **성** 텍스트 상자에서 사용자의 성(예: **Simon**)을 입력합니다.

    다. **이메일 주소** 텍스트 상자에서 사용자의 이메일 주소(예: b.simon@contoso.com)를 입력합니다.

5. 더하기 기호를 클릭하여 B.Simon을 추가합니다. 그런 후 **다음** 을 클릭합니다.

6. **사용자에 대한 서비스 추가** 창에서 **사용자 추가** 를 클릭한 다음, **마침** 을 클릭합니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 Cisco Webex 로그온 URL로 리디렉션됩니다. 

* Cisco Webex 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 Cisco Webex 타일을 클릭하면 Cisco Webex 로그온 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.


## <a name="next-steps"></a>다음 단계

Cisco Webex를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 반입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)