---
title: '자습서: Azure Active Directory를 사용한 자동 사용자 프로비전을 위한 Zendesk 구성 | Microsoft Docs'
description: 사용자 계정을 Zendesk로 자동으로 프로비저닝 및 프로비저닝 해제하도록 Azure Active Directory를 구성하는 방법을 알아봅니다.
services: active-directory
author: zhchia
writer: zhchia
manager: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 08/06/2019
ms.author: jeedes
ms.openlocfilehash: 620dd8fd586352ebeaf097a8f870a606f8e06c01
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "94359717"
---
# <a name="tutorial-configure-zendesk-for-automatic-user-provisioning"></a>자습서: 자동 사용자 프로비전에 대한 Zendesk 구성

이 자습서에서는 사용자 및 그룹을 Zendesk로 자동으로 프로비저닝 및 프로비저닝 해제하도록 Azure AD(Azure Active Directory)를 구성하기 위해 Zendesk 및 Azure AD(Azure Active Directory)에서 수행하는 단계를 보여 줍니다.

> [!NOTE]
> 이 자습서에서는 Azure AD 사용자 프로비저닝 서비스를 기반으로 구축된 커넥터에 대해 설명합니다. 이 서비스의 기능, 작동 방법 및 질문과 대답에 대한 정보는 [Azure Active Directory를 사용하여 SaaS(Software as a Service) 애플리케이션의 사용자를 자동으로 프로비저닝 및 프로비저닝 해제](../app-provisioning/user-provisioning.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

이 자습서에서 설명한 시나리오에서는 사용자에게 다음 항목이 있다고 가정합니다.

* Azure AD 테넌트.
* Professional 계획 이상을 사용하도록 설정한 Zendesk 테넌트
* 관리자 권한이 있는 Zendesk의 사용자 계정

## <a name="add-zendesk-from-the-azure-marketplace"></a>Azure Marketplace에서 Zendesk 추가

Azure AD를 사용하여 사용자를 자동으로 프로비저닝하도록 Zendesk를 구성하기 전에 Zendesk를 Azure Marketplace에서 관리형 SaaS 애플리케이션 목록으로 추가해야 합니다.

Azure Marketplace에서 Zendesk를 추가하려면 다음 단계를 수행합니다.

1. [Azure Portal](https://portal.azure.com)의 왼쪽 탐색 창에서 **Azure Active Directory** 를 선택합니다.

    ![Azure Active Directory 아이콘](common/select-azuread.png)

2. **엔터프라이즈 애플리케이션** 으로 이동한 다음, **모든 애플리케이션** 을 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

3. 새 애플리케이션을 추가하려면 대화 상자 맨 위 있는 **새 애플리케이션** 을 선택합니다.

    ![새 애플리케이션 단추](common/add-new-app.png)

4. 검색 상자에 **Zendesk** 를 입력하고 결과 패널에서 **Zendesk** 를 선택합니다. 애플리케이션을 추가하려면 **추가** 를 선택합니다.

    ![결과 목록의 Zendesk](common/search-new-app.png)

## <a name="assign-users-to-zendesk"></a>Zendesk에 사용자 할당

Azure Active Directory는 *할당* 이라는 개념을 사용하여 어떤 사용자가 선택된 앱에 대한 액세스 권한을 부여받아야 하는지 판단합니다. 자동 사용자 프로비저닝의 컨텍스트에서 Azure AD의 애플리케이션에 할당된 사용자 또는 그룹만 동기화됩니다.

자동 사용자 프로비저닝을 구성하고 사용하도록 설정하려면 먼저 Zendesk에 액세스해야 하는 Azure AD의 사용자 또는 그룹을 결정합니다. 이러한 사용자 또는 그룹을 Zendesk에 할당하려면 [엔터프라이즈 앱에 사용자 또는 그룹 할당](../manage-apps/assign-user-or-group-access-portal.md)의 지침을 따르세요.

### <a name="important-tips-for-assigning-users-to-zendesk"></a>Zendesk에 사용자를 할당하기 위한 주요 팁

* Zendesk 역할은 현재 Azure Portal UI에 자동으로 동적으로 채워집니다. 사용자에게 Zendesk 역할을 할당하기 전에 Zendesk 테넌트에서 최신 역할을 검색하기 위해 Zendesk에 대해 초기 동기화가 완료되었는지 확인합니다.

* 단일 Azure AD 사용자를 Zendesk에 할당하여 초기 자동 사용자 프로비저닝 구성을 테스트하는 것이 좋습니다. 테스트에 성공한 후 추가 사용자 또는 그룹을 나중에 할당할 수 있습니다.

* 사용자를 Zendesk에 할당할 때 할당 대화 상자에서 유효한 애플리케이션별 역할(사용 가능한 경우)을 선택해야 합니다. **기본 액세스** 역할이 있는 사용자는 프로비전에서 제외됩니다.

## <a name="configure-automatic-user-provisioning-to-zendesk"></a>Zendesk에 대한 자동 사용자 프로비저닝 구성 

이 섹션에서는 Azure AD 프로비저닝 서비스를 구성하는 단계를 안내합니다. 이는 Azure AD의 사용자 또는 그룹 할당을 기반으로 Zendesk에서 사용자 또는 그룹을 만들고, 업데이트하고, 사용하지 않도록 설정하는 데 사용됩니다.

> [!TIP]
> Zendesk에 대해 SAML 기반 Single Sign-On을 사용하도록 설정할 수도 있습니다. [Zendesk Single Sign-On 자습서](zendesk-tutorial.md)의 지침을 따르세요. Single Sign-On은 자동 사용자 프로비저닝과 별개로 구성할 수 있지만, 이러한 두 기능은 서로 보완적입니다.

### <a name="configure-automatic-user-provisioning-for-zendesk-in-azure-ad"></a>Azure AD에서 Zendesk에 대한 자동 사용자 프로비저닝 구성

1. [Azure Portal](https://portal.azure.com)에 로그인합니다. **엔터프라이즈 애플리케이션** > **모든 애플리케이션** > **Zendesk** 를 선택합니다.

    ![엔터프라이즈 애플리케이션 블레이드](common/enterprise-applications.png)

2. 애플리케이션 목록에서 **Zendesk** 를 선택합니다.

    ![애플리케이션 목록의 Zendesk 링크](common/all-applications.png)

3. **프로비전** 탭을 선택합니다.

    ![Zendesk 프로비전](./media/zendesk-provisioning-tutorial/ZenDesk16.png)

4. **프로비전 모드** 를 **자동** 으로 설정합니다.

    ![Zendesk 프로비저닝 모드](./media/zendesk-provisioning-tutorial/ZenDesk1.png)

5. **관리자 자격 증명** 섹션 아래에서 Zendesk 계정의 관리 사용자 이름, 비밀 토큰 및 도메인을 입력합니다. 이러한 값의 예는 다음과 같습니다.

   * **관리자 사용자 이름** 상자에 Zendesk 테넌트의 관리자 계정에 대한 사용자 이름을 채웁니다. 예제는 admin@contoso.com입니다.

   * **비밀 토큰** 상자에 6단계에서 설명한 대로 비밀 토큰을 채웁니다.

   * **도메인** 상자에 Zendesk 테넌트의 하위 도메인을 채웁니다. 예를 들어 테넌트 URL이 `https://my-tenant.zendesk.com`인 계정의 하위 도메인은 **my-tenant** 입니다.

6. Zendesk 계정의 비밀 토큰은 **관리자** > **API** > **설정** 에 있습니다. **토큰 액세스** 가 **사용** 으로 설정되었는지 확인합니다.

    ![Zendesk 관리자 설정](./media/zendesk-provisioning-tutorial/ZenDesk4.png)

    ![Zendesk 비밀 토큰](./media/zendesk-provisioning-tutorial/ZenDesk2.png)

7. 5단계에 표시된 상자를 채운 후 **연결 테스트** 를 선택하여 Azure AD가 Zendesk에 연결할 수 있는지 확인합니다. 연결이 실패하면 Zendesk 계정에 관리자 권한이 있는지 확인한 후 다시 시도합니다.

    ![Zendesk 연결 테스트](./media/zendesk-provisioning-tutorial/ZenDesk19.png)

8. **알림 이메일** 상자에서 프로비저닝 오류 알림을 받을 사람 또는 그룹의 이메일 주소를 입력합니다. **오류가 발생할 경우 이메일 알림 보내기** 확인란을 선택합니다.

    ![Zendesk 알림 이메일](./media/zendesk-provisioning-tutorial/ZenDesk9.png)

9. **저장** 을 선택합니다.

10. **매핑** 섹션에서 **Synchronize Azure Active Directory Users to Zendesk**(Azure Active Directory 사용자를 Zendesk에 동기화)를 선택합니다.

    ![Zendesk 사용자 동기화](./media/zendesk-provisioning-tutorial/ZenDesk10.png)

11. **특성 매핑** 섹션에서 Azure AD에서 Zendesk로 동기화되는 사용자 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업 시 Zendesk의 사용자 계정을 일치시키는 데 사용됩니다. 변경 내용을 저장하려면 **저장** 을 선택합니다.

    ![Zendesk 일치 사용자 특성](./media/zendesk-provisioning-tutorial/ZenDesk11.png)

12. **매핑** 섹션에서 **Azure Active Directory 그룹을 Zendesk에 동기화** 를 선택합니다.

    ![Zendesk 그룹 동기화](./media/zendesk-provisioning-tutorial/ZenDesk12.png)

13. **특성 매핑** 섹션에서 Azure AD에서 Zendesk로 동기화되는 그룹 특성을 검토합니다. **일치** 속성으로 선택한 특성은 업데이트 작업을 위해 Zendesk의 그룹을 일치시키는 데 사용됩니다. 변경 내용을 저장하려면 **저장** 을 선택합니다.

    ![Zendesk 일치 그룹 특성](./media/zendesk-provisioning-tutorial/ZenDesk13.png)

14. 범위 지정 필터를 구성하려면 [범위 지정 필터 자습서](../app-provisioning/define-conditional-rules-for-provisioning-user-accounts.md)의 지침을 따르세요.

15. Zendesk에 대한 Azure AD 프로비저닝 서비스를 사용하도록 설정하려면 **설정** 섹션에서 **프로비전 상태** 를 **켜기** 로 변경합니다.

    ![Zendesk 프로비전 상태](./media/zendesk-provisioning-tutorial/ZenDesk14.png)

16. Zendesk에 프로비저닝할 사용자 또는 그룹을 정의합니다. **설정** 섹션의 **범위** 에 원하는 값을 선택합니다.

    ![Zendesk 범위](./media/zendesk-provisioning-tutorial/ZenDesk15.png)

17. 프로비저닝할 준비가 되면 **저장** 을 선택합니다.

    ![Zendesk 저장](./media/zendesk-provisioning-tutorial/ZenDesk18.png)

이 작업은 **설정** 의 **범위** 섹션에 정의된 모든 사용자 또는 그룹의 초기 동기화를 시작합니다. 초기 동기화는 이후 동기화보다 더 오랜 시간이 걸립니다. Azure AD 프로비저닝 서비스가 실행되는 동안 약 40분 간격으로 발생합니다. 

**동기화 세부 정보** 섹션을 사용하여 진행 상태를 모니터링하고 링크를 통해 프로비저닝 활동 보고서를 확인할 수 있습니다. 이 보고서는 Zendesk에서 Azure AD 프로비저닝 서비스가 수행하는 모든 작업을 설명합니다.

Azure AD 프로비저닝 로그를 읽는 방법에 대한 자세한 내용은 [자동 사용자 계정 프로비저닝에 대한 보고](../app-provisioning/check-status-user-account-provisioning.md)를 참조하세요.

## <a name="connector-limitations"></a>커넥터 제한 사항

* Zendesk는 **에이전트** 역할로만 사용자에 대한 그룹의 사용을 지원합니다. 자세한 내용은 [Zendesk 설명서](https://support.zendesk.com/hc/en-us/articles/203661966-Creating-managing-and-using-groups)를 참조하세요.

* 사용자 또는 그룹에 사용자 지정 역할을 할당하면 Azure AD 자동 사용자 프로비저닝 서비스도 **에이전트** 에 기본 역할을 할당합니다. 에이전트에만 사용자 지정 역할을 할당할 수 있습니다. 자세한 내용은 [Zendesk API 설명서](https://developer.zendesk.com/rest_api/docs/support/users#json-format-for-agent-or-admin-requests)를 참조하세요. 

## <a name="additional-resources"></a>추가 리소스

* [엔터프라이즈 앱에 대한 사용자 계정 프로비전 관리](../app-provisioning/configure-automatic-user-provisioning-portal.md)
* [Azure Active Directory로 애플리케이션 액세스 및 Single Sign-On을 구현하는 방법](../manage-apps/what-is-single-sign-on.md)

## <a name="next-steps"></a>다음 단계

* [프로비저닝 작업에 대한 로그를 검토하고 보고서를 받아보는 방법을 알아봅니다](../app-provisioning/check-status-user-account-provisioning.md).

<!--Image references-->
[1]: ./media/zendesk-tutorial/tutorial_general_01.png
[2]: ./media/zendesk-tutorial/tutorial_general_02.png
[3]: ./media/zendesk-tutorial/tutorial_general_03.png
