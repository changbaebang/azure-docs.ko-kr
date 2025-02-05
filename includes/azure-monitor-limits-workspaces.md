---
title: 파일 포함
description: 포함 파일
services: azure-monitor
author: rboucher
tags: azure-service-management
ms.topic: include
ms.date: 02/07/2019
ms.author: robb
ms.custom: include file
ms.openlocfilehash: ee7ccb126eb04e168ccc213f0429d41a76a8bc2f
ms.sourcegitcommit: 772eb9c6684dd4864e0ba507945a83e48b8c16f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2021
ms.locfileid: "103021679"
---
**데이터 컬렉션 볼륨 및 보존** 

| 계층 | 일일 제한 | 데이터 보존 | 의견 |
|:---|:---|:---|:---|
| 현재 GB당 가격 책정 계층<br>(2018년 4월에 도입) | 제한 없음 | 30~730일 | 데이터를 31일 넘게 보존하려면 추가 요금을 내야 합니다. Azure Monitor 가격에 대해 자세히 알아봅니다. |
| 레거시 무료 계층<br>(2016년 4월에 도입) | 500MB | 7 일 | 작업 영역이 일일 500MB 제한에 도달하면 데이터 수집이 중지되고 다음 날부터 다시 시작됩니다. 1일은 UTC를 기준으로 합니다. Azure Security Center에서 수집하는 데이터는 이 500MB 일일 제한에 합산되지 않으며 이 제한을 초과해도 계속 수집됩니다.  |
| 레거시 독립 실행형 GB당 계층<br>(2016년 4월에 도입) | 제한 없음 | 30~730일 | 데이터를 31일 넘게 보존하려면 추가 요금을 내야 합니다. Azure Monitor 가격에 대해 자세히 알아봅니다. |
| 레거시 노드당(OMS)<br>(2016년 4월에 도입) | 제한 없음 | 30~730일 | 데이터를 31일 넘게 보존하려면 추가 요금을 내야 합니다. Azure Monitor 가격에 대해 자세히 알아봅니다. |
| 레거시 표준 계층 | 제한 없음 | 30일  | 보존 기간을 조정할 수 없음 |
| 레거시 프리미엄 계층 | 제한 없음 | 365일  | 보존 기간을 조정할 수 없음 |

**구독당 작업 영역의 수**

| 가격 책정 계층    | 작업 영역 제한 | 주석
|:---|:---|:---|
| 무료 계층  | 10 | 이 제한은 늘릴 수 없습니다. |
| 다른 모든 계층 | 제한 없음 | 리소스 그룹 내 리소스의 수와 구독당 리소스 그룹의 수가 제한됩니다. |

**Azure Portal**

| 범주 | 제한 | 주석 |
|:---|:---|:---|
| 로그 쿼리에서 반환하는 최대 레코드 수 | 10000 | 쿼리에 쿼리 범위, 시간 범위 및 필터를 사용하여 결과를 줄이세요. |


**데이터 수집기 API**

| 범주 | 제한 | 주석 |
|:---|:---|:---|
| 단일 게시물의 최대 크기 | 30MB | 더 큰 용량은 여러 개의 게시물로 분할하세요. |
| 필드 값의 최대 크기  | 32KB | 32KB보다 긴 필드는 잘립니다. |

**API 검색**

| 범주 | 제한 | 주석 |
|:---|:---|:---|
| 단일 쿼리에 반환되는 최대 레코드 수 | 500,000 | |
| 반환되는 데이터의 최대 크기 | 64,000,000바이트(61MiB 이하)| |
| 최대 쿼리 실행 시간 | 10분 | 자세한 내용은 [시간 제한](https://dev.loganalytics.io/documentation/Using-the-API/Timeouts)을 참조하세요.  |
| 최대 요청 속도 | Azure AD 사용자 또는 클라이언트 IP 주소별로 30초당 200개 요청 | 자세한 내용은 [속도 제한](https://dev.loganalytics.io/documentation/Using-the-API/Limits)을 참조하세요. |

**Azure Monitor 로그 커넥터**

| 범주 | 제한 | 주석 |
|:---|:---|:---|
| 최대 레코드 수 | 500,000 | |
| 최대 쿼리 제한 시간 | 110초 | |
| 차트 | | 로그 페이지 및 커넥터의 시각화는 다른 차트 라이브러리를 사용하고 있으며 현재 커넥터에서 일부 기능을 사용할 수 없습니다. |

**일반 작업 영역 제한**

| 범주 | 제한 | 주석 |
|:---|:---|:---|
| 테이블의 최대 열 수         | 500 | |
| 열 이름의 최대 문자 수 | 500 | |

**<a name="data-ingestion-volume-rate">데이터 수집 볼륨 속도</a>**

Azure Monitor는 점점 더 빠른 속도로 매달 테라바이트 단위의 데이터를 보내는 수천 명의 고객을 처리하는 대규모 데이터 서비스입니다. 볼륨 속도 제한은 다중 테넌트 지원 환경의 예기치 않은 수집량 급증으로부터 Azure Monitor 고객을 격리하기 위한 것입니다. 기본 수집 볼륨 속도 임계값 500MB(압축)는 작업 영역에 정의되어 있습니다. 이 임계값은 압축되지 않은 경우에는 약 **6GB/분** 로 변환됩니다. 실제 크기는 로그 길이와 압축률에 따라 데이터 형식별로 다를 수 있습니다. 볼륨 속도 제한은 [진단 설정](../articles/azure-monitor/essentials/diagnostic-settings.md)을 통해 Azure 리소스에서 수집된 데이터에 적용됩니다. 볼륨 속도 제한에 도달하면 재시도 메커니즘은 30분 동안 4번 데이터를 수집하고 작업이 실패하면 데이터를 삭제하려고 시도합니다. [에이전트](../articles/azure-monitor/agents/agents-overview.md) 또는 [데이터 수집기 API](../articles/azure-monitor/logs/data-collector-api.md)에서 수집된 데이터에는 적용되지 않습니다.

작업 영역으로 전송된 데이터의 볼륨 속도가 작업 영역에 구성된 임계값의 80%를 초과할 경우 임계값을 계속 초과하는 동안 6시간마다 작업 영역의 *Operation* 테이블로 이벤트가 전송됩니다. 수집 볼륨 속도가 임계값을 초과할 경우 일부 데이터가 삭제되고, 임계값을 계속 초과하는 동안 6시간마다 작업 영역의 *Operation* 테이블로 이벤트가 전송됩니다. 수집 볼륨 속도가 임계값을 계속 초과하거나 곧 도달할 것으로 예상되는 경우 지원 요청을 열어 임계값 상향 조정을 요청할 수 있습니다. 

수집 제한에 도달할 때 사전에 알리도록 경고 규칙을 만들려면 [Azure Monitor에서 Log Analytics 작업 영역의 상태 모니터링](../articles/azure-monitor/logs/monitor-workspace.md)을 참조하세요.

>[!NOTE]
>Log Analytics를 사용한 기간에 따라 레거시 가격 책정 계층에 대한 액세스 권한이 있을 수 있습니다. [Log Analytics 레거시 가격 책정 계층](../articles/azure-monitor/logs/manage-cost-storage.md#legacy-pricing-tiers)에 대해 자세히 알아보세요.