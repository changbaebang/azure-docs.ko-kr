---
ms.openlocfilehash: dfb887004cd29b5bd9f1d9886b7dfa5f43c83dbe
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99531836"
---
MP4 파일은 VIDEO_OUTPUT_FOLDER_ON_DEVICE 키를 사용하여 *.env* 파일에서 구성한 에지 디바이스의 디렉터리에 기록됩니다. 기본값을 사용한 경우 결과는 */var/media/* 폴더에 있어야 합니다.

MP4 클립을 재생하는 방법은 다음과 같습니다.

1. 리소스 그룹으로 이동하고, VM을 찾고, Azure Bastion을 사용하여 연결합니다.

    ![Resource group](../../../media/quickstarts/resource-group.png)
    
    ![VM](../../../media/quickstarts/virtual-machine.png)
1. [Azure 리소스 설정](../../../detect-motion-emit-events-quickstart.md#set-up-azure-resources) 과정에서 생성된 자격 증명을 사용하여 로그인합니다. 
1. 명령 프롬프트에서 관련 디렉터리로 이동합니다. 기본 위치는 */var/media* 입니다. 이 디렉터리에 MP4 파일이 있습니다.

    ![출력](../../../media/quickstarts/samples-output.png) 

1. [SCP(Secure Copy)](../../../../../virtual-machines/linux/copy-files-to-linux-vm-using-scp.md)를 사용하여 로컬 머신에 파일을 복사합니다. 
1. [VLC 미디어 플레이어](https://www.videolan.org/vlc/) 또는 기타 MP4 플레이어를 사용하여 파일을 재생합니다.
