---
title: '자습서: Azure Active Directory를 사용하여 자동 사용자 프로비저닝을 수행하도록 15Five 구성 | Microsoft Docs'
description: 사용자 계정을 15Five로 자동으로 프로비저닝 및 프로비저닝을 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다.
services: active-directory
author: zchia
writer: zchia
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 07/26/2019
ms.author: zhchia
ms.openlocfilehash: 00f713e8d319d7ad8dcea014429c57d7fba40541
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96181223"
---
# <a name="tutorial-configure-15five-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비저닝을 수행하도록 15Five 구성

이 자습서에서는 사용자 및/또는 그룹을 [15Five](https://www.15five.com/pricing/)로 자동으로 프로비저닝 및 프로비저닝을 해제하도록 Azure AD를 구성하기 위해 15Five 및 Azure AD(Azure Active Directory)에서 수행하는 단계를 보여 줍니다. 이 서비스의 기능, 작동 방법 및 질문과 대답에 대한 중요한 내용은 Azure Active Directory를 사용하여 SaaS 애플리케이션의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제를 참조하세요.

> [!NOTE]
> 이 커넥터는 현재 공개 미리 보기로 있습니다. 미리 보기 기능의 Microsoft Azure 일반 사용 약관에 대한 자세한 내용은 [Microsoft Azure 미리 보기에 대한 추가 사용 조건](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)을 참조하세요.


## <a name="capabilities-supported"></a>지원되는 기능
> [!div class="checklist"]
> * 15Five에서 사용자 만들기
> * 15Five에서 더 이상 액세스할 필요가 없는 사용자 제거
> * 사용자 특성을 Azure AD와 15Five 간에 동기화된 상태로 유지
> * 15Five에서 그룹 및 그룹 멤버 자격 프로비저닝
> * 15Five에 [Single Sign-On](./15five-tutorial.md) 사용(추천)

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 필수 구성 요소가 있다고 가정합니다.

* [Azure AD 테넌트](../develop/quickstart-create-new-tenant.md)
* 프로비저닝을 구성할 [권한](../roles/permissions-reference.md)이 있는 Azure AD의 사용자 계정(예: 애플리케이션 관리자, 클라우드 애플리케이션 관리자, 애플리케이션 소유자 또는 전역 관리자).
* [15Five 테넌트](https://www.15five.com/pricing/)
* 관리자 권한이 있는 15Five의 사용자 계정

## <a name="step-1-plan-your-provisioning-deployment"></a>1단계. 프로비저닝 배포 계획
1. [프로비저닝 서비스의 작동 방식](../app-provisioning/user-provisioning.md)에 대해 알아봅니다.
2. [프로비저닝 범위](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에 있는 사용자를 결정합니다.
3. [Azure AD와 15Five 간에 매핑](../app-provisioning/customize-application-attributes.md)할 데이터를 결정합니다. 

## <a name="step-2-configure-15five-to-support-provisioning-with-azure-ad"></a>2단계. Azure AD를 사용하여 프로비저닝을 지원하도록 15Five 구성

Azure AD를 사용하여 자동 사용자 프로비저닝을 수행하도록 15Five를 구성하려면 먼저 15Five에서 SCIM 프로비저닝을 사용하도록 설정해야 합니다.

1. [15Five 관리자 콘솔](https://my.15five.com/)에 로그인합니다. **Features(기능) > Integrations(통합)** 로 차례로 이동합니다.

    :::image type="content" source="media/15five-provisioning-tutorial/integration.png" alt-text="15Five 관리 콘솔의 스크린샷. Integrations는 메뉴의 Features 아래에 표시되며, Features 및 Integrations가 모두 강조 표시되어 있습니다." border="false":::

2.  **SCIM 2.0** 을 클릭합니다.

    :::image type="content" source="media/15five-provisioning-tutorial/image00.png" alt-text="15Five 관리 콘솔의 Integrations 페이지에 대한 스크린샷. Tool(도구) 아래에 SCIM 2.0이 표시되어 있습니다." border="false":::

3.  **SCIM integration(SCIM 통합) > Generate OAuth token(OAuth 토큰 생성)** 으로 차례로 이동합니다.

    :::image type="content" source="media/15five-provisioning-tutorial/image02.png" alt-text="15Five 관리 콘솔의 SCIM integration 페이지에 대한 스크린샷. Generate OAuth token이 강조 표시되어 있습니다." border="false":::

4.  **SCIM 2.0 base URL(SCIM 2.0 기준 URL)** 및 **Access Token(액세스 토큰)** 에 대한 값을 복사합니다. 이 값은 Azure Portal에 있는 15Five 애플리케이션에 대한 [프로비저닝] 탭의 **테넌트 URL** 및 **비밀 토큰** 필드에 입력됩니다.
    
    :::image type="content" source="media/15five-provisioning-tutorial/image03.png" alt-text="SCIM integration 페이지의 스크린샷. Token(토큰) 테이블에서 SCIM 2.0 base URL 및 Access token 옆에 있는 값이 강조 표시되어 있습니다." border="false":::

## <a name="step-3-add-15five-from-the-azure-ad-application-gallery"></a>3단계: Azure AD 애플리케이션 갤러리에서 15Five 추가

Azure AD 애플리케이션 갤러리에서 15Five를 추가하여 15Five로 프로비저닝 관리를 시작합니다. 이전에 SSO를 15Five에 사용하도록 설정한 경우 동일한 애플리케이션을 사용할 수 있습니다. 그러나 처음 통합을 테스트하는 경우 별도의 앱을 만드는 것이 좋습니다. [여기](../manage-apps/add-application-portal.md)를 클릭하여 갤러리에서 애플리케이션을 추가하는 방법에 대해 자세히 알아봅니다. 

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>4단계. 프로비저닝 범위에 있는 사용자 정의 

Azure AD 프로비저닝 서비스를 사용하면 애플리케이션에 대한 할당 또는 사용자/그룹의 특성을 기반으로 프로비저닝되는 사용자의 범위를 지정할 수 있습니다. 할당을 기준으로 앱에 프로비저닝할 사용자의 범위를 선택하려면 다음 [단계](../manage-apps/assign-user-or-group-access-portal.md)를 사용하여 애플리케이션에 사용자 및 그룹을 할당할 수 있습니다. 사용자 또는 그룹의 특성만을 기준으로 프로비저닝할 사용자의 범위를 선택하려면 [여기](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md) 설명된 대로 범위 지정 필터를 사용할 수 있습니다. 

* 사용자 및 그룹을 15Five에 할당할 때 **기본 액세스** 이외의 역할을 선택해야 합니다. 기본 액세스 역할이 있는 사용자는 프로비저닝에서 제외되고 프로비저닝 로그에 실질적으로 권한을 부여받지 않은 것으로 표시됩니다. 애플리케이션에서 사용할 수 있는 유일한 역할이 기본 액세스 역할인 경우에는 [애플리케이션 매니페스트를 업데이트](../develop/howto-add-app-roles-in-azure-ad-apps.md)하여 역할을 더 추가할 수 있습니다. 

* 소규모로 시작합니다. 모든 사용자에게 배포하기 전에 소수의 사용자 및 그룹 집합으로 테스트합니다. 할당된 사용자 및 그룹으로 프로비저닝 범위가 설정된 경우 앱에 하나 또는 두 개의 사용자 또는 그룹을 할당하여 범위를 제어할 수 있습니다. 모든 사용자 및 그룹으로 범위가 설정된 경우 [특성 기반 범위 지정 필터](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)를 지정할 수 있습니다.

## <a name="step-5-configure-automatic-user-provisioning-to-15five"></a>5단계. 15Five에 대한 자동 사용자 프로비저닝 구성 

이 섹션에서는 Azure AD의 사용자 및/또는 그룹 할당에 따라 15Five에서 사용자 및/또는 그룹을 만들고, 업데이트하고, 사용 해제하도록 Azure AD 프로비저닝 서비스를 구성하는 단계를 안내합니다.

### <a name="to-configure-automatic-user-provisioning-for-15five-in-azure-ad"></a>Azure AD에서 15Five에 대한 자동 사용자 프로비저닝을 구성하려면 다음을 수행합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. **엔터프라이즈 애플리케이션**, **모든 애플리케이션** 을 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **15Five** 를 선택합니다.

    ![애플리케이션 목록의 15Five 링크](common/all-applications.png)

3. **프로비전** 탭을 선택합니다.

    ![프로비저닝 옵션이 호출된 관리 옵션의 스크린샷](common/provisioning.png)

4. **프로비전 모드** 를 **자동** 으로 설정합니다.

    ![자동 옵션이 호출된 프로비저닝 모드 드롭다운 목록의 스크린샷](common/provisioning-automatic.png)

5.  [관리자 자격 증명] 섹션 아래에서 이전에 검색한 **SCIM 2.0 base URL(SCIM 2.0 기준 URL) 및 Access Token(액세스 토큰)** 값을 각각 **테넌트 URL** 및 **비밀 토큰** 필드에 입력합니다. **연결 테스트** 를 클릭하여 Azure AD에서 15Five에 연결할 수 있는지 확인합니다. 연결이 실패하면 15Five 계정에 관리자 권한이 있는지 확인하고 다시 시도합니다.

    ![테넌트 URL + 토큰](common/provisioning-testconnection-tenanturltoken.png)

6. **알림 메일** 필드에 프로비저닝 오류 알림을 받을 개인 또는 그룹의 메일 주소를 입력하고, **오류가 발생할 경우, 메일 알림 보내기** 확인란을 선택합니다.

    ![알림 이메일](common/provisioning-notification-email.png)

7. **저장** 을 클릭합니다.

8. **매핑** 섹션 아래에서 **Azure Active Directory 사용자를 15Five에 동기화** 를 선택합니다.

9. **특성 매핑** 섹션에서 Azure AD에서 15Five로 동기화되는 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업을 위해 15Five의 사용자 계정을 일치시키는 데 사용됩니다. **저장** 단추를 선택하여 변경 내용을 커밋합니다.


   |attribute|Type|
   |---|---|
   |활성|부울|
   |title|String|
   |emails[type eq "work"].value|String|
   |userName|String|
   |name.givenName|String|
   |name.familyName|String|
   |externalId|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager|참조|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber|String|
   |urn:ietf:params:scim:schemas:extension:15Five:2.0:User:location|String|
   |urn:ietf:params:scim:schemas:extension:15Five:2.0:User:startDate|String|

10. **매핑** 섹션 아래에서 **Azure Active Directory 그룹을 15Five에 동기화** 를 선택합니다.

11. **특성 매핑** 섹션에서 Azure AD에서 15Five로 동기화되는 그룹 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업을 위해 15Five의 그룹을 일치시키는 데 사용됩니다. **저장** 단추를 선택하여 변경 내용을 커밋합니다.

      |attribute|Type|
      |---|---|
      |externalId|String|
      |displayName|String|
      |members|참조|

12. 범위 지정 필터를 구성하려면 [범위 지정 필터 자습서](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에서 제공하는 다음 지침을 참조합니다.

13. Azure AD 프로비저닝 서비스를 15Five에 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태** 를 **켜기** 로 변경합니다.

    ![프로비전 상태 켜기로 전환](common/provisioning-toggle-on.png)

14. **설정** 의 **범위** 섹션에서 원하는 값을 선택하여 15Five에 프로비저닝하려는 사용자 및/또는 그룹을 정의합니다.

    ![프로비전 범위](common/provisioning-scope.png)

15. 프로비전할 준비가 되면 **저장** 을 클릭합니다.

    ![프로비전 구성 저장](common/provisioning-configuration-save.png)

    이 작업은 **설정** 의 **범위** 섹션에 정의된 모든 사용자 및/또는 그룹의 초기 동기화를 시작합니다. 초기 동기화는 Azure AD 프로비전 서비스가 실행되는 동안 약 40분마다 발생하는 후속 동기화보다 더 많은 시간이 걸립니다.

## <a name="step-6-monitor-your-deployment"></a>6단계. 배포 모니터링
프로비저닝을 구성한 후에는 다음 리소스를 사용하여 배포를 모니터링합니다.

1. [프로비저닝 로그](../reports-monitoring/concept-provisioning-logs.md)를 사용하여 어떤 사용자가 성공적으로 프로비저닝되었는지 확인합니다.
2. [진행률 표시줄](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md)을 통해 프로비저닝 주기 상태와 완료 정도를 확인합니다.
3. 프로비저닝 구성이 비정상 상태로 보이면 애플리케이션이 격리됩니다. 격리 상태에 대한 자세한 내용은 [여기](../app-provisioning/application-provisioning-quarantine-status.md)를 참조하세요.  
    
## <a name="connector-limitations"></a>커넥터 제한 사항

* 15Five는 사용자에 대한 일시 삭제를 지원하지 않습니다.

## <a name="change-log"></a>로그 변경

* 2020년 6월 16일 - 사용자에 대한 "관리자" 엔터프라이즈 확장 특성과 "위치" 및 "시작 날짜" 사용자 지정 특성에 대한 지원이 추가되었습니다.

## <a name="additional-resources"></a>추가 리소스

* [Enterprise 앱에 대한 사용자 계정 프로비저닝 관리](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>다음 단계

* [프로비저닝 작업에서 로그를 검토하고 보고서를 확인하는 방법을 알아봅니다](../app-provisioning/check-status-user-account-provisioning.md).