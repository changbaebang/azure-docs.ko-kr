---
title: '빠른 시작: 시작'
description: 이 빠른 시작에서는 Defender for IoT 배포의 기본 워크플로를 시작하는 방법에 대해 알아봅니다.
ms.topic: quickstart
ms.date: 2/18/2021
ms.openlocfilehash: c6136d734570714b691a4ba3c2a72305c4c85590
ms.sourcegitcommit: f611b3f57027a21f7b229edf8a5b4f4c75f76331
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104784495"
---
# <a name="quickstart-get-started-with-defender-for-iot"></a>빠른 시작: Defender for IoT 시작

이 문서에서는 Azure Defender for IoT를 설정하는 단계의 개요를 제공합니다. 이 프로세스를 진행하려면 다음을 수행해야 합니다.

- Azure Defender for IoT 포털에서 구독과 센서를 등록합니다.
- 센서 및 온-프레미스 관리 콘솔 소프트웨어를 설치합니다.
- 센서 및 관리 콘솔의 초기 활성화를 수행합니다.

## <a name="prerequisites"></a>사전 요구 사항

없음

## <a name="permission-requirements"></a>사용 권한 요구 사항

일부 설정 단계는 특정 사용자 권한이 필요합니다.

관리 사용자 권한은 센서 및 관리 콘솔을 활성화하고, SSL/TLS 인증서를 업로드하고, 새 암호를 생성하는 데 필요합니다.

다음 표에는 Azure Defender for IoT 포털 도구에 대한 사용자 액세스 권한이 설명되어 있습니다.

| 사용 권한 | 보안 판독기 | 보안 관리자 | 구독 기여자 | 구독 소유자 |
|--|--|--|--|--|
| 모든 Defender for IoT 화면 및 데이터 보기 | ✓ | ✓ | ✓ | ✓ |
| 센서 온보딩  |  |  ✓ | ✓ | ✓ |
| 가격 책정 업데이트  |  |  ✓ | ✓ | ✓ |
| 암호 복구  | ✓  |  ✓ | ✓ | ✓ |

## <a name="identify-the-solution-infrastructure"></a>솔루션 인프라 식별

**네트워크 설정 요구 사항 확인**

네트워크 아키텍처, 모니터링되는 대역폭 및 기타 네트워크 세부 정보를 조사합니다. 자세한 내용은 [Azure Defender for IoT 네트워크 설정 정보](how-to-set-up-your-network.md)를 참조하세요.

**네트워크 부하를 처리하는 데 필요한 센서 및 관리 콘솔 어플라이언스 확인**

Azure Defender for IoT는 물리적 배포와 가상 배포를 모두 지원합니다. 물리적 배포의 경우 다양한 인증 어플라이언스를 구입할 수 있습니다. 자세한 내용은 [필수 어플라이언스 식별](how-to-identify-required-appliances.md)을 참조하세요.

모니터링할 대략적인 디바이스 수를 계산하는 것이 좋습니다. 나중에 Azure 구독을 포털에 등록할 때 이 숫자를 입력하라는 메시지가 표시됩니다. 1,000초 간격으로 숫자를 늘릴 수 있습니다. 모니터링되는 디바이스 수를 *커밋된 디바이스* 라고 합니다.

## <a name="register-with-azure-defender-for-iot"></a>Azure Defender for IoT에 등록

등록에는 다음이 포함됩니다.

- Azure 구독을 Defender for IoT에 온보딩합니다.
- 커밋된 디바이스를 정의합니다.
- 온-프레미스 관리 콘솔의 활성화 파일을 다운로드합니다.

등록하려면 다음을 수행합니다.

1. Azure Defender for IoT 포털로 이동합니다.
1. **구독 등록** 을 선택합니다.
1. **가격 책정** 페이지에서 구독을 선택하거나 새 구독을 만들고 커밋된 디바이스 수를 추가합니다.
1. **온-프레미스 관리 콘솔 다운로드** 탭을 선택하고 다운로드한 활성화 파일을 저장합니다. 이 파일에는 사용자가 정의한 집계된 커밋된 디바이스가 포함되어 있습니다. 이 파일은 첫 로그인 후 관리 콘솔에 업로드됩니다.

구독을 등록 취소하는 방법은 [구독 등록 취소](how-to-manage-sensors-on-the-cloud.md#offboard-a-subscription)를 참조하세요.

## <a name="install-and-set-up-the-on-premises-management-console"></a>온-프레미스 관리 콘솔 설치 및 설정

온-프레미스 관리 콘솔 어플라이언스를 얻은 후에는 다음을 수행합니다.

- Azure Defender for IoT 포털에서 ISO 패키지를 다운로드합니다.
- 소프트웨어를 설치합니다.
- 초기 관리 콘솔 설치를 활성화하고 수행합니다.

콘솔을 설치하고 설정하려면 다음을 수행합니다.

1. Defender for IoT 포털에서 **시작** 을 선택합니다.
1. **온-프레미스 관리 콘솔** 탭을 선택합니다.
1. 버전을 선택하고 **다운로드** 를 선택합니다.
1. 온-프레미스 관리 콘솔 소프트웨어를 설치합니다. 자세한 내용은 [Defender for IoT 설치](how-to-install-software.md)를 참조하세요.
1. 관리 콘솔을 활성화하고 설정합니다. 자세한 내용은 [온-프레미스 관리 콘솔 활성화 및 설정](how-to-activate-and-set-up-your-on-premises-management-console.md)을 참조하세요.

## <a name="onboard-a-sensor"></a>센서 온보딩

센서를 Azure Defender for IoT에 등록하고 센서 활성화 파일을 다운로드하여 온보딩합니다.

1. 센서 이름을 정의하고 구독과 연결합니다.
1. 센서 관리 모드를 선택합니다.

   - **클라우드 연결 센서**: 센서에서 탐지한 정보가 센서 콘솔에 표시됩니다. 뿐만 아니라 경고 정보는 IoT 허브를 통해 전달되며 다른 Azure 서비스(예: Azure Sentinel)와 공유할 수 있습니다.

   - **로컬 관리형 센서**: 센서에서 탐지한 정보가 센서 콘솔에 표시됩니다. 에어-갭 네트워크에서 작업 중이고 여러 로컬 관리형 센서가 탐지한 모든 정보를 통합 보기에서 확인하려는 경우에는 온-프레미스 관리 콘솔을 사용합니다. 

1. 센서 활성화 파일을 다운로드합니다.

자세한 내용은 [Defender for IoT 포털에서 센서 온보딩 및 관리](how-to-manage-sensors-on-the-cloud.md)를 참조하세요.

## <a name="install-and-set-up-the-sensor"></a>센서 설치 및 설정

Azure Defender for IoT 포털에서 ISO 패키지를 다운로드하고, 소프트웨어를 설치하고, 센서를 설정합니다.

1. Defender for IoT 포털에서 **시작** 을 선택합니다.
1. **센서 설정** 을 선택합니다.
1. 버전을 선택하고 **다운로드** 를 선택합니다.
1. 센서 소프트웨어를 설치합니다. 자세한 내용은 [Defender for IoT 설치](how-to-install-software.md)를 참조하세요.
1. 센서를 활성화하고 설정합니다. 자세한 내용은 [로그인하고 센서 활성화](how-to-activate-and-set-up-your-sensor.md)를 참조하세요.

## <a name="connect-sensors-to-an-on-premises-management-console"></a>온-프레미스 관리 콘솔에 센서 연결

관리 콘솔에 센서를 연결하여 다음을 확인합니다.

- 센서가 온-프레미스 관리 콘솔에 경고 및 디바이스 인벤토리 정보를 보냅니다.

- 온-프레미스 관리 콘솔에서 센서 백업을 수행하고, 센서에서 탐지하는 경고를 관리하고, 센서 연결 끊김을 조사하고, 연결된 센서에서 기타 작업을 수행할 수 있습니다.

동일한 네트워크를 모니터링하는 여러 센서를 한 영역에 그룹화하는 것이 좋습니다. 이렇게 하면 여러 센서에서 수집된 정보가 병합됩니다.

자세한 내용은 [온-프레미스 관리 콘솔에 센서 연결](how-to-activate-and-set-up-your-on-premises-management-console.md#connect-sensors-to-the-on-premises-management-console)을 참조하세요.

## <a name="populate-azure-sentinel-with-alert-information-optional"></a>Azure Sentinel에 경고 정보 채우기(선택 사항)

Azure Sentinel을 구성하여 경고 정보를 Azure Sentinel에 보냅니다. [Defender for IoT의 데이터를 Azure Sentinel에 연결](how-to-configure-with-sentinel.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [Azure Defender for IoT 시작](overview.md)
> [Azure Defender for IoT 아키텍처](architecture.md)
