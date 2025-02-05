---
title: Azure Notification Hubs를 사용하여 Xamarin에 푸시 알림 보내기 | Microsoft Docs
description: 이 자습서에서 Azure Notification Hubs를 사용하여 Xamarin iOS 애플리케이션에 푸시 알림을 보내는 방법을 알아봅니다.
services: notification-hubs
keywords: ios 푸시 알림, 푸시 메시지, 푸시 알림, 푸시 메시지
documentationcenter: xamarin
author: sethmanheim
manager: femila
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: tutorial
ms.custom: mvc, devx-track-csharp
ms.date: 01/12/2021
ms.author: sethm
ms.reviewer: thsomasu
ms.lastreviewed: 05/23/2019
ms.openlocfilehash: ff1e5edad05ebd7157f71ad2e099ea88905be4f3
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98221139"
---
# <a name="tutorial-send-push-notifications-to-xamarinios-apps-using-azure-notification-hubs"></a>자습서: Azure Notification Hubs를 사용하여 Xamarin.iOS 앱에 푸시 알림 보내기

[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>개요

이 자습서에서는 Azure Notification Hubs를 사용하여 iOS 애플리케이션에 푸시 알림을 보내는 방법을 보여 줍니다. [APNs(Apple Push Notification service)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html)를 사용하여 푸시 알림을 받는 빈 Xamarin.iOS 앱을 만듭니다.

완료하면 알림 허브를 사용하여 앱을 실행하는 모든 디바이스로 푸시 알림을 브로드캐스트할 수 있습니다. 완성된 코드는 [NotificationHubs 앱][GitHub] 샘플에서 사용할 수 있습니다.

이 자습서에서는 다음 작업을 수행하는 코드를 생성/업데이트합니다.

> [!div class="checklist"]
> * 인증서 서명 요청 파일 생성
> * 푸시 알림에 대해 앱 등록
> * 앱용 프로비저닝 프로필 만들기
> * iOS 푸시 알림에 대해 알림 허브 구성
> * 테스트 푸시 알림 보내기

## <a name="prerequisites"></a>사전 요구 사항

* **Azure 구독**. Azure 구독이 아직 없는 경우 시작하기 전에 [Azure 체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
* [Xcode][Install Xcode]
* iOS 10 이상 호환 디바이스
* [Apple 개발자 프로그램](https://developer.apple.com/programs/) 멤버 자격
* [Mac용 Visual Studio]
  
  > [!NOTE]
  > iOS 푸시 알림에 대한 구성 요구 사항 때문에 시뮬레이터 대신 실제 iOS 디바이스(iPhone 또는 iPad)에서 애플리케이션 예제를 배포 및 테스트해야 합니다.

먼저 이 자습서를 완료해야 Xamarin.iOS 앱에 대한 다른 모든 Notification Hubs 자습서를 진행할 수 있습니다.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="connect-your-app-to-the-notification-hub"></a>알림 허브에 앱 연결

### <a name="create-a-new-project"></a>새 프로젝트 만들기

1. Visual Studio에서 새 iOS 프로젝트를 만들고, **단일 뷰 앱** 템플릿을 선택하고, **다음** 을 클릭합니다.

     ![Visual Studio - 애플리케이션 유형 선택][31]

2. 앱 이름 및 조직 식별자를 입력한 후, **다음** 을 클릭한 다음, **만들기** 를 클릭합니다.

3. 솔루션 보기에서 *Into.plist* 를 두 번 클릭하고, **ID** 아래에서 번들 식별자가 프로비전 프로필을 만들 때 사용한 식별자와 일치하는지 확인합니다. **서명** 아래에서 **팀** 에 대해 개발자 계정이 선택되고, "자동으로 서명 관리"가 선택되고, 서명 인증서 및 프로비전 프로필이 자동으로 선택되어 있는지 확인합니다.

    ![Visual Studio - iOS 앱 구성][32]

4. 솔루션 보기에서 `Entitlements.plist`를 두 번 클릭하고 **푸시 알림 사용** 이 선택되어 있는지 확인합니다.

    ![Visual Studio-iOS 자격 구성][33]

5. Azure Messaging 패키지를 추가합니다. [솔루션] 보기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** > **NuGet 패키지 추가** 를 차례로 선택합니다. **Xamarin.Azure.NotificationHubs.iOS** 를 검색하고 프로젝트에 이 패키지를 추가합니다.

6. 클래스에 새 파일을 추가하고, 이름을 `Constants.cs`로 지정하고, 다음 변수를 추가하고, 문자열 리터럴 자리 표시자를 `hubname` 및 앞에서 언급한 `DefaultListenSharedAccessSignature`로 바꿉니다.

    ```csharp
    // Azure app-specific connection string and hub path
    public const string ListenConnectionString = "<Azure DefaultListenSharedAccess Connection String>";
    public const string NotificationHubName = "<Azure Notification Hub Name>";
    ```

7. `AppDelegate.cs`에서 다음 using 문을 추가합니다.

    ```csharp
    using WindowsAzure.Messaging.NotificationHubs;
    using UserNotifications
    ```

8. `AppDelegate.cs`에서 `MSNotificationHubDelegate` 구현을 만듭니다.

    ```csharp
    public class AzureNotificationHubListener : MSNotificationHubDelegate
    {
        public override void DidReceivePushNotification(MSNotificationHub notificationHub, MSNotificationHubMessage message)
        {

        }
    }
    ```

9. `AppDelegate.cs`에서 다음 코드와 일치하도록 `FinishedLaunching()`을 업데이트합니다.

    ```csharp
    public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
    {
        // Set the Message listener
        MSNotificationHub.SetDelegate(new AzureNotificationHubListener());
        
        // Start the SDK
        MSNotificationHub.Start(ListenConnectionString, NotificationHubName);

        return true;
    }
    ```

10. `AppDelegate.cs`에서 `AzureNotificationHubListener` 클래스에 대한 `DidReceivePushNotification` 메서드를 구현합니다.

    ```csharp
    public override void DidReceivePushNotification(MSNotificationHub notificationHub, MSNotificationHubMessage message)
    {
        // This sample assumes { aps: { alert: { title: "Hello", body: "World" } } }
        var alertTitle = message.Title ?? "Notification";
        var alertBody = message.Body;

        var myAlert = UIAlertController.Create(alertTitle, alertBody, UIAlertControllerStyle.Alert);
        myAlert.AddAction(UIAlertAction.Create("OK", UIAlertActionStyle.Default, null));
        UIApplication.SharedApplication.KeyWindow.RootViewController.PresentViewController(myAlert, true, null);
    }
    ```

11. 디바이스에서 앱을 실행합니다.

## <a name="send-test-push-notifications"></a>테스트 푸시 알림 보내기

[Azure Portal]에서 *테스트 보내기* 옵션을 사용하여 앱에서 알림 수신을 테스트할 수 있습니다. 이렇게 하면 테스트 푸시 알림이 디바이스로 전송됩니다.

![Azure Portal - 보내기 테스트][30]

푸시 알림은 일반적으로 호환 라이브러리를 사용하는 Mobile Apps 또는 ASP.NET과 같은 백 엔드 서비스에서 전송됩니다. 백 엔드에서 라이브러리를 사용할 수 없는 경우 REST API를 직접 사용하여 알림 메시지를 보낼 수도 있습니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 백 엔드에 등록된 모든 iOS 디바이스로 브로드캐스트 알림을 보냈습니다. 특정 iOS 디바이스로 알림을 푸시하는 방법을 알아보려면 다음 자습서를 계속 진행합니다.

> [!div class="nextstepaction"]
>[특정 디바이스에 알림 푸시](notification-hubs-ios-xplat-segmented-apns-push-notification.md)

<!-- Images. -->
[6]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config.png
[7]: ./media/notification-hubs-ios-get-started/notification-hubs-apple-config-cert.png
[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png
[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png
[30]: ./media/notification-hubs-ios-get-started/notification-hubs-test-send.png
[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png
[32]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-app-settings.png
[33]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-entitlements-settings.png

<!-- URLs. -->
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: https://go.microsoft.com/fwlink/p/?LinkId=272456
[Mac용 Visual Studio]: https://visualstudio.microsoft.com/vs/mac/
[Local and Push Notification Programming Guide]: https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html
[Apple Push Notification Service fwlink]: https://go.microsoft.com/fwlink/p/?LinkId=272584
[GitHub]: https://github.com/xamarin/mobile-samples/tree/master/Azure/NotificationHubs
[Azure Portal]: https://portal.azure.com
