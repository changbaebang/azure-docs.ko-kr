---
title: Azure IoT Central로 빌드된 용수 사용량 모니터링 솔루션을 위한 참조 아키텍처| Microsoft Docs
description: Azure IoT Central로 빌드된 용수 사용량 모니터링 솔루션의 개념에 대해 알아보세요.
author: miriambrus
ms.author: miriamb
ms.date: 12/11/2020
ms.topic: conceptual
ms.service: iot-central
services: iot-central
ms.openlocfilehash: da1eafee719919d7f3086a059d8d2c70ef8d8cb1
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99831657"
---
# <a name="water-consumption-monitoring-reference-architecture"></a>용수 사용량 모니터링 참조 아키텍처 

용수 사용량 모니터링 솔루션은 **Azure IoT Central 앱 템플릿** 을 사용하여 킥 스타터 IoT 애플리케이션으로 빌드할 수 있습니다. 이 문서는 엔드투엔드 솔루션 빌드에 관한 높은 수준의 참조 아키텍처를 제공합니다. 

![용수 사용량 모니터링 아키텍처](./media/concepts-waterconsumptionmonitoring-architecture/concepts-waterconsumptionmonitoring-architecture1.png)

개념:

1. 디바이스 및 연결  
1. IoT Central 
1. 확장성 및 통합
1. 비즈니스 애플리케이션

용수 사용량 모니터링 솔루션과 관련된 주요 구성 요소를 살펴보겠습니다.

## <a name="devices-and-connectivity"></a>디바이스 및 연결 
이 섹션에서는 수질 모니터링 또는 용수 사용량 모니터링과 같이 스마트 워터 솔루션에 디바이스를 스마트 워터 디바이스라고 통칭합니다. 스마트 워터 디바이스에는 유량계, 용수 품질 모니터, 스마트 밸브, 누출 감지기 등이 포함될 수 있습니다.

스마트 워터 솔루션에 사용되는 디바이스는 일반적으로 타사 네트워크 사업자를 통한 LPWAN(저전력 광대역 네트워크)을 통해 연결됩니다. 이러한 유형의 디바이스의 경우 [Azure IoT Central Device Bridge](../core/howto-build-iotc-device-bridge.md)를 사용하여 디바이스 데이터를 Azure IoT Central의 IoT 애플리케이션으로 전송할 수 있습니다. 또는 IP 기능이 포함된 디바이스 게이트웨이를 보유한 경우 Azure IoT Central에 직접 연결할 수 있습니다.

## <a name="iot-central"></a>IoT Central 
Azure IoT Central은 IoT 솔루션을 빠르게 시작하거나 실행하도록 도와주는 IoT 앱 플랫폼입니다. 솔루션을 브랜딩 및 사용자 지정하거나 타사 서비스와 통합할 수 있습니다.
스마트 워터 디바이스를 IoT Central에 연결하면 디바이스 명령 및 제어, 모니터링 및 경고, RBAC가 내장된 사용자 인터페이스, 구성 가능한 인사이트 대시보드, 확장성 옵션을 이용할 수 있습니다. 


## <a name="extensibility-and-integrations"></a>확장성 및 통합
Azure IoT Central에서 IoT 애플리케이션을 확장하고 필요에 따라 다음을 수행할 수 있습니다.
* 고급 분석을 위해 IoT 데이터를 변환하고 통합(예: IoT Central 애플리케이션에서 데이터를 지속적으로 내보내 Machine Learning 모델을 교육)
* Azure IoT Central 애플리케이션의 웹후크 또는 Power Automate를 통해 작업을 트리거하여 다른 시스템의 워크플로 자동화
* IoT Central API를 통해 IoT Central의 IoT 애플리케이션에 프로그래밍 방식으로 액세스

## <a name="business-applications"></a>비즈니스 애플리케이션 
IoT 데이터는 상수도 시설 내 다양한 종류의 비즈니스 애플리케이션을 지원하는 데 사용될 수 있습니다. IoT Central 용수 사용량 모니터링 애플리케이션을 필드 서비스와 연결하는 방법은 [Dynamics 365 Field Services와 통합하는 방법](./how-to-configure-connected-field-services.md) 자습서를 참조하세요. 


## <a name="next-steps"></a>다음 단계
* [용수 사용량](./tutorial-water-consumption-monitoring.md) IoT Central 애플리케이션을 만드는 방법에 대해 자세히 알아보기
* [Azure IoT Central 정부 템플릿](./overview-iot-central-government.md)에 대해 자세히 알아보기
* [Azure IoT Central 개요](../core/overview-iot-central.md)를 참조하여 Azure IoT Central에 대해 자세히 알아보기
