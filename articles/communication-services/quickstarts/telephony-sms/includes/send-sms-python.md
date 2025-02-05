---
title: 파일 포함
description: 포함 파일
services: azure-communication-services
author: lakshmans
manager: ankita
ms.service: azure-communication-services
ms.subservice: azure-communication-services
ms.date: 03/11/2021
ms.topic: include
ms.custom: include file
ms.author: lakshmans
ms.openlocfilehash: e8424f6b5b7617b00de6dedbece3325f3c5513c8
ms.sourcegitcommit: 18a91f7fe1432ee09efafd5bd29a181e038cee05
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2021
ms.locfileid: "103622086"
---
Communication Services Python SMS 클라이언트 라이브러리를 사용하여 SMS 메시지를 보내 Azure Communication Services를 시작하세요.

이 빠른 시작을 완료하면 Azure 계정에서 USD 센트 이하의 작은 비용이 발생합니다.

<!--**TODO: update all these reference links as the resources go live**

[API reference documentation](../../../references/overview.md) | [Library source code](#todo-sdk-repo) | [Package (PiPy)](#todo-nuget) | [Samples](#todo-samples)--> 

## <a name="prerequisites"></a>필수 구성 요소

- 활성 구독이 있는 Azure 계정. [체험 계정을 만듭니다](https://azure.microsoft.com/free/?WT.mc_id=A261C142F). 
- [Python](https://www.python.org/downloads/) 2.7, 3.5 이상.
- 활성 Communication Services 리소스 및 연결 문자열입니다. [Communication Services 리소스를 만듭니다](../../create-communication-resource.md).
- SMS 지원 전화 번호입니다. [전화 번호를 가져옵니다](../get-phone-number.md).

### <a name="prerequisite-check"></a>필수 구성 요소 확인

- 터미널 또는 명령 창에서 `python --version` 명령을 실행하여 Python이 설치되어 있는지 확인합니다.
- Communication Services 리소스와 연결된 전화 번호를 보려면 [Azure Portal](https://portal.azure.com/)에 로그인하고 Communication Services 리소스를 찾아 왼쪽 탐색 창에서 **전화 번호** 탭을 엽니다.

## <a name="setting-up"></a>설치

### <a name="create-a-new-python-application"></a>새 Python 애플리케이션 만들기

터미널 또는 명령 창을 열어 앱에 대한 새 디렉터리를 만들고 해당 디렉터리로 이동합니다.

```console
mkdir sms-quickstart && cd sms-quickstart
```

텍스트 편집기를 사용하여 프로젝트 루트 디렉터리에 **send-sms.py** 라는 파일을 만들고 기본 예외 처리를 비롯한 프로그램의 구조를 추가합니다. 이 빠른 시작의 모든 소스 코드를 다음 섹션의 이 파일에 추가합니다.

```python
import os
from azure.communication.sms import SmsClient

try:
    # Quickstart code goes here
except Exception as ex:
    print('Exception:')
    print(ex)
```

### <a name="install-the-package"></a>패키지 설치

애플리케이션 디렉터리에 있는 동안 `pip install` 명령을 사용하여 Python 패키지용 Azure Communication Services SMS 클라이언트 라이브러리를 설치합니다.

```console
pip install azure-communication-sms --pre
```

## <a name="object-model"></a>개체 모델

다음 클래스 및 인터페이스는 Python용 Azure Communication Services SMS 클라이언트 라이브러리의 주요 기능 중 일부를 처리합니다.

| 이름                                  | 설명                                                  |
| ------------------------------------- | ------------------------------------------------------------ |
| SmsClient | 이 클래스는 모든 SMS 기능에 필요합니다. 구독 정보를 사용하여 인스턴스화하고 SMS 메시지를 보내는 데 사용합니다.                                                                                                                 |
| SmsSendResult               | 이 클래스는 SMS 서비스의 결과를 포함합니다.                                          |

## <a name="authenticate-the-client"></a>클라이언트 인증

연결 문자열로 **SmsClient** 를 인스턴스화합니다. 아래 코드는 `COMMUNICATION_SERVICES_CONNECTION_STRING`이라는 환경 변수에서 리소스에 대한 연결 문자열을 검색합니다. [리소스의 연결 문자열을 관리](../../create-communication-resource.md#store-your-connection-string)하는 방법을 알아봅니다.

```python
# This code demonstrates how to fetch your connection string
# from an environment variable.
connection_string = os.getenv('COMMUNICATION_SERVICES_CONNECTION_STRING')

# Create the SmsClient object which will be used to send SMS messages
sms_client = SmsClient.from_connection_string(connection_string)
```

## <a name="send-a-11-sms-message"></a>1:1 SMS 메시지 보내기

단일 수신자에게 SMS 메시지를 보내려면 단일 수신자 전화 번호로 **SmsClient** 에서 ```send``` 메서드를 호출합니다. 선택적 매개 변수를 전달하여 전달 보고서를 사용하도록 설정할지 여부를 지정하고 사용자 지정 태그를 설정할 수도 있습니다. 다음 코드를 **send-sms.py** 의 `try` 블록 끝에 추가합니다.

```python

# calling send() with sms values
sms_responses = sms_client.send(
    from_="<from-phone-number>",
    to="<to-phone-number>,
    message="Hello World via SMS",
    enable_delivery_report=True, # optional property
    tag="custom-tag") # optional property

```

`<from-phone-number>`를 Communication Services와 연결된 SMS 지원 전화 번호로 바꾸고, `<to-phone-number>`를 메시지를 보낼 전화 번호로 바꿔야 합니다. 

## <a name="send-a-1n-sms-message"></a>1:N SMS 메시지 보내기

SMS 메시지를 수신자 목록에 보내려면 수신자의 전화 번호 목록이 포함된 **SmsClient** 에서 ```send``` 메서드를 호출합니다. 선택적 매개 변수를 전달하여 전달 보고서를 사용하도록 설정할지 여부를 지정하고 사용자 지정 태그를 설정할 수도 있습니다. 다음 코드를 **send-sms.py** 의 `try` 블록 끝에 추가합니다.

```python

# calling send() with sms values
sms_responses = sms_client.send(
    from_="<from-phone-number>",
    to=["<to-phone-number-1>", "<to-phone-number-2>"],
    message="Hello World via SMS",
    enable_delivery_report=True, # optional property
    tag="custom-tag") # optional property

```

`<from-phone-number>`를 Communication Services와 연결된 SMS 지원 전화 번호로 바꾸고, `<to-phone-number-1>` 및 `<to-phone-number-2>`를 메시지를 보낼 전화 번호로 바꿔야 합니다. 

## <a name="optional-parameters"></a>선택적 매개 변수

`enable_delivery_report` 매개 변수는 전달 보고를 구성하는 데 사용할 수 있는 선택적 매개 변수입니다. 이 기능은 SMS 메시지가 전달될 때 이벤트를 내보내려는 시나리오에 유용합니다. SMS 메시지에 대한 전달 보고를 구성하려면 [SMS 이벤트 처리](../handle-sms-events.md)를 참조하세요.

`tag` 매개 변수는 사용자 지정 태그를 구성하는 데 사용할 수 있는 선택적 매개 변수입니다.

## <a name="run-the-code"></a>코드 실행

`python` 명령을 사용하여 애플리케이션 디렉터리에서 애플리케이션을 실행합니다.

```console
python send-sms.py
```
