---
author: craigktreasure
ms.service: azure-object-anchors
ms.topic: include
ms.date: 02/18/2021
ms.author: crtreasu
ms.openlocfilehash: 4345810292896cf88de19baf419eee025ba5853f
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102044792"
---
다음은 Unity용 Azure Object Anchors 패키지를 다운로드하는 단계입니다.

# <a name="download-with-web-browser"></a>[웹 브라우저를 사용하여 다운로드](#tab/unity-package-web-ui)

[여기](https://aka.ms/aoa/unity-sdk/package)에서 Unity용 Azure Object Anchors 패키지를 찾습니다. 원하는 버전을 선택하고 **다운로드** 단추를 사용하여 패키지를 다운로드합니다.

# <a name="download-with-npm"></a>[NPM을 사용하여 다운로드](#tab/unity-package-npm)

이 단계를 수행하려면 <a href="https://www.npmjs.com/get-npm" target="_blank">NPM</a>이 설치되어 있고 사용이 가능해야 합니다.

다음 명령을 실행하여 `<version_number>`를 다운로드할 Azure Object Anchors 버전으로 바꿉니다.

```bash
npm pack com.microsoft.azure.object-anchors.runtime@<version_number> --registry https://pkgs.dev.azure.com/aipmr/MixedReality-Unity-Packages/_packaging/Unity-packages/npm/registry/
```

> [!NOTE]
> 사용 가능한 Azure Object Anchors 패키지 버전을 나열하려면 다음을 실행합니다.
>
> ```bash
> npm view com.microsoft.azure.object-anchors.runtime --registry https://pkgs.dev.azure.com/aipmr/MixedReality-Unity-Packages/_packaging/Unity-packages/npm/registry/ versions
> ```

Azure Object Anchors 패키지는 명령을 실행한 폴더에 다운로드됩니다.

# <a name="install-with-mixed-reality-feature-tool-beta"></a>[Mixed Reality 기능 도구(베타)를 사용하여 설치](#tab/unity-package-mixed-reality-feature-tool)

다음 단계를 계속 진행합니다. 이후 단계에서 <a a href="https://aka.ms/MRFeatureToolDocs" target="_blank">Mixed Reality 기능 도구</a>를 사용합니다.

---
