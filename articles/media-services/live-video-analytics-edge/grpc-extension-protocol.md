---
title: gRPC 확장 프로토콜 - Azure
description: 이 문서에서는 gRPC 확장 프로토콜을 사용하여 Live Video Analytics 모듈과 AI 또는 CV 사용자 지정 확장 간에 메시지를 보내는 방법에 대해 알아봅니다.
ms.topic: overview
ms.date: 09/14/2020
ms.openlocfilehash: f7b5be859702199b07dfa0d6a43a09ca8ff0c42f
ms.sourcegitcommit: e6de1702d3958a3bea275645eb46e4f2e0f011af
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102455859"
---
# <a name="grpc-extension-protocol"></a>gRPC 확장 프로토콜

IoT Edge의 Live Video Analytics를 사용하면 [그래프 확장 노드](/azure/media-services/live-video-analytics-edge/media-graph-extension-concept)를 통해 미디어 그래프 처리 기능을 확장할 수 있습니다. gRPC 확장 프로세서를 확장 노드로 사용하는 경우 Live Video Analytics 모듈과 AI 또는 CV 모듈 간의 통신은 gRPC 기반의 고성능 구조화된 프로토콜을 통해 이루어집니다.

이 문서에서는 gRPC 확장 프로토콜을 사용하여 Live Video Analytics 모듈과 AI 또는 CV 사용자 지정 확장 간에 메시지를 보내는 방법에 대해 알아봅니다.

gRPC는 모든 환경에서 실행되고 플랫폼 간 및 언어 간 통신을 지원하는 최신 오픈 소스 고성능 RPC 프레임워크입니다. gRPC 전송 서비스는 다음 사이에 HTTP/2 양방향 스트리밍을 사용합니다.

* gRPC 클라이언트(IoT Edge 모듈의 Live Video Analytics) 및 
* gRPC 서버(사용자 지정 확장)

gRPC 세션은 TCP/TLS 포트를 통해 gRPC 클라이언트에서 gRPC 서버로 연결되는 단일 연결입니다. 

단일 세션에서: 클라이언트는 gRPC 스트림 세션을 통해 미디어 스트림 설명자, 다음으로 비디오 프레임을 [protobuf](https://github.com/Azure/live-video-analytics/tree/master/contracts/grpc) 메시지로 서버에 보냅니다. 서버는 스트림 설명자의 유효성을 검사하고, 비디오 프레임을 분석하고, 유추 결과를 protobuf 메시지로 반환합니다. 

[유추 메타데이터 스키마 개체 모델](/azure/media-services/live-video-analytics-edge/inference-metadata-schema)에 따라 정의된 미리 설정된 스키마에 따라 유효한 JSON 문서를 사용하여 응답을 반환하는 것이 좋습니다. 이렇게 하면 다른 구성 요소와의 상호 운용성과 Live Video Analytics 모듈에 추가되는 향후 기능이 보다 효과적으로 보장됩니다.

![gRPC 확장 계약](./media/grpc-extension-protocol/grpc.png)

## <a name="implementing-grpc-protocol"></a>gRPC 프로토콜 구현

### <a name="creating-a-grpc-connection"></a>gRPC 연결 만들기

사용자 지정 확장은 다음 gRPC 서비스를 구현해야 합니다.

```
service MediaGraphExtension
    {
        rpc ProcessMediaStream(stream MediaStreamMessage) returns (stream MediaStreamMessage);
    }
```

이를 호출하면 gRPC 확장과 Live Video Analytics 그래프 간에 메시지를 전달하는 양방향 스트림이 열립니다. 각 파티에서 이 스트림에 보내는 첫 번째 메시지에는 다음 MediaSample에서 보내는 정보를 정의하는 MediaStreamDescriptor가 포함됩니다.

예를 들어 그래프 확장은 gRPC 메시지에 포함된 416x416 rgb24 인코딩 프레임을 사용자 지정 확장으로 보낼 것임을 나타내는 메시지(여기서는 JSON으로 표현됨)를 보낼 수 있습니다.

```
 {
    "sequence_number": 1,
    "ack_sequence_number": 0,
    "media_stream_descriptor": 
    {
        "graph_identifier": 
        {
            "media_services_arm_id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/microsoft.media/mediaservices/mediaAccountName",
            "graph_instance_name": "mediaGraphName",
            "graph_node_name": "grpcExtension"
        },
        "media_descriptor": 
        {
            "timescale": 90000,
            "video_frame_sample_format": 
            {
                "encoding": "RAW",
                "pixel_format": "RGB24",
                "dimensions": 
                {
                    "width": 416,
                    "height": 416
                },
                "stride_bytes": 1248
            }
        }
    }
}
```

사용자 지정 확장은 이에 대한 응답으로 유추만 반환함을 나타내는 다음 메시지를 보냅니다.

```
{
    "sequence_number": 1,
    "ack_sequence_number": 1,
    "media_stream_descriptor": 
    {
        "extension_identifier": "customExtensionName"    
    }
}
```

이제 양쪽 모두에서 미디어 설명자를 교환했으므로 Live Video Analytics에서 프레임을 확장으로 전송하기 시작합니다.

> [!NOTE]
> gRPC 서버 쪽 구현은 선택한 프로그래밍 언어로 수행할 수 있습니다.
### <a name="sequence-numbers"></a>시퀀스 번호

gRPC 확장 노드와 사용자 지정 확장은 모두 메시지에 할당된 별도의 시퀀스 번호 세트를 유지 관리합니다. 이 시퀀스 번호는 1부터 시작하여 단조롭게 증가해야 합니다. 메시지를 승인하지 않는 경우 `ack_sequence_number`를 무시할 수 있습니다. 이는 첫 번째 메시지를 보낼 때 발생할 수 있습니다.

해당 메시지가 완전히 처리되면 요청을 승인해야 합니다. 공유 메모리 전송의 경우 이 승인은 발신기에서 공유 메모리를 해제할 수 있고 수신기에서 더 이상 이 메모리에 액세스할 수 없음을 나타냅니다. 발신기는 승인될 때까지 공유 메모리를 보유해야 합니다.

### <a name="reading-embedded-content"></a>포함된 콘텐츠 읽기

포함된 콘텐츠는 `content_byte` 필드를 통해 `MediaSample` 메시지에서 직접 읽을 수 있습니다. 데이터는 `MediaDescriptor`에 따라 인코딩됩니다.

### <a name="reading-content-from-shared-memory"></a>공유 메모리에서 콘텐츠 읽기

공유 메모리를 통해 콘텐츠를 전송하는 경우 발신기는 먼저 세션을 설정할 때 `SharedMemoryBufferTransferProperties`를 `MediaStreamDescriptor`에 포함합니다. 이는 다음과 같을 수 있습니다(JSON으로 표현됨).

```
{
  "handle_name": "inference_client_share_memory_2146989006636459346"
  "length_bytes": 20971520
}
```

그런 다음, 수신기는 `/dev/shm/inference_client_share_memory_2146989006636459346` 파일을 엽니다. 발신기는 이 파일의 특정 위치를 참조하는 `ContentReference`가 포함된 `MediaSample` 메시지를 보냅니다.

```
{
    "timestamp": 143598615750000,
    "content_reference": 
    {
        "address_offset": 519168,
        "length_bytes": 173056
    }
}
```

그런 다음, 수신기는 파일의 이 위치에서 데이터를 읽습니다.

Live Video Analytics 컨테이너에서 공유 메모리를 통해 통신하려면 컨테이너의 IPC 모드를 올바르게 구성해야 합니다. 이는 여러 가지 방법으로 수행할 수 있지만, 몇 가지 추천 구성은 다음과 같습니다.

* 호스트 디바이스에서 실행되는 gRPC 유추 엔진과 통신하는 경우 IPC 모드를 호스트로 설정해야 합니다.
* 다른 IoT Edge 모듈에서 실행되는 gRPC 서버와 통신하는 경우 IPC 모드는 Live Video Analytics 모듈에 대해 공유 가능으로 설정하고 사용자 지정 확장에 대해 `container:liveVideoAnalytics`로 설정해야 합니다. 여기서 `liveVideoAnalytics`는 Live Video Analytics 모듈의 이름입니다.

위의 첫 번째 옵션을 사용하는 디바이스 쌍에서 이는 다음과 같을 수 있습니다.

```
"liveVideoAnalytics": 
{
  "version": "1.0",
  "type": "docker",
  "status": "running",
  "restartPolicy": "always",
  "settings": 
  {
    "image": "mcr.microsoft.com/media/live-video-analytics:1",
    "createOptions": 
      "HostConfig": 
      {
        "IpcMode": "host"
      }
  }
}
```

IPC 모드에 대한 자세한 내용은 https://docs.docker.com/engine/reference/run/#ipc-settings---ipc 를 참조하세요.

## <a name="mediagraph-grpc-extension-contract-definitions"></a>MediaGraph gRPC 확장 계약 정의

이 섹션에서는 데이터 흐름을 정의하는 gRPC 계약을 정의합니다.

### <a name="protocol-messages"></a>프로토콜 메시지

![프로토콜 메시지](./media/grpc-extension-protocol/grpc2.png)
 
### <a name="client-authentication"></a>클라이언트 인증

사용자 지정 확장의 구현자는 들어오는 gRPC 연결의 신뢰성을 확인하여 gRPC 확장 노드에서 오는지 확인할 수 있습니다. 노드는 유효성을 검사할 요청 헤더에 항목을 제공합니다.

이는 사용자 이름/암호 자격 증명을 사용하여 수행할 수 있습니다. gRPC 확장 노드를 만들 때 자격 증명은 다음과 같이 제공됩니다.

```
{
  "@type": "#Microsoft.Media.MediaGraphGrpcExtension",
  "name": "{moduleIdentifier}",
  "endpoint": 
  {
    "@type": "#Microsoft.Media.MediaGraphUnsecuredEndpoint",
    "url": "tcp://customExtension:8081",
    "credentials": 
    {
      "@type": "#Microsoft.Media.MediaGraphUsernamePasswordCredentials",
      "username": "username",
      "password": "password"
    }
  }
  // Other fields omitted
}
```

gRPC 요청을 보내면 HTTP 기본 인증을 모방한 다음 헤더가 요청 메타데이터에 포함됩니다.

`x-ms-authentication: Basic (Base64 Encoded username:password)`


## <a name="configuring-inference-server-for-each-mediagraph-over-grpc-extension"></a>gRPC 확장을 통한 각 MediaGraph에 대한 유추 서버 구성
유추 서버를 구성하는 경우 유추 서버 내에 패키징된 모든 AI 모델에 대해 노드를 노출하지 않아도 됩니다. 대신, 그래프 인스턴스의 경우 `MediaGraphGrpcExtension` 노드의 `extensionConfiguration` 속성을 사용하고 AI 모델을 선택하는 방법을 정의할 수 있습니다. 실행 중에 LVA는 이 문자열을 유추 서버로 전달하여 원하는 AI 모델을 호출하는 데 사용할 수 있습니다. 이 `extensionConfiguration` 속성은 선택적 속성이며 서버마다 다릅니다. 속성은 다음과 같이 사용할 수 있습니다.
```
{
  "@type": "#Microsoft.Media.MediaGraphGrpcExtension",
  "name": "{moduleIdentifier}",
  "endpoint": 
  {
    "@type": "#Microsoft.Media.MediaGraphUnsecuredEndpoint",
    "url": "${grpcExtensionAddress}",
    "credentials": 
    {
      "@type": "#Microsoft.Media.MediaGraphUsernamePasswordCredentials",
      "username": "${grpcExtensionUserName}",
      "password": "${grpcExtensionPassword}"
    }
  },
    // Optional server configuration string. This is server specific 
  "extensionConfiguration": "{Optional extension specific string}",
  "dataTransfer": 
  {
    "mode": "sharedMemory",
    "SharedMemorySizeMiB": "5"
  }
    //Other fields omitted
}
```

## <a name="using-grpc-over-tls"></a>TLS를 통한 gRPC 사용

유추에 사용되는 gRPC 연결은 TLS를 통해 보호될 수 있습니다. 이는 Live Video Analytics와 유추 엔진 간의 네트워크 보안을 보장할 수 없는 경우에 유용합니다. TLS는 gRPC 메시지에 포함된 모든 콘텐츠를 암호화하므로 프레임을 높은 속도로 전송할 때 추가 CPU 오버헤드가 발생합니다.

IgnoreHostname 및 IgnoreSignature 확인 옵션은 gRPC에서 지원되지 않으므로 유추 엔진에서 제공하는 서버 인증서에는 gRPC 확장 노드의 엔드포인트 URL에 있는 IP 주소/호스트 이름과 정확히 일치하는 CN이 포함되어야 합니다.

## <a name="next-steps"></a>다음 단계

[유추 메타데이터 스키마에 대해 알아보기](inference-metadata-schema.md)
