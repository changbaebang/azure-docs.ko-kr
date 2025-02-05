---
ms.openlocfilehash: 94044e95e83742487a0d4d650814a5324f07011a
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "101750449"
---
배포 매니페스트는 에지 디바이스에 배포되는 모듈을 정의합니다. 또한 해당 모듈에 대한 구성 설정을 정의합니다. 

다음 단계에 따라 템플릿 파일에서 매니페스트를 생성한 다음, 에지 디바이스에 배포합니다.

1. Visual Studio Code를 엽니다.
1. **AZURE IOT HUB** 창 옆에 있는 **추가 작업** 아이콘을 선택하여 IoT Hub 연결 문자열을 설정합니다. *src/cloud-to-device-console-app/appsettings.json* 파일에서 문자열을 복사할 수 있습니다. 

    ![IOT 연결 문자열 설정](../../../media/quickstarts/set-iotconnection-string.png)

> [!NOTE]
> IoT Hub에 대한 기본 제공 엔드포인트 정보를 제공하라는 메시지가 표시될 수 있습니다. 해당 정보를 가져오려면 Azure Portal에서 IoT Hub로 이동하여 왼쪽 탐색 창에서 **기본 제공 엔드포인트** 옵션을 찾습니다. 여기를 클릭하고 **Event Hub 호환 엔드포인트** 섹션에서 **Event Hub 호환 엔드포인트** 를 찾습니다. 상자의 텍스트를 복사하여 사용합니다. 엔드포인트는 다음과 같이 표시됩니다.  
    ```
    Endpoint=sb://iothub-ns-xxx.servicebus.windows.net/;SharedAccessKeyName=iothubowner;SharedAccessKey=XXX;EntityPath=<IoT Hub name>
    ```

1. **src/edge/deployment.template.json** 을 마우스 오른쪽 단추로 클릭하고 **IoT Edge 배포 매니페스트 생성** 을 선택합니다.

    ![IoT Edge 배포 매니페스트 생성](../../../media/quickstarts/generate-iot-edge-deployment-manifest.png)

    이렇게 하면 *src/edge/config* 폴더에 *deployment.amd64.json* 이라는 매니페스트 파일이 생성됩니다.
1. **src/edge/config/deployment.amd64.json** 을 마우스 오른쪽 단추로 클릭하고 **단일 디바이스용 배포 만들기** 를 선택하고 에지 디바이스의 이름을 선택합니다.

    ![단일 디바이스에 대한 배포 만들기](../../../media/quickstarts/create-deployment-single-device.png)

1. IoT Hub 디바이스를 선택하라는 메시지가 표시되면 드롭다운 메뉴에서 **lva-sample-device** 를 선택합니다.
1. 약 30초 후 창의 왼쪽 아래 모서리에서 Azure IoT Hub가 새로 고쳐집니다. 이제 에지 디바이스에 다음과 같은 배포된 모듈이 표시됩니다.

    * Live Video Analytics on IoT Edge(`lvaEdge` 모듈 이름)
    * RTSP(Real-Time Streaming Protocol) 시뮬레이터(`rtspsim` 모듈 이름)

RTSP 시뮬레이터 모듈은 [Live Video Analytics 리소스 설치 스크립트](https://github.com/Azure/live-video-analytics/tree/master/edge/setup)를 실행할 때 에지 디바이스에 복사된 비디오 파일을 사용하여 라이브 비디오 스트림을 시뮬레이션합니다. 

> [!NOTE]
> 설치 스크립트를 통해 프로비저닝된 에지 디바이스 대신 사용자 고유의 에지 디바이스를 사용하는 경우 에지 디바이스로 이동하고, **관리자 권한** 으로 다음 명령을 실행하여 이 빠른 시작에 사용되는 샘플 비디오 파일을 가져와 저장합니다.  

```
mkdir /home/lvaedgeuser/samples      
mkdir /home/lvaedgeuser/samples/input    
curl https://lvamedia.blob.core.windows.net/public/camera-300s.mkv > /home/lvaedgeuser/samples/input/camera-300s.mkv  
chown -R lvalvaedgeuser:localusergroup /home/lvaedgeuser/samples/  
```
이 단계에서는 모듈이 배포되었지만 미디어 그래프가 활성화되지 않았습니다.
