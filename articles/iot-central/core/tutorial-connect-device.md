---
title: 자습서 - Azure IoT Central에 제네릭 클라이언트 앱 연결 | Microsoft Docs
description: 이 자습서에서는 디바이스 개발자가 C, C#, Java, JavaScript 또는 Python 클라이언트 앱을 실행하는 디바이스를 Azure IoT Central 애플리케이션에 연결하는 방법을 보여줍니다. 운영자가 연결된 디바이스와 상호 작용할 수 있도록 하는 보기를 추가하여 자동으로 생성된 디바이스 템플릿을 수정합니다.
author: dominicbetts
ms.author: dobett
ms.date: 11/24/2020
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom:
- mqtt
- device-developer
zone_pivot_groups: programming-languages-set-twenty-six
ms.openlocfilehash: 8f1b5eabe235d107b48dc7b2db5b6d4b1188a3fa
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99833969"
---
# <a name="tutorial-create-and-connect-a-client-application-to-your-azure-iot-central-application"></a>자습서: 클라이언트 애플리케이션을 만들어 Azure IoT Central 애플리케이션에 연결

*이 문서는 솔루션 빌더 및 디바이스 개발자에게 적용됩니다.*

이 자습서에서는 디바이스 개발자가 클라이언트 애플리케이션을 Azure IoT Central 애플리케이션에 연결하는 방법을 보여줍니다. 이 애플리케이션은 자동 온도 조절 디바이스의 동작을 시뮬레이션합니다. 애플리케이션이 IoT Central에 연결되면 자동 온도 조절 디바이스 모델의 모델 ID를 보냅니다. IoT Central은 모델 ID를 사용하여 디바이스 모델을 검색하고 디바이스 템플릿을 만듭니다. 운영자가 디바이스와 상호 작용할 수 있도록 디바이스 템플릿에 사용자 지정 및 보기를 추가합니다.

이 자습서에서는 다음과 같은 작업을 수행하는 방법을 살펴봅니다.

> [!div class="checklist"]
> * 디바이스 코드를 만들고 실행하며, IoT Central 애플리케이션에 연결되는지 확인합니다.
> * 디바이스에서 보낸 시뮬레이션된 원격 분석 데이터 보기
> * 디바이스 템플릿에 사용자 지정 보기를 추가합니다.
> * 디바이스 템플릿을 게시합니다.
> * 보기를 사용하여 디바이스 속성을 관리합니다.
> * 명령을 호출하여 디바이스를 제어합니다.

:::zone pivot="programming-language-ansi-c"

[!INCLUDE [iot-central-connect-device-c](../../../includes/iot-central-connect-device-c.md)]

:::zone-end

:::zone pivot="programming-language-csharp"

[!INCLUDE [iot-central-connect-device-csharp](../../../includes/iot-central-connect-device-csharp.md)]

:::zone-end

:::zone pivot="programming-language-java"

[!INCLUDE [iot-central-connect-device-java](../../../includes/iot-central-connect-device-java.md)]

:::zone-end

:::zone pivot="programming-language-javascript"

[!INCLUDE [iot-central-connect-device-nodejs](../../../includes/iot-central-connect-device-nodejs.md)]

:::zone-end

:::zone pivot="programming-language-python"

[!INCLUDE [iot-central-connect-device-python](../../../includes/iot-central-connect-device-python.md)]

:::zone-end

## <a name="view-raw-data"></a>원시 데이터 보기

디바이스 개발자는 **원시 데이터** 보기를 사용하여 장치에서 IoT Central로 전송하는 원시 데이터를 검사할 수 있습니다.

:::image type="content" source="media/tutorial-connect-device/raw-data.png" alt-text="원시 데이터 보기":::

이 보기에서 표시할 열을 선택하고 표시할 시간 범위를 설정할 수 있습니다. **모델링되지 않은 데이터** 열에는 디바이스 템플릿의 속성 또는 원격 분석 정의와 일치하지 않는 디바이스 데이터가 표시됩니다.

## <a name="clean-up-resources"></a>리소스 정리

[!INCLUDE [iot-central-clean-up-resources](../../../includes/iot-central-clean-up-resources.md)]

## <a name="next-steps"></a>다음 단계

IoT Central 자습서 세트를 계속 진행하고 IoT Central 솔루션 빌드에 대해 자세히 알아보려면 다음을 참조하세요.

> [!div class="nextstepaction"]
> [게이트웨이 디바이스 템플릿 만들기](./tutorial-define-gateway-device-type.md)

디바이스 개발자로서, Java를 사용하여 디바이스를 만드는 방법의 기본 사항을 배웠으므로 이제 다음 단계를 수행하는 것이 좋습니다.

* 디바이스 코드를 구현할 때 디바이스 템플릿의 역할을 자세히 알아보려면 [디바이스 템플릿이란?](./concepts-device-templates.md)을 참조하세요.
* IoT Central에 디바이스를 등록하는 방법과 IoT Central에서 디바이스 연결을 보호하는 방법에 대한 자세한 내용은 [Azure IoT Central에 연결](./concepts-get-connected.md)을 참조하세요.
* 디바이스에서 IoT Central과 교환하는 데이터에 대한 자세한 내용은 [원격 분석, 속성 및 명령 페이로드](concepts-telemetry-properties-commands.md)를 참조하세요.
* [IoT 플러그 앤 플레이 디바이스 개발자 가이드](../../iot-pnp/concepts-developer-guide-device.md)를 읽습니다.
