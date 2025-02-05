---
title: Azure 파일 동기화 클라우드 계층화 정책 | Microsoft Docs
description: 다양 한 시나리오에서 날짜 및 볼륨의 사용 가능한 공간 정책이 함께 작동 하는 방법에 대 한 세부 정보입니다.
author: roygara
ms.service: storage
ms.topic: conceptual
ms.date: 1/4/2021
ms.author: rogarana
ms.subservice: files
ms.openlocfilehash: 3020737e91e1fe5c4af3e23a147fa0ea16037d3b
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "102204432"
---
# <a name="cloud-tiering-policies"></a>클라우드 계층화 정책

클라우드 계층화에는 클라우드로 계층화 되는 파일을 결정 하는 두 가지 정책, 즉 **사용 가능한 볼륨 공간 정책과** **날짜 정책이** 있습니다.

**사용 가능한 볼륨 공간 정책은** 서버 끝점이 있는 로컬 볼륨의 지정 된 백분율이 항상 사용 가능한 상태로 유지 되도록 합니다. 

마지막으로 x 일 전에 마지막으로 액세스 한 **날짜 정책** 계층 파일입니다. 사용 가능한 볼륨 공간 정책은 항상 우선 적용 됩니다. 볼륨에 사용 가능한 공간이 부족 하 여 날짜 정책에 설명 된 대로 파일 수를 저장할 수 없는 경우, Azure 파일 동기화는 날짜 정책을 재정의 하 고 사용 가능한 볼륨 공간 백분율이 충족 될 때까지 coldest 파일의 계층화를 계속 합니다.

## <a name="how-both-policies-work-together"></a>두 정책 모두 함께 작동 하는 방법

예를 사용 하 여 이러한 정책의 작동 방식을 보여 줍니다. 500 GB 로컬 볼륨에 Azure 파일 동기화를 구성 했으며 클라우드 계층화를 사용 하도록 설정 하지 않은 경우를 가정해 보겠습니다. 파일 공유의 파일은 다음과 같습니다.

|파일 이름 |마지막 액세스 시간  |파일 크기  |저장 된 |
|----------|------------------|-----------|----------|
|파일 1    | 2일 전  | 10GB | 서버 및 Azure 파일 공유
|파일 2    | 10일 전 | 30GB | 서버 및 Azure 파일 공유
|파일 3    | 1 년 전 | 200GB | 서버 및 Azure 파일 공유
|파일 4    | 1 년, 2 일 전 | 130 GB | 서버 및 Azure 파일 공유
|파일 5    | 2 년, 1 일 전 | 140GB | 서버 및 Azure 파일 공유

**변경 1:** 클라우드 계층화를 사용 하도록 설정 하 고, 사용 가능한 볼륨 공간 정책을 20%로 설정 하 고, 날짜 정책을 사용 하지 않도록 설정 했습니다. 이 구성을 사용 하 여 클라우드 계층화는 20% (이 경우 100 GB)의 공간을 확보 하 고 로컬 컴퓨터에서 사용할 수 있도록 합니다. 따라서 로컬 캐시의 총 용량은 400 GB입니다. 이 400 GB는 가장 최근에 액세스 한 파일을 로컬 볼륨에 저장 합니다.

이 구성을 사용 하면 1 ~ 4 파일만 로컬 캐시에 저장 되 고 파일 5는 계층화 됩니다. 이는 사용할 수 있는 400 GB 중 370입니다. 파일 5는 140이 고, 로컬로 캐시 된 경우 400 GB 제한을 초과 합니다. 

**변경 2:** 사용자가 파일 5에 액세스 한다고 가정 합니다. 그러면 파일 5가 공유에서 가장 최근에 액세스 한 파일을 사용 합니다. 따라서 파일 5는 로컬 캐시에 저장 되 고 400-GB 제한에 맞게 파일 4가 계층화 됩니다. 다음 표에서는 이러한 업데이트를 사용 하 여 파일이 저장 되는 위치를 보여 줍니다.

|파일 이름 |마지막 액세스 시간  |파일 크기  |저장 된 |
|----------|------------------|-----------|----------|
|파일 5    | 2시간 전 | 140GB | 서버 및 Azure 파일 공유
|파일 1    | 2일 전  | 10GB | 서버 및 Azure 파일 공유
|파일 2    | 10일 전 | 30GB | 서버 및 Azure 파일 공유
|파일 3    | 1 년 전 | 200GB | 서버 및 Azure 파일 공유
|파일 4    | 1 년, 2 일 전 | 130 GB | 로컬로 계층화 된 Azure 파일 공유

**변경 3:** 날짜 기반 계층화 정책을 60 일로 지정 하 고 사용 가능한 볼륨 공간 정책이 70% 되도록 정책을 업데이트 했다고 가정해 보겠습니다. 이제 최대 150 GB만 로컬 캐시에 저장할 수 있습니다. 파일 2에 액세스 하는 데 60 일이 지난 후에는 사용 가능한 볼륨 공간 정책이 날짜 정책을 재정의 하 고 파일 2가 계층화 되어 70%의 사용 가능한 로컬 공간을 유지 합니다.

**변경 4:** 사용 가능한 볼륨 공간 정책을 20%로 변경한 다음 `Invoke-StorageSyncFileRecall` 클라우드 계층화 정책을 준수 하면서 로컬 드라이브에 맞는 모든 파일을 회수 하는 데 사용 되는 경우 테이블은 다음과 같습니다.

|파일 이름 |마지막 액세스 시간  |파일 크기  |저장 된 |
|----------|------------------|-----------|----------|
|파일 5    | 1 시간 전  | 140GB | 서버 및 Azure 파일 공유
|파일 1    | 2일 전  | 10GB | 서버 및 Azure 파일 공유
|파일 2    | 10일 전 | 30GB | 서버 및 Azure 파일 공유
|파일 3    | 1 년 전 | 200GB | 로컬로 계층화 된 Azure 파일 공유
|파일 4    | 1 년, 2 일 전 | 130 GB | 로컬로 계층화 된 Azure 파일 공유

이 경우 파일 1, 2 및 5는 로컬로 캐시 되 고 파일 3과 4는 계층화 됩니다. 날짜 정책이 60 일 이기 때문에 파일 3 및 4는 볼륨의 사용 가능한 공간 정책이 로컬에서 최대 400 GB를 허용 하더라도 계층화 됩니다.

> [!NOTE] 
> 고객이 볼륨 사용 가능 공간 정책을 더 작은 값 (예: 20% ~ 10%)으로 변경 하면 파일이 자동으로 회수 되지 않습니다. 또는 날짜 정책을 더 큰 값으로 변경 합니다 (예: 20 일에서 50 일로).

## <a name="multiple-server-endpoints-on-a-local-volume"></a>로컬 볼륨의 여러 서버 끝점

단일 로컬 볼륨의 여러 서버 끝점에 대해 클라우드 계층화를 사용 하도록 설정할 수 있습니다. 이 구성에서는 동일한 볼륨의 모든 서버 끝점에 대해 사용 가능한 볼륨 공간을 동일한 양만큼 설정 해야 합니다. 동일한 볼륨의 여러 서버 끝점에 대해 사용 가능한 볼륨 공간 정책을 여러 개 설정 하면 사용 가능한 최대 볼륨 공간 백분율이 우선적으로 적용 됩니다. 이를 **유효 볼륨 사용 가능 공간 정책** 이라고 합니다. 예를 들어 세 개의 서버 끝점이 동일한 로컬 볼륨에 있고, 하나는 15%로 설정 되 고, 세 번째는 30%로 설정 된 경우 사용 가능한 공간이 30% 미만이 면 모두 coldest 파일의 계층을 시작 합니다.

## <a name="next-steps"></a>다음 단계
* [클라우드 계층화 모니터링](storage-sync-monitor-cloud-tiering.md)
