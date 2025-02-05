---
title: Windows Virtual Desktop 앱 그룹 관리 포털 - Azure
description: Azure Portal을 사용하여 Windows Virtual Desktop 앱 그룹을 관리하는 방법입니다.
author: Heidilohr
ms.topic: tutorial
ms.date: 10/09/2020
ms.author: helohr
manager: lizross
ms.openlocfilehash: ec26f021ffa581b0713973904c97349df83a08ef
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "91930274"
---
# <a name="tutorial-manage-app-groups-with-the-azure-portal"></a>자습서: Azure Portal을 사용하여 앱 그룹 관리

>[!IMPORTANT]
>이 콘텐츠는 Azure Resource Manager Windows Virtual Desktop 개체를 통해 Windows Virtual Desktop에 적용됩니다. Azure Resource Manager 개체 없이 Windows Virtual Desktop(클래식)을 사용하는 경우 [이 문서](./virtual-desktop-fall-2019/manage-app-groups-2019.md)를 참조하세요.

새 Windows Virtual Desktop 호스트 풀에 대해 생성된 기본 앱 그룹도 전체 데스크톱을 게시합니다. 뿐만 아니라 호스트 풀에 대한 하나 이상의 RemoteApp 애플리케이션 그룹을 만들 수 있습니다. 이 자습서에 따라 RemoteApp 앱 그룹을 만들고 개별 시작 메뉴 엡을 게시해 보세요.

이 자습서에서는 다음 방법을 알아봅니다.

> [!div class="checklist"]
> * RemoteApp 그룹 만들기
> * RemoteApp 프로그램에 액세스 권한을 부여합니다.

## <a name="create-a-remoteapp-group"></a>RemoteApp 그룹 만들기

Azure Portal 또는 PowerShell을 사용하여 호스트 풀 및 세션 호스트 VM을 이미 만든 경우 다음 프로세스를 사용하여 Azure Portal에서 애플리케이션 그룹을 추가할 수 있습니다.

1.  [Azure Portal](https://portal.azure.com/)에 로그인합니다.
   
    >[!NOTE]
    > US Gov 포털에 로그인하는 경우 [https://portal.azure.us/](https://portal.azure.us/)로 이동합니다.

2.  **Windows Virtual Desktop** 을 검색하여 선택합니다.

3. 애플리케이션 그룹을 직접 추가하거나 기존 호스트 풀에서 추가할 수 있습니다. 아래 옵션을 선택합니다.

    - 페이지 왼쪽의 메뉴에서 **애플리케이션 그룹** 을 선택한 다음, **+ 추가** 를 선택합니다.

    - 화면 왼쪽의 메뉴에서 **호스트 풀** 을 선택하고 호스트 풀의 이름을 선택하고 왼쪽의 메뉴에서 **애플리케이션 그룹** 을 선택한 다음, **+ 추가** 를 선택합니다. 이 경우 기본 탭에서 호스트 풀이 이미 선택되어 있습니다.

4. **기본** 탭에서 앱 그룹을 만들려는 **구독** 및 **리소스 그룹** 을 선택합니다. 기존 리소스 그룹을 선택하는 대신 새 리소스 그룹을 만들도록 선택할 수도 있습니다.

5. 드롭다운 메뉴에서 애플리케이션 그룹과 연결될 **호스트 풀** 을 선택합니다.

    >[!NOTE]
    >애플리케이션 그룹과 연결되는 호스트 풀을 선택해야 합니다. 세션 호스트에서 제공되는 앱 또는 데스크톱은 앱 그룹에 포함되고, 세션 호스트는 호스트 풀에 포함됩니다. 앱 그룹은 만드는 중에 호스트 풀과 연결되어야 합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Portal의 기본 탭에 대한 스크린샷](media/basics-tab.png)

6. **애플리케이션 그룹 유형** 아래에서 **RemoteApp** 을 선택한 다음, RemoteApp 이름을 입력합니다.

      > [!div class="mx-imgBorder"]
      > !["RemoteApp"이 강조 표시된 애플리케이션 그룹 유형 필드의 스크린샷](media/remoteapp-button.png)

7.  **다음: 할당 >** 탭을 선택합니다.

8.  개별 사용자 또는 사용자 그룹을 앱 그룹에 할당하려면 **+ Azure AD 사용자 또는 사용자 그룹 추가** 를 선택합니다.

9.  앱에 액세스 권한을 부여할 사용자를 선택합니다. 하나 또는 여러 사용자 및 사용자 그룹을 선택할 수 있습니다.

     > [!div class="mx-imgBorder"]
     > ![사용자 선택 메뉴의 스크린샷](media/select-users.png)

10.  **선택** 을 선택합니다.

11.  **다음: 애플리케이션>** 을 선택한 다음, **+ 애플리케이션 추가** 를 선택합니다.

12.  시작 메뉴에서 애플리케이션을 추가하려면 다음을 수행합니다.

      - **애플리케이션 원본** 아래의 드롭다운 메뉴에서 **시작 메뉴** 를 선택합니다. 다음으로, **애플리케이션** 아래의 드롭다운 메뉴에서 애플리케이션을 선택합니다.

     > [!div class="mx-imgBorder"]
     > ![시작 메뉴가 선택된 애플리케이션 추가 화면의 스크린샷](media/add-app-start.png)

      - **표시 이름** 에서 클라이언트의 사용자에게 표시될 애플리케이션의 이름을 입력합니다.

      - 다른 옵션을 그대로 두고, **저장** 을 선택합니다.

13.  특정 파일 경로에서 애플리케이션을 추가하려면 다음을 수행합니다.

      - **애플리케이션 원본** 아래의 드롭다운 메뉴에서 **파일 경로** 를 선택합니다.

      - **애플리케이션 경로** 에서 연결된 호스트 풀에 등록된 세션 호스트의 애플리케이션에 대한 경로를 입력합니다.

      - **애플리케이션 이름**, **표시 이름**, **아이콘 경로** 및 **아이콘 인덱스** 필드에서 애플리케이션의 세부 정보를 입력합니다.

      - **저장** 을 선택합니다.

     > [!div class="mx-imgBorder"]
     > ![파일 경로가 선택된 애플리케이션 추가 페이지의 스크린샷](media/add-app-file.png)

14.  애플리케이션 그룹에 추가하려는 모든 애플리케이션에 대해 이 프로세스를 반복합니다.

15.  다음으로, **다음: 작업 영역 >** 을 선택합니다.

16.  앱 그룹을 작업 영역에 등록하려면 **애플리케이션 그룹 등록** 에서 **예** 를 선택합니다. 나중에 앱 그룹을 등록하려면 **아니요** 를 선택합니다.

17.  **예** 를 선택하는 경우 기존 작업 영역을 선택하여 앱 그룹이 등록할 수 있습니다.

       >[!NOTE]
       >호스트 풀과 동일한 위치에 만든 작업 영역에만 앱 그룹을 등록할 수 있습니다. 또한, 이전에 새 앱 그룹과 동일한 호스트 풀의 다른 앱 그룹을 작업 영역에 등록한 경우 해당 앱 그룹이 선택되어 있지만 편집할 수는 없습니다. 호스트 풀의 모든 앱 그룹은 동일한 작업 영역에 등록해야 합니다.

     > [!div class="mx-imgBorder"]
     > ![이미 있는 작업 영역에 대한 애플리케이션 그룹 등록 페이지의 스크린샷. 호스트 풀이 미리 선택되어 있습니다.](media/register-existing.png)

18.  필요에 따라 작업 영역을 쉽게 구성할 수 있도록 태그를 만들려면 **다음: 태그 >** 를 선택하고 태그 이름을 입력합니다.

19.  완료되면 **검토 + 만들기** 를 선택합니다.

20.  유효성 검사 프로세스가 완료될 때까지 잠시 기다립니다. 완료되면 **만들기** 를 선택하여 앱 그룹을 배포합니다.

배포 프로세스에서 수행하는 작업은 다음과 같습니다.

- RemoteApp 앱 그룹을 만듭니다.
- 선택한 앱을 앱 그룹에 추가합니다.
- 게시된 앱 그룹을 선택한 사용자 및 사용자 그룹에 게시합니다.
- 앱 그룹을 등록하도록 선택한 경우 이 작업을 수행합니다.
- 나중에 다운로드하여 저장할 수 있는 구성에 따라 Azure Resource Manager 템플릿에 대한 링크를 만듭니다.

>[!IMPORTANT]
>각 Azure Active Directory 테넌트에 대해 200개의 애플리케이션 그룹만 만들 수 있습니다. 사용자의 피드를 검색하는 서비스 제한으로 인해 이 제한을 추가했습니다. 이 제한은 Windows Virtual Desktop(클래식)에서 만든 앱 그룹에는 적용되지 않습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 앱 그룹을 만들고, RemoteApp 프로그램을 사용하여 채우고, 앱 그룹에 사용자를 할당하는 방법을 알아보았습니다. 유효성 검사 호스트 풀을 만드는 방법을 알아보려면 다음 자습서를 참조하세요. 프로덕션 환경에 배포하기 전에 유효성 검사 호스트 풀을 사용하여 서비스 업데이트를 모니터링할 수 있습니다.

> [!div class="nextstepaction"]
> [서비스 업데이트의 유효성을 검사하기 위한 호스트 풀 만들기](./create-validation-host-pool.md)
