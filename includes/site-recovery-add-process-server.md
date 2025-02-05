---
author: rayne-wiselman
ms.service: site-recovery
ms.topic: include
ms.date: 10/26/2018
ms.author: raynew
ms.openlocfilehash: 31e61069c95be9bd1c7a684bb83ebcd93bcb14be
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "96019148"
---
1. Azure Site Recovery UnifiedSetup.exe 시작
2. **시작하기 전에** 에서 **배포 규모 확장을 위해 추가 프로세스 서버 추가** 를 선택합니다.

   ![프로세스 서버 추가](./media/site-recovery-add-process-server/ps-page-1.png)

3. **구성 서버 세부 정보** 에서 구성 서버의 IP 주소 및 암호를 지정합니다.

   ![프로세스 서버 2 추가](./media/site-recovery-add-process-server/ps-page-2.png)
4. **인터넷 설정** 에서 구성 서버에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다.

   ![프로세스 서버 3 추가](./media/site-recovery-add-process-server/ps-page-3.png)

   * 현재 컴퓨터에 설정된 프록시를 사용하여 연결하려면 **기존 프록시 설정을 사용하여 연결** 을 선택합니다.
   * 공급자가 직접 연결되도록 하려면 **프록시 없이 직접 연결** 을 선택합니다.
   * 기존 프록시에 인증이 필요하거나 공급자 연결에 대해 사용자 지정 프록시를 사용하려면 **사용자 지정 프록시 설정을 사용하여 연결** 을 선택합니다.

     * 사용자 지정 프록시를 사용하는 경우 주소, 포트 및 자격 증명을 지정해야 합니다.
     * 프록시를 사용하는 경우 이미 서비스 URL에 대한 액세스를 허용했어야 합니다.

5. **필수 조건 확인** 에서 설치 프로그램은 설치가 실행될 수 있는지 확인합니다. **글로벌 시간 동기화 확인** 에 대한 경고가 표시되면 시스템 시계의 시간(**날짜 및 시간** 설정)이 표준 시간대와 같은지 확인합니다.

     ![프로세스 서버 4 추가](./media/site-recovery-add-process-server/ps-page-4.png)

6. **환경 세부 정보** 에서 VMware VM을 복제 여부를 선택합니다. 복제할 경우 설치 프로그램에서 PowerCLI 6.0이 설치되어 있는지 확인합니다.

     ![프로세스 서버 5 추가](./media/site-recovery-add-process-server/ps-page-5.png)

7. **설치 위치** 에서 이진 파일을 설치하고 캐시를 저장할 위치를 선택합니다. 최소 5GB의 디스크 공간이 있는 드라이브를 선택해야 하지만 600GB 이상의 사용 가능한 공간이 있는 캐시 드라이브를 선택하는 것이 좋습니다.
     ![이진 파일 및 캐시 스토리지의 설치 위치를 보여 주는 스크린샷](./media/site-recovery-add-process-server/ps-page-6.png)

8. **네트워크 선택** 에서 구성 서버가 복제 데이터를 전송 및 수신할 수신기(네트워크 어댑터 및 SSL 포트)를 지정합니다. 9443 포트는 복제 트래픽을 보내고 받는 데 사용되는 기본 포트이지만, 환경의 요구 사항에 맞게 이 포트 번호를 수정할 수 있습니다. 9443 포트 외에도 웹 서버에서 복제 작업을 조정하기 위해 사용하는 443 포트를 엽니다. 복제 트래픽을 보내거나 받는 데 443 포트를 사용하면 안 됩니다.

     ![프로세스 서버 6 추가](./media/site-recovery-add-process-server/ps-page-7.png)
9. **요약** 에서 정보를 검토하고 **설치** 를 클릭합니다. 설치가 완료되면 암호가 생성됩니다. 복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.

     ![프로세스 서버 7 추가](./media/site-recovery-add-process-server/ps-page-8.png)
