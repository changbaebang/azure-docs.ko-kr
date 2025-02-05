---
title: 빠른 시작 - Azure IoT Hub에 원격 분석 전송 빠른 시작(C#) | Microsoft Docs
description: 이 빠른 시작에서는 두 가지 샘플 C# 애플리케이션을 실행하여 시뮬레이션된 원격 분석을 IoT Hub로 보내고, 클라우드에서 처리할 원격 분석을 IoT Hub에서 읽습니다.
author: robinsh
manager: philmea
ms.author: robinsh
ms.service: iot-hub
services: iot-hub
ms.devlang: csharp
ms.topic: quickstart
ms.custom:
- mvc
- mqtt
- 'Role: Cloud Development'
- devx-track-azurecli
ms.date: 06/01/2020
ms.openlocfilehash: 914df5b80dee7da041b268a3aaf25ac493d0cf5b
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98624442"
---
# <a name="quickstart-send-telemetry-from-a-device-to-an-iot-hub-and-read-it-with-a-service-application-net"></a>빠른 시작: 디바이스에서 IoT 허브로 원격 분석을 보내고 서비스 애플리케이션(.NET)으로 읽습니다.

[!INCLUDE [iot-hub-quickstarts-1-selector](../../includes/iot-hub-quickstarts-1-selector.md)]

IoT Hub는 스토리지 또는 처리를 위해 IoT 디바이스에서 클라우드로 다량의 원격 분석 데이터를 수집할 수 있게 해주는 Azure 서비스입니다. 이 빠른 시작에서는 시뮬레이션된 디바이스 애플리케이션에서 IoT Hub를 통해 서비스 애플리케이션으로 원격 분석을 처리를 위해 보냅니다.

빠른 시작은 두 개의 미리 작성된 C# 애플리케이션을 사용합니다. 하나는 원격 분석을 보내고 다른 하나는 허브에서 원격 분석을 읽기 위한 것입니다. 이 두 애플리케이션을 실행하기 전에 IoT 허브를 만들고 허브에 디바이스를 등록합니다.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>필수 구성 요소

* 이 빠른 시작에서 실행하는 두 개의 샘플 애플리케이션은 C#을 사용하여 작성되었습니다. 개발 머신에 .NET Core SDK 3.1 이상이 필요합니다.

    [.NET](https://www.microsoft.com/net/download/all)에서 여러 플랫폼에 대한 .NET Core SDK를 다운로드할 수 있습니다.

    다음 명령을 사용하여 개발 컴퓨터에서 C#의 현재 버전을 확인할 수 있습니다.

    ```cmd/sh
    dotnet --version
    ```

    > [!NOTE]
    > 이 빠른 시작에서 원격 분석을 읽는 데 사용되는 Event Hubs 서비스 코드를 컴파일하려면 .NET Core SDK 3.1 이상이 권장됩니다.


* [https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip](https://github.com/Azure-Samples/azure-iot-samples-csharp/archive/master.zip)에서 Azure IoT C# 샘플을 다운로드하고 ZIP 보관 파일을 추출합니다.

* 방화벽에서 포트 8883이 열려 있는지 확인합니다. 이 빠른 시작의 디바이스 샘플은 포트 8883을 통해 통신하는 MQTT 프로토콜을 사용합니다. 이 포트는 일부 회사 및 교육용 네트워크 환경에서 차단될 수 있습니다. 이 문제를 해결하는 자세한 내용과 방법은 [IoT Hub에 연결(MQTT)](iot-hub-mqtt-support.md#connecting-to-iot-hub)을 참조하세요.

[!INCLUDE [azure-cli-prepare-your-environment.md](../../includes/azure-cli-prepare-your-environment-no-header.md)]

[!INCLUDE [iot-hub-cli-version-info](../../includes/iot-hub-cli-version-info.md)]

## <a name="create-an-iot-hub"></a>IoT Hub 만들기

[!INCLUDE [iot-hub-include-create-hub](../../includes/iot-hub-include-create-hub.md)]

## <a name="register-a-device"></a>디바이스 등록

연결을 위해 디바이스를 IoT Hub에 등록해야 합니다. 이 빠른 시작에서는 Azure Cloud Shell을 사용하여 시뮬레이션된 디바이스를 등록합니다.

1. Azure Cloud Shell에서 다음 명령을 실행하여 디바이스 ID를 만듭니다.

   **YourIoTHubName**: 이 자리 표시자를 IoT 허브용으로 선택한 이름으로 바꿉니다.

   **MyDotnetDevice**: 등록 중인 디바이스의 이름입니다. 표시된 대로 **MyDotnetDevice** 를 사용하는 것이 좋습니다. 다른 디바이스 이름을 선택하는 경우 이 문서 전체에서도 해당 이름을 사용해야 하며, 샘플 애플리케이션에서 디바이스 이름을 업데이트한 후 실행해야 합니다.

    ```azurecli-interactive
    az iot hub device-identity create --hub-name {YourIoTHubName} --device-id MyDotnetDevice
    ```

2. Azure Cloud Shell에서 다음 명령을 실행하여 방금 등록한 디바이스의 _디바이스 연결 문자열_ 을 가져옵니다.

   **YourIoTHubName**: 이 자리 표시자를 IoT 허브용으로 선택한 이름으로 바꿉니다.

    ```azurecli-interactive
    az iot hub device-identity connection-string show --hub-name {YourIoTHubName} --device-id MyDotnetDevice --output table
    ```

    다음과 같은 디바이스 연결 문자열을 기록해 둡니다.

   `HostName={YourIoTHubName}.azure-devices.net;DeviceId=MyDotnetDevice;SharedAccessKey={YourSharedAccessKey}`

    이 값은 빠른 시작의 뒷부분에서 사용합니다.

3. 또한 서비스 애플리케이션이 IoT 허브에 연결하고 메시지를 검색할 수 있도록 하려면 IoT 허브에서 _Event Hubs 호환 엔드포인트_, _Event Hubs 호환 경로_ 및 _서비스 기본 키_ 가 필요합니다. 다음 명령은 IoT 허브에 대해 이 값을 검색합니다.

   **YourIoTHubName**: 이 자리 표시자를 IoT 허브용으로 선택한 이름으로 바꿉니다.

    ```azurecli-interactive
    az iot hub show --query properties.eventHubEndpoints.events.endpoint --name {YourIoTHubName}

    az iot hub show --query properties.eventHubEndpoints.events.path --name {YourIoTHubName}

    az iot hub policy show --name service --query primaryKey --hub-name {YourIoTHubName}
    ```

    빠른 시작의 뒷부분에서 사용하기 위해 이 세 개의 값을 기록해 둡니다.

## <a name="send-simulated-telemetry"></a>시뮬레이션된 원격 분석 전송

시뮬레이션된 디바이스 애플리케이션은 IoT 허브의 디바이스 관련 엔드포인트에 연결하고 시뮬레이션된 온도 및 습도 원격 분석을 전송합니다.

1. 로컬 터미널 창에서 샘플 C# 프로젝트의 루트 폴더로 이동합니다. 그런 다음, **iot-hub\Quickstarts\SimulatedDevice** 폴더로 이동합니다.

2. 로컬 터미널 창에서 다음 명령을 실행하여 시뮬레이션된 디바이스 애플리케이션에 필요한 패키지를 설치합니다.

    ```cmd/sh
    dotnet restore
    ```

3. 로컬 터미널 창에서 다음 명령을 실행하여 이전에 기록해 둔 디바이스 연결 문자열로 시뮬레이션된 디바이스 애플리케이션을 빌드하고 실행합니다.

    ```cmd/sh
    dotnet run -- {DeviceConnectionString}
    ```

    다음 스크린샷에서는 시뮬레이션된 디바이스 애플리케이션에서 IoT 허브에 원격 분석을 보낼 때의 출력을 보여 줍니다.

    ![시뮬레이션된 디바이스 실행](media/quickstart-send-telemetry-dotnet/simulated-device.png)

## <a name="read-the-telemetry-from-your-hub"></a>허브에서 원격 분석 읽기

서비스 애플리케이션은 IoT Hub의 서비스 측 **이벤트** 엔드포인트에 연결합니다. 애플리케이션은 시뮬레이션된 디바이스에서 전송하는 디바이스-클라우드 메시지를 받습니다. IoT Hub 서비스 애플리케이션은 일반적으로 클라우드에서 실행되며 디바이스-클라우드 메시지를 수신하고 처리합니다.

1. 또 다른 로컬 터미널 창에서 샘플 C# 프로젝트의 루트 폴더로 이동합니다. 그런 다음, **iot-hub\Quickstarts\ReadD2cMessages** 폴더로 이동합니다.

2. 로컬 터미널 창에서 다음 명령을 실행하여 애플리케이션에 필요한 라이브러리를 설치합니다.

    ```cmd/sh
    dotnet restore
    ```

3. 로컬 터미널 창에서 다음 명령을 실행하여 매개 변수 옵션을 확인합니다.

    ```cmd/sh
    dotnet run
    ```

4. 로컬 터미널 창에서 다음 명령 중 하나를 실행하여 다음 항목이 포함된 애플리케이션을 빌드하고 실행합니다.

    ```cmd/sh
    dotnet run -- -c {EventHubConnectionString}
    ```

    또는

    ```cmd/sh
    dotnet run -- -e {EventHubCompatibleEndpoint} -n {EventHubName} -s {SharedAccessKey}
    ```

    다음 스크린샷에서는 시뮬레이션된 디바이스에서 허브에 보낸 원격 분석을 서비스 애플리케이션에서 받을 때의 출력을 보여줍니다.

    ![서비스 애플리케이션 실행](media/quickstart-send-telemetry-dotnet/read-device-to-cloud.png)

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [iot-hub-quickstarts-clean-up-resources](../../includes/iot-hub-quickstarts-clean-up-resources.md)]

## <a name="next-steps"></a>다음 단계

이 빠른 시작에서 IoT 허브를 설치하고, 디바이스를 등록하고, C# 애플리케이션을 사용하여 허브에 시뮬레이션된 원격 분석을 보내고, 간단한 서비스 애플리케이션을 사용하여 허브에서 원격 분석을 읽습니다.

서비스 애플리케이션에서 시뮬레이션된 디바이스를 제어하는 방법을 알아보려면 다음 빠른 시작을 계속합니다.

> [!div class="nextstepaction"]
> [빠른 시작: IoT 허브에 연결된 디바이스 제어](quickstart-control-device-dotnet.md)
