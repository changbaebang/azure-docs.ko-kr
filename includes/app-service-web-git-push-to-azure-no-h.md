---
title: 파일 포함
description: 포함 파일
services: app-service
author: cephalin
ms.service: app-service
ms.topic: include
ms.date: 02/02/2018
ms.author: cephalin
ms.custom: include file
ms.openlocfilehash: 08f4e76869f124d946566f64da394c895d0af308
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102206008"
---
로컬 터미널 창으로 돌아와서 로컬 Git 리포지토리에 Azure 원격을 추가합니다. *\<deploymentLocalGitUrl-from-create-step>* 를 [웹앱 만들기](#create-a-web-app)에 저장된 Git 원격의 URL로 바꿉니다.

```bash
git remote add azure <deploymentLocalGitUrl-from-create-step>
```

다음 명령을 사용하여 Azure 원격에 푸시하여 앱을 배포합니다. Git Credential Manager에서 자격 증명을 묻는 메시지가 표시되면 Azure Portal에 로그인하는 데 사용하는 자격 증명이 아니라 **배포 사용자 구성** 에서 만든 자격 증명을 입력해야 합니다.

```bash
git push azure main
```

이 명령을 실행하는 데 몇 분 정도 걸릴 수 있습니다. 실행 시 다음 예와 유사한 정보를 출력합니다.
