---
title: '자습서: Azure Active Directory를 사용하여 자동 사용자 프로비저닝을 수행하도록 OpenText Directory Services 구성 | Microsoft Docs'
description: 사용자 계정을 Azure AD에서 OpenText Directory Services로 자동으로 프로비저닝 및 프로비저닝 해제하는 방법을 알아봅니다.
services: active-directory
documentationcenter: ''
author: Zhchia
writer: Zhchia
manager: beatrizd
ms.assetid: ad55ba5f-c56c-4ed0-bdfd-163d2883ed80
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 10/01/2020
ms.author: Zhchia
ms.openlocfilehash: 2f31eddab1070d073d3fd5a4761dad597e42a2e0
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96181888"
---
# <a name="tutorial-configure-opentext-directory-services-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비저닝을 수행하도록 OpenText Directory Services 구성

이 자습서에서는 자동 사용자 프로비저닝을 구성하기 위해 OpenText Directory Services 및 Azure AD(Azure Active Directory) 모두에서 수행해야 하는 단계에 대해 설명합니다. 구성되면 Azure AD에서 Azure AD 프로비저닝 서비스를 사용하여 사용자 및 그룹을 OpenText Directory Services로 자동으로 프로비저닝 및 프로비저닝 해제합니다. 이 서비스의 기능, 작동 방법 및 질문과 대답에 대한 중요한 내용은 [Azure Active Directory를 사용하여 SaaS 애플리케이션의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제](../app-provisioning/user-provisioning.md)를 참조하세요. 


## <a name="capabilities-supported"></a>지원되는 기능
> [!div class="checklist"]
> * OpenText Directory Services에서 사용자 만들기
> * OpenText Directory Services에서 더 이상 액세스할 필요가 없는 사용자 제거
> * 사용자 특성을 Azure AD와 OpenText Directory Services 간에 동기화된 상태로 유지
> * OpenText Directory Services에서 그룹 및 그룹 멤버 자격 프로비저닝
> * OpenText Directory Services에 [Single Sign-On](./opentext-directory-services-tutorial.md) 사용(추천)

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에 설명된 시나리오에서는 사용자에게 이미 다음 필수 구성 요소가 있다고 가정합니다.

* [Azure AD 테넌트](../develop/quickstart-create-new-tenant.md) 
* 프로비저닝을 구성할 [권한](../roles/permissions-reference.md)이 있는 Azure AD의 사용자 계정(예: 애플리케이션 관리자, 클라우드 애플리케이션 관리자, 애플리케이션 소유자 또는 전역 관리자). 
* Azure AD에서 액세스 할 수 있는 OTDS 설치

## <a name="step-1-plan-your-provisioning-deployment"></a>1단계. 프로비저닝 배포 계획
1. [프로비저닝 서비스의 작동 방식](../app-provisioning/user-provisioning.md)에 대해 알아봅니다.
2. [프로비저닝 범위](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에 있는 사용자를 결정합니다.
3. [Azure AD와 OpenText Directory Services 간에 매핑](../app-provisioning/customize-application-attributes.md)할 데이터를 결정합니다. 

## <a name="step-2-configure-opentext-directory-services-to-support-provisioning-with-azure-ad"></a>2단계. Azure AD를 사용하여 프로비저닝을 지원하도록 OpenText Directory Services 구성

> [!NOTE]
> 아래 단계는 OpenText Directory Services 설치에 적용됩니다. OpenText CoreShare 또는 OpenText OT2 테넌트에는 적용되지 않습니다.

1. 전용 기밀 **OAuth 클라이언트** 를 만듭니다.
2. 긴 **액세스 토큰 수명** 을 설정합니다.

      ![액세스 토큰 수명](media/open-text-directory-services-provisioning-tutorial/token-life.png)

3. 리디렉션 URL은 필요하지 않으므로 지정하지 않습니다. 
4. OTDS에서 **클라이언트 암호** 를 생성하고 표시합니다. **클라이언트 ID** 및 **클라이언트 암호** 를 안전한 위치에 저장합니다.

      ![클라이언트 암호](media/open-text-directory-services-provisioning-tutorial/client-secret.png)

5. Azure AD에서 동기화할 사용자 및 그룹에 대한 파티션을 만듭니다.

      ![파티션 페이지](media/open-text-directory-services-provisioning-tutorial/partition.png)

6. 동기화되는 Azure AD 사용자 및 그룹에 사용할 파티션에서 만든 OAuth 클라이언트에 관리 권한을 부여합니다.    
      * Partition(파티션) -> Actions(작업) -> Edit Administrators(관리자 편집)

      ![관리자 페이지](media/open-text-directory-services-provisioning-tutorial/administrator.png)

5. 비밀 토큰은 Azure AD에서 검색하고 구성해야 합니다. 이 작업에는 모든 HTTP 클라이언트 애플리케이션을 사용할 수 있습니다. OTDS에 포함된 Swagger API 애플리케이션을 사용하여 검색하는 단계는 다음과 같습니다.
      * 웹 브라우저에서 {OTDS URL}/otdsws/oauth2로 이동합니다.
      * /token으로 이동하여 오른쪽 위에 있는 잠금 아이콘을 클릭합니다. 이전에 검색한 OAuth 클라이언트 ID와 비밀을 각각 사용자 이름과 암호로 입력합니다. 권한 부여를 클릭합니다.

      ![권한 부여 단추](media/open-text-directory-services-provisioning-tutorial/authorization.png)

6. grant_type에 대해 **client_credentials** 를 선택하고, **Execute(실행)** 를 클릭합니다.

      ![Execute 단추](media/open-text-directory-services-provisioning-tutorial/execute.png)

7. 응답의 액세스 토큰은 Azure AD의 **비밀 토큰** 필드에서 사용해야 합니다.

      ![액세스 토큰](media/open-text-directory-services-provisioning-tutorial/access-token.png)

## <a name="step-3-add-opentext-directory-services-from-the-azure-ad-application-gallery"></a>3단계: Azure AD 애플리케이션 갤러리에서 OpenText Directory Services 추가

Azure AD 애플리케이션 갤러리에서 OpenText Directory Services를 추가하여 OpenText Directory Services로 프로비저닝 관리를 시작합니다. 이전에 SSO를 OpenText Directory Services에 사용하도록 설정한 경우 동일한 애플리케이션을 사용할 수 있습니다. 그러나 처음 통합을 테스트하는 경우 별도의 앱을 만드는 것이 좋습니다. [여기](../manage-apps/add-application-portal.md)를 클릭하여 갤러리에서 애플리케이션을 추가하는 방법에 대해 자세히 알아봅니다. 

## <a name="step-4-define-who-will-be-in-scope-for-provisioning"></a>4단계. 프로비저닝 범위에 있는 사용자 정의 

Azure AD 프로비저닝 서비스를 사용하면 애플리케이션에 대한 할당 또는 사용자/그룹의 특성을 기반으로 프로비저닝되는 사용자의 범위를 지정할 수 있습니다. 할당을 기준으로 앱에 프로비저닝할 사용자의 범위를 선택하려면 다음 [단계](../manage-apps/assign-user-or-group-access-portal.md)를 사용하여 애플리케이션에 사용자 및 그룹을 할당할 수 있습니다. 사용자 또는 그룹의 특성만을 기준으로 프로비저닝할 사용자의 범위를 선택하려면 [여기](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md) 설명된 대로 범위 지정 필터를 사용할 수 있습니다. 

* 사용자 및 그룹을 OpenText Directory Services에 할당할 때 **기본 액세스** 이외의 역할을 선택해야 합니다. 기본 액세스 역할이 있는 사용자는 프로비저닝에서 제외되고 프로비저닝 로그에 실질적으로 권한을 부여받지 않은 것으로 표시됩니다. 애플리케이션에서 사용할 수 있는 유일한 역할이 기본 액세스 역할인 경우에는 [애플리케이션 매니페스트를 업데이트](../develop/howto-add-app-roles-in-azure-ad-apps.md)하여 역할을 더 추가할 수 있습니다. 

* 소규모로 시작합니다. 모든 사용자에게 배포하기 전에 소수의 사용자 및 그룹 집합으로 테스트합니다. 할당된 사용자 및 그룹으로 프로비저닝 범위가 설정된 경우 앱에 하나 또는 두 개의 사용자 또는 그룹을 할당하여 범위를 제어할 수 있습니다. 모든 사용자 및 그룹으로 범위가 설정된 경우 [특성 기반 범위 지정 필터](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)를 지정할 수 있습니다. 


## <a name="step-5-configure-automatic-user-provisioning-to-opentext-directory-services"></a>5단계. OpenText Directory Services에 대한 자동 사용자 프로비저닝 구성 

이 섹션에서는 Azure AD의 사용자 및/또는 그룹 할당에 따라 TestApp에서 사용자 및/또는 그룹을 만들고, 업데이트하고, 사용 해제하도록 Azure AD 프로비저닝 서비스를 구성하는 단계를 안내합니다.

### <a name="to-configure-automatic-user-provisioning-for-opentext-directory-services-in-azure-ad"></a>Azure AD에서 OpenText Directory Services에 대한 자동 사용자 프로비저닝을 구성하려면 다음을 수행합니다.

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. **엔터프라이즈 애플리케이션**, **모든 애플리케이션** 을 차례로 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **OpenText Directory Services** 를 선택합니다.

    ![애플리케이션 목록의 OpenText Directory Services 링크](common/all-applications.png)

3. **프로비전** 탭을 선택합니다.

    ![프로비저닝 탭](common/provisioning.png)

4. **프로비전 모드** 를 **자동** 으로 설정합니다.

    ![프로비저닝 탭 자동](common/provisioning-automatic.png)

5. **관리자 자격 증명** 섹션 아래에서 OpenText Directory Services 테넌트 URL을 입력합니다.
   * 비특정 테넌트 URL: {OTDS URL}/scim/{partitionName}
   * 특정 테넌트 URL: {OTDS URL}/otdstenant/{tenantID}/scim/{partitionName}

6. 2단계에서 검색한 비밀 토큰을 입력합니다. **연결 테스트** 를 클릭하여 Azure AD에서 OpenText Directory Services에 연결할 수 있는지 확인합니다. 연결이 실패하면 OpenText Directory Services 계정에 관리자 권한이 있는지 확인하고 다시 시도합니다.

      ![토큰](common/provisioning-testconnection-tenanturltoken.png)

6. **알림 이메일** 필드에 프로비저닝 오류 알림을 받을 개인 또는 그룹의 메일 주소를 입력하고, **오류가 발생할 경우 메일 알림 보내기** 확인란을 선택합니다.

    ![알림 이메일](common/provisioning-notification-email.png)

7. **저장** 을 선택합니다.

8. **매핑** 섹션 아래에서 **Azure Active Directory 사용자를 OpenText Directory Services에 동기화** 를 선택합니다.

9. **특성 매핑** 섹션에서 Azure AD에서 OpenText Directory Services로 동기화되는 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업을 위해 OpenText Directory Services의 사용자 계정을 일치시키는 데 사용됩니다. [일치하는 대상 특성](../app-provisioning/customize-application-attributes.md)을 변경하도록 선택하는 경우 OpenText Directory Services API에서 해당 특성에 따라 사용자를 필터링하도록 지원하는지 확인해야 합니다. **저장** 단추를 선택하여 변경 내용을 커밋합니다.

   |attribute|Type|
   |---|---|
   |userName|String|
   |활성|부울|
   |displayName|String|
   |title|String|
   |emails[type eq "work"].value|String|
   |preferredLanguage|String|
   |name.givenName|String|
   |name.familyName|String|
   |name.formatted|String|
   |addresses[type eq "work"].formatted|String|
   |addresses[type eq "work"].streetAddress|String|
   |addresses[type eq "work"].locality|String|
   |addresses[type eq "work"].region|String|
   |addresses[type eq "work"].postalCode|String|
   |addresses[type eq "work"].country|String|
   |phoneNumbers[type eq "work"].value|String|
   |phoneNumbers[type eq "mobile"].value|String|
   |phoneNumbers[type eq "fax"].value|String|
   |externalId|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:employeeNumber|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:department|String|
   |urn:ietf:params:scim:schemas:extension:enterprise:2.0:User:manager|참조| 

10. **매핑** 섹션 아래에서 **Azure Active Directory 그룹을 OpenText Directory Services에 동기화** 를 선택합니다.

11. **특성 매핑** 섹션에서 Azure AD에서 OpenText Directory Services로 동기화되는 그룹 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업을 위해 OpenText Directory Services의 그룹을 일치시키는 데 사용됩니다. **저장** 단추를 선택하여 변경 내용을 커밋합니다.

      |attribute|Type|
      |---|---|
      |displayName|String|
      |externalId|String|
      |members|참조|

12. 범위 지정 필터를 구성하려면 [범위 지정 필터 자습서](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)에서 제공하는 다음 지침을 참조합니다.

13. Azure AD 프로비저닝 서비스를 OpenText Directory Services에 사용하도록 설정하려면 **설정** 섹션에서 **프로비저닝 상태** 를 **켜기** 로 변경합니다.

    ![프로비전 상태 켜기로 전환](common/provisioning-toggle-on.png)

14. **설정** 의 **범위** 섹션에서 원하는 값을 선택하여 OpenText Directory Services에 프로비저닝하려는 사용자 및/또는 그룹을 정의합니다.

    ![프로비전 범위](common/provisioning-scope.png)

15. 프로비전할 준비가 되면 **저장** 을 클릭합니다.

    ![프로비전 구성 저장](common/provisioning-configuration-save.png)

이 작업은 **설정** 의 **범위** 섹션에 정의된 모든 사용자 및/또는 그룹의 초기 동기화 주기를 시작합니다. 초기 주기는 Azure AD 프로비저닝 서비스가 실행되는 동안 약 40분마다 발생하는 후속 주기보다 더 많은 시간이 걸립니다. 

## <a name="step-6-monitor-your-deployment"></a>6단계. 배포 모니터링
프로비저닝을 구성한 후에는 다음 리소스를 사용하여 배포를 모니터링합니다.

1. [프로비저닝 로그](../reports-monitoring/concept-provisioning-logs.md)를 사용하여 어떤 사용자가 성공적으로 프로비저닝되었는지 확인합니다.
2. [진행률 표시줄](../app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user.md)을 통해 프로비저닝 주기 상태와 완료 정도를 확인합니다.
3. 프로비저닝 구성이 비정상 상태로 보이면 애플리케이션이 격리됩니다. 격리 상태에 대한 자세한 내용은 [여기](../app-provisioning/application-provisioning-quarantine-status.md)를 참조하세요.  

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>다음 단계

* [프로비저닝 작업에 대한 로그를 검토하고 보고서를 받아보는 방법을 알아봅니다](../app-provisioning/check-status-user-account-provisioning.md).