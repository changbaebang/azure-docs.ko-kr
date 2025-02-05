---
title: '자습서: BeyondTrust Remote Support와 Azure Active Directory SSO(Single Sign-On) 통합 | Microsoft Docs'
description: Azure Active Directory와 BeyondTrust Remote Support 간에 Single Sign-On을 구성하는 방법에 대해 알아봅니다.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 03/03/2021
ms.author: jeedes
ms.openlocfilehash: 1996024d163a4bf7cfa741110038bb8db5b883e8
ms.sourcegitcommit: b572ce40f979ebfb75e1039b95cea7fce1a83452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/11/2021
ms.locfileid: "102632749"
---
# <a name="tutorial-azure-active-directory-single-sign-on-sso-integration-with-beyondtrust-remote-support"></a>자습서: BeyondTrust Remote Support와 Azure Active Directory SSO(Single Sign-On) 통합

이 자습서에서는 Azure AD(Azure Active Directory)와 BeyondTrust Remote Support를 통합하는 방법에 대해 알아봅니다. BeyondTrust Remote Support를 Azure AD와 통합하는 경우 다음을 수행할 수 있습니다.

* BeyondTrust Remote Support에 대한 액세스 권한이 있는 사용자를 Azure AD에서 제어합니다.
* 사용자가 자신의 Azure AD 계정으로 BeyondTrust Remote Support에 자동으로 로그인되도록 설정합니다.
* 단일 중앙 위치인 Azure Portal에서 계정을 관리합니다.

## <a name="prerequisites"></a>사전 요구 사항

시작하려면 다음 항목이 필요합니다.

* Azure AD 구독 구독이 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 얻을 수 있습니다.
* BeyondTrust Remote Support SSO(Single Sign-On)가 설정된 구독

## <a name="scenario-description"></a>시나리오 설명

이 자습서에서는 테스트 환경에서 Azure AD SSO를 구성하고 테스트합니다.

* BeyondTrust Remote Support는 **SP** 시작 SSO를 지원합니다.
* BeyondTrust Remote Support는 **Just-In-Time** 사용자 프로비저닝을 지원합니다.

## <a name="adding-beyondtrust-remote-support-from-the-gallery"></a>갤러리에서 BeyondTrust Remote Support 추가

BeyondTrust Remote Support의 Azure AD 통합을 구성하려면 갤러리의 BeyondTrust Remote Support를 관리형 SaaS 앱 목록에 추가해야 합니다.

1. Azure Portal에 회사 또는 학교 계정, 개인 Microsoft 계정으로 로그인합니다.
1. 왼쪽 탐색 창에서 **Azure Active Directory** 서비스를 선택합니다.
1. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.
1. 새 애플리케이션을 추가하려면 **새 애플리케이션** 을 선택합니다.
1. **갤러리에서 추가** 섹션의 검색 상자에 **BeyondTrust Remote Support** 를 입력합니다.
1. 결과 패널에서 **BeyondTrust Remote Support** 를 선택하고 앱을 추가합니다. 앱이 테넌트에 추가될 때까지 잠시 동안 기다려 주세요.

## <a name="configure-and-test-azure-ad-sso-for-beyondtrust-remote-support"></a>BeyondTrust Remote Support에 대한 Azure AD SSO 구성 및 테스트

**B.Simon** 이라는 테스트 사용자를 사용하여 BeyondTrust Remote Support에서 Azure AD SSO를 구성하고 테스트합니다. SSO가 작동하려면 Azure AD 사용자와 BeyondTrust Remote Support의 관련 사용자 간에 연결 관계를 설정해야 합니다.

BeyondTrust Remote Support에서 Azure AD SSO를 구성하고 테스트하려면 다음 단계를 수행합니다.

1. **[Azure AD SSO 구성](#configure-azure-ad-sso)** - 사용자가 이 기능을 사용할 수 있도록 합니다.
    * **[Azure AD 테스트 사용자 만들기](#create-an-azure-ad-test-user)** - B.Simon을 사용하여 Azure AD Single Sign-On을 테스트합니다.
    * **[Azure AD 테스트 사용자 할당](#assign-the-azure-ad-test-user)** - B. Simon이 Azure AD Single Sign-On을 사용할 수 있도록 합니다.
1. **[BeyondTrust Remote Support SSO 구성](#configure-beyondtrust-remote-support-sso)** - 애플리케이션 쪽에서 Single Sign-On 설정을 구성합니다.
    * **[BeyondTrust Remote Support 테스트 사용자 만들기](#create-beyondtrust-remote-support-test-user)** - B.Simon의 Azure AD 표현과 연결된 해당 사용자를 BeyondTrust Remote Support에 만듭니다.
1. **[SSO 테스트](#test-sso)** - 구성이 작동하는지 여부를 확인합니다.

## <a name="configure-azure-ad-sso"></a>Azure AD SSO 구성

Azure Portal에서 Azure AD SSO를 사용하도록 설정하려면 다음 단계를 수행합니다.

1. Azure Portal의 **BeyondTrust Remote Support** 애플리케이션 통합 페이지에서 **관리** 섹션을 찾아 **Single Sign-On** 을 선택합니다.
1. **Single Sign-On 방법 선택** 페이지에서 **SAML** 을 선택합니다.
1. **SAML로 Single Sign-On 설정** 페이지에서 **기본 SAML 구성** 에 대한 편집(연필 모양) 아이콘을 클릭하여 설정을 편집합니다.

   ![기본 SAML 구성 편집](common/edit-urls.png)

1. **기본 SAML 구성** 섹션에서 다음 필드에 대한 값을 입력합니다.

    a. **식별자** 텍스트 상자에서 `https://<HOSTNAME>.bomgar.com` 패턴을 사용하는 URL을 입력합니다.

    b. **회신 URL** 텍스트 상자에서 `https://<HOSTNAME>.bomgar.com/saml/sso` 패턴을 사용하여 URL을 입력합니다.
    
    다. **로그인 URL** 텍스트 상자에서 `https://<HOSTNAME>.bomgar.com/saml` 패턴을 사용하여 URL을 입력합니다.

    > [!NOTE]
    > 이러한 값은 실제 값이 아닙니다. 실제 식별자, 회신 URL 및 로그온 URL을 사용하여 이러한 값을 업데이트합니다. 이러한 값은 자습서의 뒷부분에서 설명합니다.

1. BeyondTrust Remote Support 애플리케이션에는 특정 형식의 SAML 어설션이 필요하므로, SAML 토큰 특성 구성에 사용자 지정 특성 매핑을 추가해야 합니다. 다음 스크린샷에서는 기본 특성의 목록을 보여 줍니다.

    ![이미지](common/default-attributes.png)

1. 위에서 언급한 특성 외에도 BeyondTrust Remote Support 애플리케이션에는 아래에 표시된 SAML 응답에서 다시 전달되어야 하는 몇 가지 특성이 추가로 필요합니다. 이러한 특성도 미리 채워져 있지만 요구 사항에 따라 검토할 수 있습니다.

    | Name |  원본 특성|
    | ---------------| ----------|
    | 사용자 이름 | user.userprincipalname |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |
    | 그룹 | user.groups |

    > [!NOTE]
    > BeyondTrust Remote Support 애플리케이션에 대한 Azure AD 그룹을 할당할 때 '클레임에서 반환된 그룹' 옵션을 [없음]에서 [SecurityGroup]으로 수정해야 합니다. 그룹은 애플리케이션에 개체 ID로 가져오게 됩니다. Azure AD 그룹의 개체 ID는 Azure Active Directory 인터페이스에서 속성을 확인하여 찾을 수 있습니다. Azure AD 그룹을 참조하고 올바른 그룹 정책에 할당하는 데 필요합니다.

1. 고유한 사용자 ID를 설정할 때 이 값을 NameID 형식으로 설정해야 합니다. **영구적**. 사용자를 올바르게 식별하고 사용 권한에 대한 올바른 그룹 정책에 연결하려면 이 식별자가 영구적 식별자여야 합니다. 편집 아이콘을 클릭하여 **사용자 특성 및 클레임** 대화 상자를 열고 고유한 사용자 ID 값을 편집합니다.

1. **클레임 관리** 섹션에서 **이름 식별자 형식 선택** 을 클릭하고, 값을 **영구적** 으로 설정하고, **저장** 을 클릭합니다.

    ![사용자 특성 및 클레임](./media/bomgarremotesupport-tutorial/attribute-unique-user-identifier.png)

1. **SAML로 Single Sign-On 설정** 페이지의 **SAML 서명 인증서** 섹션에서 **페더레이션 메타데이터 XML** 을 찾고, **다운로드** 를 선택하여 인증서를 컴퓨터에 다운로드 및 저장합니다.

    ![인증서 다운로드 링크](common/metadataxml.png)

1. **BeyondTrust Remote Support 설정** 섹션에서 요구 사항에 따라 적절한 URL을 복사합니다.

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

이 섹션에서는 Azure Single Sign-On을 사용할 수 있도록 B.Simon에게 BeyondTrust Remote Support에 대한 액세스 권한을 부여합니다.

1. Azure Portal에서 **엔터프라이즈 애플리케이션** 을 선택한 다음, **모든 애플리케이션** 을 선택합니다.
1. 애플리케이션 목록에서 **BeyondTrust Remote Support** 를 선택합니다.
1. 앱의 개요 페이지에서 **관리** 섹션을 찾고 **사용자 및 그룹** 을 선택합니다.
1. **사용자 추가** 를 선택한 다음, **할당 추가** 대화 상자에서 **사용자 및 그룹** 을 선택합니다.
1. **사용자 및 그룹** 대화 상자의 사용자 목록에서 **B.Simon** 을 선택한 다음, 화면 아래쪽에서 **선택** 단추를 클릭합니다.
1. 사용자에게 역할을 할당할 것으로 예상되는 경우 **역할 선택** 드롭다운에서 선택할 수 있습니다. 이 앱에 대한 역할이 설정되지 않은 경우 "기본 액세스" 역할이 선택된 것으로 표시됩니다.
1. **할당 추가** 대화 상자에서 **할당** 단추를 클릭합니다.

## <a name="configure-beyondtrust-remote-support-sso"></a>BeyondTrust Remote Support SSO 구성

1. 다른 웹 브라우저 창에서 BeyondTrust Remote Support에 관리자로 로그인합니다.

1. **사용자 및 보안** > **보안 공급자** 로 이동합니다.

1. **SAML 공급자** 에서 **편집** 아이콘을 클릭합니다.

    ![SAML 공급자 편집 아이콘](./media/bomgarremotesupport-tutorial/saml-providers.png)

1. **서비스 공급자 설정** 섹션을 확장합니다.

1. **서비스 공급자 메타데이터 다운로드** 를 클릭하거나 **엔터티 ID** 및 **ACS URL** 값을 복사하고, Azure Portal의 **기본 SAML 구성** 섹션에서 이러한 값을 사용할 수 있습니다.

    ![서비스 공급자 메타데이터 다운로드](./media/bomgarremotesupport-tutorial/service-provider-metadata.png)


1. ID 공급자 설정 섹션에서 **ID 공급자 메타데이터 업로드** 를 클릭하고 Azure Portal에서 다운로드한 메타데이터 XML 파일을 찾습니다.

1.  **엔터티 ID**, **Single Sign-On 서비스 URL** 및 **서버 인증서** 가 자동으로 업로드되며, **SSO URL 프로토콜 바인딩** 을 **HTTP POST** 로 변경해야 합니다.

    ![스크린샷은 이러한 작업을 수행하는 ID 공급자 설정 섹션을 보여줍니다.](./media/bomgarremotesupport-tutorial/identity-provider.png)

1. **Save** 를 클릭합니다.

### <a name="create-beyondtrust-remote-support-test-user"></a>BeyondTrust Remote Support 테스트 사용자 만들기

이 섹션에서는 BeyondTrust Remote Support에서 Britta Simon이라는 사용자를 만듭니다. BeyondTrust Remote Support는 기본적으로 사용하도록 설정되는 Just-In-Time 사용자 프로비저닝을 지원합니다. 이 섹션에 작업 항목이 없습니다. BeyondTrust Remote Support에 사용자가 아직 없는 경우 인증 후에 새 사용자가 만들어집니다.

BeyondTrust Remote Support를 구성하는 데 필수인 다음 절차를 따르세요.

여기서는 사용자 프로비저닝 설정을 구성하겠습니다. 이 섹션에 사용되는 값은 Azure Portal의 **사용자 특성 및 클레임** 섹션에서 참조됩니다. 이 값을 생성 시 가져오는 기본값으로 구성했지만, 필요한 경우 값을 사용자 지정할 수 있습니다.

![스크린샷은 사용자 값을 구성할 수 있는 사용자 프로비전 설정을 보여줍니다.](./media/bomgarremotesupport-tutorial/user-attribute.png)

> [!NOTE]
> 그룹 및 이메일 특성은 이 구현에 필요하지 않습니다. Azure AD 그룹을 활용하고 사용 권한에 대한 BeyondTrust Remote Support 그룹 정책에 할당할 때 그룹의 개체 ID는 Azure Portal에서 속성을 통해 참조해야 하며 '사용 가능한 그룹' 섹션에 배치해야 합니다. 이 작업이 완료되면 개체 ID/AD 그룹을 사용 권한에 대한 그룹 정책에 할당하는 데 사용할 수 있습니다.

![스크린샷은 멤버 자격 유형, 원본, 형식 및 개체 ID가 있는 IT 섹션을 보여줍니다.](./media/bomgarremotesupport-tutorial/config-user-2.png)

![스크린샷은 그룹 정책에 대한 기본 설정 페이지를 보여줍니다.](./media/bomgarremotesupport-tutorial/group-policy.png)

> [!NOTE]
> 또는 SAML2 보안 공급자에서 기본 그룹 정책을 설정할 수 있습니다. 이 옵션을 정의하면 SAML을 통해 인증하는 모든 사용자에게 그룹 정책 내에 지정된 사용 권한이 할당됩니다. 일반 멤버 정책은 사용 권한이 제한된 BeyondTrust Remote Support/권한 있는 원격 액세스에 포함되며, 이를 사용하여 인증을 테스트하고 사용자를 올바른 정책에 할당할 수 있습니다. 사용자는 첫 번째 인증 시도가 성공할 때까지 /login > 사용자 및 보안을 통해 SAML2 사용자 목록을 채우지 않습니다. 그룹 정책에 대한 추가 정보는 `https://www.beyondtrust.com/docs/remote-support/getting-started/admin/group-policies.htm` 링크에서 확인할 수 있습니다.

## <a name="test-sso"></a>SSO 테스트

이 섹션에서는 다음 옵션을 사용하여 Azure AD Single Sign-On 구성을 테스트합니다. 

* Azure Portal에서 **이 애플리케이션 테스트** 를 클릭합니다. 그러면 로그인 흐름을 시작할 수 있는 BeyondTrust Remote Support 로그온 URL로 리디렉션됩니다. 

* BeyondTrust Remote Support 로그온 URL로 직접 이동하여 해당 위치에서 로그인 흐름을 시작합니다.

* Microsoft 내 앱을 사용할 수 있습니다. 내 앱에서 BeyondTrust Remote Support 타일을 클릭하면 BeyondTrust Remote Support 로그인 URL로 리디렉션됩니다. 내 앱에 대한 자세한 내용은 [내 앱 소개](../user-help/my-apps-portal-end-user-access.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

BeyondTrust Remote Support를 구성한 후에는 세션 제어를 적용하여 조직의 중요한 데이터의 반출 및 침입을 실시간으로 보호할 수 있습니다. 세션 제어는 조건부 액세스에서 확장됩니다. [Microsoft Cloud App Security를 사용하여 세션 제어를 적용하는 방법 알아보기](/cloud-app-security/proxy-deployment-aad)