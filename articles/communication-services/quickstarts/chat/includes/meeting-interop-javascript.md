---
title: 빠른 시작 - Teams 모임 참가
author: askaur
ms.author: askaur
ms.date: 03/10/2021
ms.topic: quickstart
ms.service: azure-communication-services
ms.openlocfilehash: dd183e9088f24aa8b94955bc8ed2a68b4a7eb27c
ms.sourcegitcommit: 4bda786435578ec7d6d94c72ca8642ce47ac628a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103496181"
---
## <a name="joining-the-meeting-chat"></a>모임 채팅 참가 

Teams 상호 운용성을 사용하도록 설정하면 Communication Services 사용자가 호출 클라이언트 라이브러리를 사용하여 Teams 호출에 외부 사용자로 참가할 수 있습니다. 통화에 조인하면 채팅 통화에 참가자로 추가됩니다. 그러면 통화 중인 다른 사용자와 메시지를 주고받을 수 있습니다. 사용자는 통화에 조인하기 전에 전송된 채팅 메시지에 액세스할 수 없습니다. 모임에 참가하고 채팅을 시작하려면 다음 단계를 수행하면 됩니다.

## <a name="install-the-chat-packages"></a>채팅 패키지 설치

`npm install` 명령을 사용하여 필수 JavaScript용 Communication Services 클라이언트 라이브러리를 설치합니다.

```console
npm install @azure/communication-common --save

npm install @azure/communication-identity --save

npm install @azure/communication-signaling --save

npm install @azure/communication-chat --save

npm install @azure/communication-calling --save
```

`--save` 옵션은 라이브러리를 **package.json** 파일의 종속성으로 나열합니다.

## <a name="add-the-teams-ui-controls"></a>Teams UI 컨트롤 추가

index.html의 코드를 다음 코드 조각으로 바꿉니다.
페이지 맨 위에 있는 텍스트 상자는 Teams 모임 컨텍스트 및 모임 스레드 ID를 입력하는 데 사용됩니다. 'Teams 모임 참가' 단추는 지정된 모임에 참가하는 데 사용됩니다.
페이지 아래쪽에 채팅 팝업이 표시됩니다. 이를 사용하여 모임 스레드에서 메시지를 보낼 수 있으며 ACS 사용자가 구성원인 동안 스레드에서 보낸 메시지를 실시간으로 표시합니다.

```html
<!DOCTYPE html>
<html>
   <head>
      <title>Communication Client - Calling and Chat Sample</title>
      <style>
         body {box-sizing: border-box;}
         /* The popup chat - hidden by default */
         .chat-popup {
         display: none;
         position: fixed;
         bottom: 0;
         left: 15px;
         border: 3px solid #f1f1f1;
         z-index: 9;
         }
         .message-box {
         display: none;
         position: fixed;
         bottom: 0;
         left: 15px;
         border: 3px solid #FFFACD;
         z-index: 9;
         }
         .form-container {
         max-width: 300px;
         padding: 10px;
         background-color: white;
         }
         .form-container textarea {
         width: 90%;
         padding: 15px;
         margin: 5px 0 22px 0;
         border: none;
         background: #e1e1e1;
         resize: none;
         min-height: 50px;
         }
         .form-container .btn {
         background-color: #4CAF40;
         color: white;
         padding: 14px 18px;
         margin-bottom:10px;
         opacity: 0.6;
         border: none;
         cursor: pointer;
         width: 100%;
         }
         .container {
         border: 1px solid #dedede;
         background-color: #F1F1F1;
         border-radius: 3px;
         padding: 8px;
         margin: 8px 0;
         }
         .darker {
         border-color: #ccc;
         background-color: #ffdab9;
         margin-left: 25px;
         margin-right: 3px;
         }
         .lighter {
         margin-right: 20px;
         margin-left: 3px;
         }
         .container::after {
         content: "";
         clear: both;
         display: table;
         }
      </style>
   </head>
   <body>
      <h4>Azure Communication Services</h4>
      <h1>Calling and Chat Quickstart</h1>
          <input id="teams-link-input" type="text" placeholder="Teams meeting link"
        style="margin-bottom:1em; width: 300px;" />
          <input id="thread-id-input" type="text" placeholder="Chat thread id"
        style="margin-bottom:1em; width: 300px;" />
        <p>Call state <span style="font-weight: bold" id="call-state">-</span></p>
      <div>
        <button id="join-meeting-button" type="button">
            Join Teams Meeting
        </button>
        <button id="hang-up-button" type="button" disabled="true">
            Hang Up
        </button>
      </div>
      <div class="chat-popup" id="chat-box">
         <div id="messages-container"></div>
         <form class="form-container">
            <textarea placeholder="Type message.." name="msg" id="message-box" required></textarea>
            <button type="button" class="btn" id="send-message">Send</button>
         </form>
      </div>
      <script src="./bundle.js"></script>
   </body>
</html>
```

## <a name="enable-the-teams-ui-controls"></a>Teams UI 컨트롤 사용

client.js 파일의 내용을 다음 코드 조각으로 바꿉니다.

코드 조각 내에서 다음과 같이 바꿉니다. 
- `SECRET CONNECTION STRING`을 Communication Service의 연결 문자열로 
- `ENDPOINT URL`을 Communication Service의 엔드포인트 URL로

```javascript
// run using
// npx webpack-dev-server --entry ./client.js --output bundle.js --debug --devtool inline-source-map
import { CallClient, CallAgent } from "@azure/communication-calling";
import { AzureCommunicationUserCredential } from "@azure/communication-common";
import { CommunicationIdentityClient } from "@azure/communication-identity";
import { ChatClient } from "@azure/communication-chat";

let call;
let callAgent;
let chatClient;
let chatThreadClient;

const meetingLinkInput = document.getElementById('teams-link-input');
const threadIdInput = document.getElementById('thread-id-input');
const callButton = document.getElementById("join-meeting-button");
const hangUpButton = document.getElementById("hang-up-button");
const callStateElement = document.getElementById('call-state');

const messagesContainer = document.getElementById("messages-container");
const chatBox = document.getElementById("chat-box");
const sendMessageButton = document.getElementById("send-message");
const messagebox = document.getElementById("message-box");

var userId = '';
var messages = '';

async function init() {
  const connectionString = "<SECRET CONNECTION STRING>";
  const endpointUrl = "<ENDPOINT URL>";

  const identityClient = new CommunicationIdentityClient(connectionString);

  let identityResponse = await identityClient.createUser();
  userId = identityResponse.communicationUserId;
  console.log(
    `\nCreated an identity with ID: ${identityResponse.communicationUserId}`
  );

  let tokenResponse = await identityClient.issueToken(identityResponse, [
    "voip",
    "chat",
  ]);
  const { token, expiresOn } = tokenResponse;
  console.log(
    `\nIssued an access token that expires at ${expiresOn}:`
  );
  console.log(token);

  const callClient = new CallClient();
  const tokenCredential = new AzureCommunicationUserCredential(token);
  callAgent = await callClient.createCallAgent(tokenCredential);
  callButton.disabled = false;

  chatClient = new ChatClient(
    endpointUrl,
    new AzureCommunicationUserCredential(token)
  );

  console.log('Azure Communication Chat client created!');
}

init();

callButton.addEventListener("click", async () => {
  // join with meeting link
  call = callAgent.join({meetingLink: meetingLinkInput.value}, {});
    
  call.on('callStateChanged', () => {
        callStateElement.innerText = call.state;
  })
  // toggle button and chat box states
  chatBox.style.display = "block";
  hangUpButton.disabled = false;
  callButton.disabled = true;

  messagesContainer.innerHTML = messages;
  
  console.log(call);

  // open notifications channel
  await chatClient.startRealtimeNotifications();

  // subscribe to new message notifications
  chatClient.on("chatMessageReceived", (e) => {
    console.log("Notification chatMessageReceived!");
    
    if (e.sender.communicationUserId != userId) {
       renderReceivedMessage(e.content);
    }
    else {
       renderSentMessage(e.content);
    }
  });
  chatThreadClient = await chatClient.getChatThreadClient(threadIdInput.value);
});

async function renderReceivedMessage(message) {
   messages += '<div class="container lighter">' + message + '</div>';
   messagesContainer.innerHTML = messages;
}

async function renderSentMessage(message) {
   messages += '<div class="container darker">' + message + '</div>';
   messagesContainer.innerHTML = messages;
}

hangUpButton.addEventListener("click", async () => 
  {
    // end the current call
    await call.hangUp();

    // toggle button states
    hangUpButton.disabled = true;
    callButton.disabled = false;
    callStateElement.innerText = '-';

    // toggle chat states
    chatBox.style.display = "none";
    messages = "";
  });

sendMessageButton.addEventListener("click", async () =>
  {
      let message = messagebox.value;

      let sendMessageRequest = { content: message };
      let sendMessageOptions = { senderDisplayName : 'Jack' };
      let sendChatMessageResult = await chatThreadClient.sendMessage(sendMessageRequest, sendMessageOptions);
      let messageId = sendChatMessageResult.id;

      messagebox.value = '';
      console.log(`Message sent!, message id:${messageId}`);
  });
```

## <a name="get-a-teams-meeting-chat-thread-for-a-communication-services-user"></a>Communication Services 사용자를 위한 Teams 미팅 채팅 스레드 가져오기

Teams 모임 링크 및 채팅은 [그래프 문서](/graph/api/onlinemeeting-createorget?tabs=http&view=graph-rest-beta)에 자세히 설명된 Graph API를 사용하여 검색할 수 있습니다. Communication Services Calling SDK는 전체 Teams 미팅 링크를 수락합니다. 이 링크는 [`joinWebUrl` 속성](/graph/api/resources/onlinemeeting?view=graph-rest-beta)에서 액세스할 수 있는 `onlineMeeting` 리소스의 일부로 반환됩니다. [Graph API](/graph/api/onlinemeeting-createorget?tabs=http&view=graph-rest-beta)를 사용하면 `threadId`를 얻을 수도 있습니다. 응답에는 `threadID`를 포함하는 `chatInfo` 개체가 포함됩니다. 

또한 Teams 모임 초대 자체의 **모임 참가** URL에서 필요한 모임 정보 및 스레드 ID를 가져올 수 있습니다.
Teams 미팅 링크는 `https://teams.microsoft.com/l/meetup-join/meeting_chat_thread_id/1606337455313?context=some_context_here`와 같습니다. `threadId`는 링크의 `meeting_chat_thread_id` 위치에 있습니다. 사용하기 전에 `meeting_chat_thread_id`가 이스케이프되지 않았는지 확인합니다. `19:meeting_ZWRhZDY4ZGUtYmRlNS00OWZaLTlkZTgtZWRiYjIxOWI2NTQ4@thread.v2` 형식이어야 합니다.


## <a name="run-the-code"></a>코드 실행

webpack 사용자는 `webpack-dev-server`를 사용하여 앱을 빌드하고 실행할 수 있습니다. 다음 명령을 실행하여 로컬 웹 서버에서 애플리케이션 호스트를 번들로 묶습니다.

```console
npx webpack-dev-server --entry ./client.js --output bundle.js --debug --devtool inline-source-map
```

브라우저를 열고 http://localhost:8080/로 이동합니다. 다음이 표시되어야 합니다.

:::image type="content" source="../acs-join-teams-meeting-chat-quickstart.png" alt-text="완성된 JavaScript 애플리케이션의 스크린샷":::

텍스트 상자에 Teams 모임 링크와 스레드 ID를 삽입합니다. Teams 모임에 참가하려면 *팀 모임 참가* 를 누릅니다. ACS 사용자가 모임에 입장한 후 Communication Services 애플리케이션에서 채팅할 수 있습니다. 페이지 맨 아래에 있는 상자로 이동하여 채팅을 시작합니다.

> [!NOTE] 
> 현재는 Teams와의 상호 운용성 시나리오에 대해서만 메시지를 보내고 받고 편집할 수 있습니다. 입력 표시기 및 Communication Services 사용자와 같은 다른 기능에서는 아직 Teams 미팅에서 다른 사용자를 추가하거나 제거할 수 없습니다.  
