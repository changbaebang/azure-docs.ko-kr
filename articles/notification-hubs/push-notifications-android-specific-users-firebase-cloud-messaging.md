---
title: Azure Notification Hubs를 사용하여 특정 Android 앱에 푸시 알림 보내기
description: Azure Notification Hubs를 사용하여 특정 Android 앱에 푸시 알림을 보내는 방법을 알아봅니다.
documentationcenter: android
services: notification-hubs
author: sethmanheim
manager: femila
editor: jwargo
ms.assetid: ae0e17a8-9d2b-496e-afd2-baa151370c25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: tutorial
ms.custom: mvc, devx-track-java
ms.date: 09/11/2019
ms.author: sethm
ms.reviewer: jowargo
ms.lastreviewed: 09/11/2019
ms.openlocfilehash: 870842074bb4a0012a48115586a8ad571275d470
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96022414"
---
# <a name="tutorial-send-push-notifications-to-specific-android-apps-using-azure-notification-hubs"></a>자습서: Azure Notification Hubs를 사용하여 특정 Android 앱에 푸시 알림 보내기

[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

이 자습서에서는 Azure Notification Hubs를 사용하여 특정 디바이스에서 특정 앱 사용자에게 푸시 알림을 보내는 방법을 보여 줍니다. [앱 백 엔드에서 등록](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) 지침 문서에 나와 있는 대로 ASP.NET WebAPI 백 엔드는 클라이언트를 인증하고 알림을 생성하는 데 사용됩니다. 이 자습서는 [자습서: Azure Notification Hubs 및 Firebase Cloud Messaging을 사용하여 Android 디바이스에 알림 푸시](notification-hubs-android-push-notification-google-fcm-get-started.md)

이 자습서에서 수행하는 단계는 다음과 같습니다.

> [!div class="checklist"]
> * 사용자를 인증하는 백 엔드 Web API 프로젝트를 만듭니다.  
> * Android 애플리케이션을 업데이트합니다.
> * 앱 테스트

## <a name="prerequisites"></a>필수 구성 요소

이 자습서를 시작하기 전에 [자습서: Azure Notification Hubs 및 Cloud Messaging을 사용하여 Android 디바이스에 알림 푸시](notification-hubs-android-push-notification-google-fcm-get-started.md)를 완료하세요.

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="create-the-android-project"></a>Android 프로젝트 만들기

다음 단계는 [자습서: Azure Notification Hubs 및 Firebase Cloud Messaging을 사용하여 Android 디바이스에 알림 푸시](notification-hubs-android-push-notification-google-fcm-get-started.md)

1. `res/layout/activity_main.xml` 파일을 열고 다음 콘텐츠 정의를 바꿉니다.

    그러면 사용자로 로그인할 수 있는 새 EditText 컨트롤이 추가됩니다. 또한 보내는 알림의 일부가 될 사용자 이름 태그 필드가 추가됩니다.

    ```xml
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools" android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/usernameText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="@string/usernameHint"
        android:layout_above="@+id/passwordText"
        android:layout_alignParentEnd="true" />
    <EditText
        android:id="@+id/passwordText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="@string/passwordHint"
        android:inputType="textPassword"
        android:layout_above="@+id/buttonLogin"
        android:layout_alignParentEnd="true" />
    <Button
        android:id="@+id/buttonLogin"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/loginButton"
        android:onClick="login"
        android:layout_above="@+id/toggleButtonFCM"
        android:layout_centerHorizontal="true"
        android:layout_marginBottom="24dp" />
    <ToggleButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textOn="WNS on"
        android:textOff="WNS off"
        android:id="@+id/toggleButtonWNS"
        android:layout_toLeftOf="@id/toggleButtonFCM"
        android:layout_centerVertical="true" />
    <ToggleButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textOn="FCM on"
        android:textOff="FCM off"
        android:id="@+id/toggleButtonFCM"
        android:checked="true"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true" />
    <ToggleButton
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textOn="APNS on"
        android:textOff="APNS off"
        android:id="@+id/toggleButtonAPNS"
        android:layout_toRightOf="@id/toggleButtonFCM"
        android:layout_centerVertical="true" />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessageTag"
        android:layout_below="@id/toggleButtonFCM"
        android:layout_centerHorizontal="true"
        android:hint="@string/notification_message_tag_hint" />
    <EditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/editTextNotificationMessage"
        android:layout_below="@+id/editTextNotificationMessageTag"
        android:layout_centerHorizontal="true"
        android:hint="@string/notification_message_hint" />
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/send_button"
        android:id="@+id/sendbutton"
        android:onClick="sendNotificationButtonOnClick"
        android:layout_below="@+id/editTextNotificationMessage"
        android:layout_centerHorizontal="true" />
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        android:id="@+id/text_hello"
        />
    </RelativeLayout>
    ```
2. `res/values/strings.xml` 파일을 열고 `send_button` 정의를 다음 줄로 바꿉니다. 그러면 `send_button`에 대한 문자열이 다시 정의되고 다른 컨트롤에 대한 문자열이 추가됩니다.

    ```xml
    <string name="usernameHint">Username</string>
    <string name="passwordHint">Password</string>
    <string name="loginButton">1. Sign in</string>
    <string name="send_button">2. Send Notification</string>
    <string name="notification_message_hint">Notification message</string>
    <string name="notification_message_tag_hint">Recipient username</string>
    ```

    `main_activity.xml` 그래픽 레이아웃은 다음 이미지와 같이 표시되어야 합니다.

    ![주 작업 X M L 그래픽 레이아웃의 모양을 표시하는 에뮬레이터의 스크린샷.][A1]
3. `MainActivity` 클래스와 동일한 패키지에서 `RegisterClient`라는 새 클래스를 만듭니다. 새 클래스 파일에 아래 코드를 사용합니다.

    ```java
  
    import java.io.IOException;
    import java.io.UnsupportedEncodingException;
    import java.util.Set;
    
    import org.apache.http.HttpResponse;
    import org.apache.http.HttpStatus;
    import org.apache.http.client.ClientProtocolException;
    import org.apache.http.client.HttpClient;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.client.methods.HttpPut;
    import org.apache.http.client.methods.HttpUriRequest;
    import org.apache.http.entity.StringEntity;
    import org.apache.http.impl.client.DefaultHttpClient;
    import org.apache.http.util.EntityUtils;
    import org.json.JSONArray;
    import org.json.JSONException;
    import org.json.JSONObject;
    
    import android.content.Context;
    import android.content.SharedPreferences;
    import android.util.Log;
    
    public class RegisterClient {
        private static final String PREFS_NAME = "ANHSettings";
        private static final String REGID_SETTING_NAME = "ANHRegistrationId";
        private String Backend_Endpoint;
        SharedPreferences settings;
        protected HttpClient httpClient;
        private String authorizationHeader;
    
        public RegisterClient(Context context, String backendEndpoint) {
            super();
            this.settings = context.getSharedPreferences(PREFS_NAME, 0);
            httpClient =  new DefaultHttpClient();
            Backend_Endpoint = backendEndpoint + "/api/register";
        }
    
        public String getAuthorizationHeader() {
            return authorizationHeader;
        }
    
        public void setAuthorizationHeader(String authorizationHeader) {
            this.authorizationHeader = authorizationHeader;
        }
    
        public void register(String handle, Set<String> tags) throws ClientProtocolException, IOException, JSONException {
            String registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
    
            JSONObject deviceInfo = new JSONObject();
            deviceInfo.put("Platform", "fcm");
            deviceInfo.put("Handle", handle);
            deviceInfo.put("Tags", new JSONArray(tags));
    
            int statusCode = upsertRegistration(registrationId, deviceInfo);
    
            if (statusCode == HttpStatus.SC_OK) {
                return;
            } else if (statusCode == HttpStatus.SC_GONE){
                settings.edit().remove(REGID_SETTING_NAME).commit();
                registrationId = retrieveRegistrationIdOrRequestNewOne(handle);
                statusCode = upsertRegistration(registrationId, deviceInfo);
                if (statusCode != HttpStatus.SC_OK) {
                    Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                    throw new RuntimeException("Error upserting registration");
                }
            } else {
                Log.e("RegisterClient", "Error upserting registration: " + statusCode);
                throw new RuntimeException("Error upserting registration");
            }
        }
    
        private int upsertRegistration(String registrationId, JSONObject deviceInfo)
                throws UnsupportedEncodingException, IOException,
                ClientProtocolException {
            HttpPut request = new HttpPut(Backend_Endpoint+"/"+registrationId);
            request.setEntity(new StringEntity(deviceInfo.toString()));
            request.addHeader("Authorization", "Basic "+authorizationHeader);
            request.addHeader("Content-Type", "application/json");
            HttpResponse response = httpClient.execute(request);
            int statusCode = response.getStatusLine().getStatusCode();
            return statusCode;
        }
    
        private String retrieveRegistrationIdOrRequestNewOne(String handle) throws ClientProtocolException, IOException {
            if (settings.contains(REGID_SETTING_NAME))
                return settings.getString(REGID_SETTING_NAME, null);
    
            HttpUriRequest request = new HttpPost(Backend_Endpoint+"?handle="+handle);
            request.addHeader("Authorization", "Basic "+authorizationHeader);
            HttpResponse response = httpClient.execute(request);
            if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                Log.e("RegisterClient", "Error creating registrationId: " + response.getStatusLine().getStatusCode());
                throw new RuntimeException("Error creating Notification Hubs registrationId");
            }
            String registrationId = EntityUtils.toString(response.getEntity());
            registrationId = registrationId.substring(1, registrationId.length()-1);
    
            settings.edit().putString(REGID_SETTING_NAME, registrationId).commit();
    
            return registrationId;
        }
    }
    ```

    이 구성 요소는 푸시 알림을 등록하기 위해 앱 백 엔드에 접속하는 데 필요한 REST 호출을 구현합니다. 또한 *앱 백 엔드에서 등록* 에 설명된 대로 알림 허브에서 생성된 [registrationId](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend)를 로컬로 저장합니다. 이 구성 요소는 **로그인** 단추를 클릭할 때 로컬 스토리지에 저장된 인증 토큰을 사용합니다.
4. `MainActivity` 클래스에서 `RegisterClient` 클래스에 대한 필드 및 ASP.NET 백 엔드의 엔드포인트에 대한 문자열을 추가합니다. `<Enter Your Backend Endpoint>`를 이전에 얻은 실제 백 엔드 엔드포인트으로 바꿔야 합니다. 예들 들어 `http://mybackend.azurewebsites.net`입니다.

    ```java
    private RegisterClient registerClient;
    private static final String BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
    FirebaseInstanceId fcm;
    String FCM_token = null;
    ```

5. `MainActivity` 클래스의 `onCreate` 메서드에서 `hub` 필드의 초기화를 제거하거나 주석 처리하고 `registerWithNotificationHubs` 메서드를 호출합니다. 그런 다음 `RegisterClient` 클래스의 인스턴스를 초기화할 코드를 추가합니다. 메서드에는 다음 줄이 포함되어야 합니다.

    ```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        mainActivity = this;
        FirebaseService.createChannelAndHandleNotifications(getApplicationContext());
        fcm = FirebaseInstanceId.getInstance();
        registerClient = new RegisterClient(this, BACKEND_ENDPOINT);
        setContentView(R.layout.activity_main);
    }
    ```
7. 다음 `import` 문을 `MainActivity.java` 파일에 추가합니다.

    ```java
    import android.util.Base64;
    import android.view.View;
    import android.widget.EditText;
    
    import android.widget.Button;
    import android.widget.ToggleButton;
    import java.io.UnsupportedEncodingException;
    import android.content.Context;
    import java.util.HashSet;
    import android.widget.Toast;
    import org.apache.http.client.ClientProtocolException;
    import java.io.IOException;
    import org.apache.http.HttpStatus;
    
    import android.os.AsyncTask;
    import org.apache.http.HttpResponse;
    import org.apache.http.client.methods.HttpPost;
    import org.apache.http.entity.StringEntity;
    import org.apache.http.impl.client.DefaultHttpClient;
    
    import android.app.AlertDialog;
    import android.content.DialogInterface;
    
    import com.google.firebase.iid.FirebaseInstanceId;
    import com.google.firebase.iid.InstanceIdResult;
    import com.google.android.gms.tasks.OnSuccessListener;
    import java.util.concurrent.TimeUnit;
    ```
8. onStart 메서드의 코드를 다음 코드로 바꿉니다.

    ```java
    super.onStart();
    Button sendPush = (Button) findViewById(R.id.sendbutton);
    sendPush.setEnabled(false);
    ```
9. 그런 다음, **로그인** 단추 클릭 이벤트를 처리하고 푸시 알림을 보내는 다음 메서드를 추가합니다.

    ```java
    public void login(View view) throws UnsupportedEncodingException {
        this.registerClient.setAuthorizationHeader(getAuthorizationHeader());

        final Context context = this;
        new AsyncTask<Object, Object, Object>() {
            @Override
            protected Object doInBackground(Object... params) {
                try {

                    FirebaseInstanceId.getInstance().getInstanceId().addOnSuccessListener(new OnSuccessListener<InstanceIdResult>() {
                        @Override
                        public void onSuccess(InstanceIdResult instanceIdResult) {
                            FCM_token = instanceIdResult.getToken();
                            Log.d(TAG, "FCM Registration Token: " + FCM_token);
                        }
                    });
                    TimeUnit.SECONDS.sleep(1);
                    registerClient.register(FCM_token, new HashSet<String>());
                } catch (Exception e) {
                    DialogNotify("MainActivity - Failed to register", e.getMessage());
                    return e;
                }
                return null;
            }

            protected void onPostExecute(Object result) {
                Button sendPush = (Button) findViewById(R.id.sendbutton);
                sendPush.setEnabled(true);
                Toast.makeText(context, "Signed in and registered.",
                        Toast.LENGTH_LONG).show();
            }
        }.execute(null, null, null);
    }

    private String getAuthorizationHeader() throws UnsupportedEncodingException {
        EditText username = (EditText) findViewById(R.id.usernameText);
        EditText password = (EditText) findViewById(R.id.passwordText);
        String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
        basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
        return basicAuthHeader;
    }

    /**
        * This method calls the ASP.NET WebAPI backend to send the notification message
        * to the platform notification service based on the pns parameter.
        *
        * @param pns     The platform notification service to send the notification message to. Must
        *                be one of the following ("wns", "fcm", "apns").
        * @param userTag The tag for the user who will receive the notification message. This string
        *                must not contain spaces or special characters.
        * @param message The notification message string. This string must include the double quotes
        *                to be used as JSON content.
        */
    public void sendPush(final String pns, final String userTag, final String message)
            throws ClientProtocolException, IOException {
        new AsyncTask<Object, Object, Object>() {
            @Override
            protected Object doInBackground(Object... params) {
                try {

                    String uri = BACKEND_ENDPOINT + "/api/notifications";
                    uri += "?pns=" + pns;
                    uri += "&to_tag=" + userTag;

                    HttpPost request = new HttpPost(uri);
                    request.addHeader("Authorization", "Basic "+ getAuthorizationHeader());
                    request.setEntity(new StringEntity(message));
                    request.addHeader("Content-Type", "application/json");

                    HttpResponse response = new DefaultHttpClient().execute(request);

                    if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                        DialogNotify("MainActivity - Error sending " + pns + " notification",
                                response.getStatusLine().toString());
                        throw new RuntimeException("Error sending notification");
                    }
                } catch (Exception e) {
                    DialogNotify("MainActivity - Failed to send " + pns + " notification ", e.getMessage());
                    return e;
                }

                return null;
            }
        }.execute(null, null, null);
    }
    ```

    **로그인** 단추에 대한 `login` 처리기는 입력 사용자 이름과 암호(이는 인증 체계에서 사용하는 모든 토큰을 나타냄)를 사용하여 기본 인증 토큰을 생성하고 `RegisterClient`를 사용하여 등록을 위한 백 엔드를 호출합니다.

    `sendPush` 메서드는 사용자 태그를 기반으로 사용자에 대한 보안 알림을 트리거하는 백 엔드를 호출합니다. `sendPush`에서 대상으로 하는 플랫폼 알림 서비스는 전달되는 `pns` 문자열에 따라 다릅니다.

10. `MainActivity` 클래스에 다음 `DialogNotify` 메서드를 추가합니다.

    ```java
    protected void DialogNotify(String title, String message)
    {
        AlertDialog alertDialog = new AlertDialog.Builder(MainActivity.this).create();
        alertDialog.setTitle(title);
        alertDialog.setMessage(message);
        alertDialog.setButton(AlertDialog.BUTTON_NEUTRAL, "OK",
                new DialogInterface.OnClickListener() {
                    public void onClick(DialogInterface dialog, int which) {
                        dialog.dismiss();
                    }
                });
        alertDialog.show();
    }
    ```
11. 다음과 같이 `MainActivity` 클래스에서 사용자가 선택한 플랫폼 알림 서비스를 사용하여 `sendPush` 메서드를 호출하도록 `sendNotificationButtonOnClick` 메서드를 업데이트합니다.

    ```java
    /**
    * Send Notification button click handler. This method sends the push notification
    * message to each platform selected.
    *
    * @param v The view
    */
    public void sendNotificationButtonOnClick(View v)
            throws ClientProtocolException, IOException {

        String nhMessageTag = ((EditText) findViewById(R.id.editTextNotificationMessageTag))
                .getText().toString();
        String nhMessage = ((EditText) findViewById(R.id.editTextNotificationMessage))
                .getText().toString();

        // JSON String
        nhMessage = "\"" + nhMessage + "\"";

        if (((ToggleButton)findViewById(R.id.toggleButtonWNS)).isChecked())
        {
            sendPush("wns", nhMessageTag, nhMessage);
        }
        if (((ToggleButton)findViewById(R.id.toggleButtonFCM)).isChecked())
        {
            sendPush("fcm", nhMessageTag, nhMessage);
        }
        if (((ToggleButton)findViewById(R.id.toggleButtonAPNS)).isChecked())
        {
            sendPush("apns", nhMessageTag, nhMessage);
        }
    }
    ```
12. `build.gradle` 파일에서 다음 줄을 `buildTypes` 섹션 다음의 `android` 섹션에 추가합니다.

    ```java
    useLibrary 'org.apache.http.legacy'
    ```
13. 앱이 API 수준 28(Android 9.0) 이상을 대상으로 하는 경우 `AndroidManifest.xml`의 `<application>` 요소 내에 다음 선언을 포함합니다.

    ```xml
    <uses-library
        android:name="org.apache.http.legacy"
        android:required="false" />
    ```
14. 프로젝트를 빌드합니다.

## <a name="test-the-app"></a>앱 테스트

1. Android Studio를 사용하여 디바이스 또는 에뮬레이터에서 애플리케이션을 실행합니다.
2. Android 앱에서 사용자 이름과 암호를 입력합니다. 둘 다 동일한 문자열 값이어야 하며 공백이나 특수 문자를 포함해서는 안 됩니다.
3. Android 앱에서 **로그인** 을 클릭합니다. **로그인 및 등록됨** 를 알리는 알림 메시지를 기다립니다. 이렇게 하면 **알림 보내기** 단추가 사용되도록 설정됩니다.

    ![로그인 후 사용자에게 알릴 Notification Hubs 앱의 모양을 보여주는 에뮬레이터의 스크린샷.][A2]
4. 토글 단추를 클릭하여 앱을 실행하고 사용자를 등록한 모든 플랫폼을 활성화합니다.
5. 알림 메시지를 받을 사용자의 이름을 입력합니다. 대상 디바이스에 이 사용자에 대한 알림이 등록되어 있어야 합니다.
6. 사용자가 푸시 알림 메시지로 받을 메시지를 입력합니다.
7. **Send Notification** 을 클릭합니다.  일치하는 사용자 이름 태그로 등록된 각 디바이스에 푸시 알림이 수신됩니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 등록에 태그가 연결된 특정 사용자에게 알림을 푸시하는 방법을 배웠습니다. 위치 기반 알림을 푸시하는 방법을 알아보려면 다음 자습서를 계속 진행합니다.

> [!div class="nextstepaction"]
>[위치 기반 알림 푸시](notification-hubs-push-bing-spatial-data-geofencing-notification.md)

[A1]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users.png
[A2]: ./media/notification-hubs-aspnet-backend-android-notify-users/android-notify-users-enter-password.png
