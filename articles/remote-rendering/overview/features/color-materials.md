---
title: 색 재질
description: 색 재질 유형을 설명 합니다.
author: jakrams
ms.author: jakras
ms.date: 02/11/2020
ms.topic: article
ms.openlocfilehash: fb26a669229ac140aba262032f8ce84ef9f37727
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "99593386"
---
# <a name="color-materials"></a>색 재질

*색 자료* 는 Azure 원격 렌더링에서 지원 되는 [재질 유형](../../concepts/materials.md) 중 하나입니다. 모든 종류의 조명을 받지 않아야 하는 [메시](../../concepts/meshes.md) 에 사용 되며 항상 전체 밝기가 됩니다. 자동차 대시보드, 광원 전구 등의 ' 반짝이 ' 자료 또는 [photogrammetry](https://en.wikipedia.org/wiki/Photogrammetry)을 통해 얻은 모델과 같이 고정 조명을 이미 포함 하는 데이터의 경우이 경우를 들 수 있습니다.

색 자료는 더 간단한 음영 [모델 때문에](pbr-materials.md) ,이를 통해 더 효율적으로 사용할 수 있습니다. 다른 투명도 모드도 지원 합니다.

## <a name="common-material-properties"></a>공통 재질 속성

이러한 속성은 모든 자료에 공통적입니다.

* **Albedocolor:** 이 색을 *Albedomap* 또는 *:::no-loc text="vertex"::: colors* 와 같은 다른 색과 곱합니다. 재질에서 *투명도* 를 사용 하는 경우 알파 채널을 사용 하 여 불투명도를 조정 하 `1` 고 완전히 불투명 하며 `0` 의미를 완전히 투명 하 게 나타냅니다. 기본값은 흰색입니다.

  > [!NOTE]
  > 색 자료는 환경을 반영 하지 않으므로 완전히 투명 한 색 재질은 보이지 않게 됩니다. 이는 [.pbr 자료](pbr-materials.md)에서 다릅니다.

* **Albedomap:** 픽셀 별 albedo 값에 대 한 [2d 질감](../../concepts/textures.md) 입니다.

* **alphaClipEnabled** 및 **alphaClipThreshold:** *alphaClipEnabled* 가 true 이면 Albedo 알파 값이 *alphaClipThreshold* 보다 낮은 모든 픽셀은 그려지지 않습니다. 알파 클리핑을 투명도를 사용 하지 않고도 사용할 수 있으며 렌더링 속도가 훨씬 빠릅니다. 그러나 알파 클리핑 재질은 완전히 불투명 한 재질 보다 렌더링 하는 속도가 느립니다. 기본적으로 알파 클리핑을 사용 하지 않도록 설정 됩니다.

* **textureCoordinateScale** 및 **textureCoordinateOffset:** 눈금은 UV 질감 좌표에 곱하고이에 오프셋을 추가 합니다. 질감을 늘이거나 이동 하는 데 사용할 수 있습니다. 기본 소수 자릿수는 (1, 1)이 고 offset은 (0, 0)입니다.

* **useVertexColor:** 메시에 :::no-loc text="vertex"::: 색이 포함 되어 있고이 옵션을 사용 하는 경우 망상의 :::no-loc text="vertex"::: 색을 *albedocolor* 및 *albedocolor* 에 곱합니다. 기본적으로 *useVertexColor* 는 사용 되지 않습니다.

* **isDoubleSided:** 이중 sidedness가 true로 설정 된 경우 카메라가 뒷면 얼굴을 보는 경우에도이 재질의 삼각형이 렌더링 됩니다. 기본적으로이 옵션은 사용할 수 없습니다. [ :::no-loc text="Single-sided"::: 렌더링](single-sided-rendering.md)도 참조 하세요.

* **TransparencyWritesDepth:** TransparencyWritesDepth 플래그가 재질에 설정 되어 있고 자료가 투명 하면이 자료를 사용 하는 개체는 최종 깊이 버퍼에도 영향을 주지 않습니다. 다음 섹션에서 색 재질 속성 *transparencyMode* 을 참조 하세요. 이 기능을 사용 하는 경우 사용 사례에 완전히 투명 한 장면에 대 한 보다 타당 [늦은 단계 다시 프로젝션이](late-stage-reprojection.md) 필요한 경우에 권장 됩니다. 불투명 투명/투명 한 장면을 혼합 하는 경우이 설정으로 인해 집합 reprojection 동작이 나 reprojection 아티팩트가 발생할 수 있습니다. 이러한 이유로 일반 사용 사례에 대 한 기본 및 권장 설정은이 플래그를 사용 하지 않도록 설정 하는 것입니다. 작성 된 깊이 값은 카메라에 가장 가까운 개체의 픽셀 별 깊이 계층에서 가져옵니다.

* **FresnelEffect:** 이 재질 플래그를 사용 하면 해당 재질에서 가산 [프레스 넬 대칭 효과](../../overview/features/fresnel-effect.md) 를 사용할 수 있습니다. 효과의 모양은 다음에 설명 된 다른 프레스 넬 대칭 매개 변수에 의해 제어 됩니다. 

* **FresnelEffectColor:** 이 재질에 사용 되는 프레스 넬 대칭 색입니다. 이 자료에 프레스 넬 대칭 효과 비트가 설정 된 경우에만 중요 합니다 (위 참조). 이 속성은 프레스 넬 대칭 빛의 기본 색을 제어 합니다 (전체 설명에 대 한 [프레스 넬 대칭 효과](../../overview/features/fresnel-effect.md) 참조). 현재는 rgb 채널 값만 중요 하며 알파 값은 무시 됩니다.

* **FresnelEffectExponent:** 이 재질에 사용 되는 프레스 넬 대칭 지 수입니다. 이 자료에 프레스 넬 대칭 효과 비트가 설정 된 경우에만 중요 합니다 (위 참조). 이 속성은 프레스 넬 대칭 빛의 스프레드를 제어 합니다. 최소값 0.01은 전체 개체에 걸쳐 분산 됩니다. 최 댓 값 10.0은 제한를 가장 gracing 가장자리로 표시 합니다.

## <a name="color-material-properties"></a>색 재질 속성

다음 속성은 색 재질에만 적용 됩니다.

* **vertexMix:** 과 사이의이 `0` 값 `1` 은 :::no-loc text="vertex"::: [망상](../../concepts/meshes.md) 의 색이 최종 색에 기여 하는 정도를 지정 합니다. 기본값 1에서 :::no-loc text="vertex"::: 색은 albedo 색에 완전히 곱합니다. 값이 0 이면 :::no-loc text="vertex"::: 색이 완전히 무시 됩니다.

* **transparencyMode:** 다른 투명도 [모드를 구분 하는 경우](pbr-materials.md), 즉,

  1. **불투명:** 기본 모드에서는 투명도를 사용 하지 않습니다. 그러나 알파 캡처는 여전히 가능 하지만 충분 한 경우에는 선호 해야 합니다.
  
  1. **AlphaBlended:** 이 모드는 .PBR 재질의 투명도 모드와 비슷합니다. 유리와 같은 보기 자료에 사용 해야 합니다.

  1. **덧셈:** 이 모드는 가장 간단 하 고 가장 효율적인 투명도 모드입니다. 재질의 기여는 렌더링 된 이미지에 추가 됩니다. 이 모드는 중요 한 개체를 강조 표시 하는 데 사용 되는 표식과 같이 투명 한 개체 (투명 한 개체)를 시뮬레이트하는 데 사용할 수 있습니다.

## <a name="api-documentation"></a>API 설명서

* [C # Colormaterial 클래스](/dotnet/api/microsoft.azure.remoterendering.colormaterial)
* [C # RenderingConnection CreateMaterial ()](/dotnet/api/microsoft.azure.remoterendering.renderingconnection.creatematerial)
* [C + + ColorMaterial 클래스](/cpp/api/remote-rendering/colormaterial)
* [C + + RenderingConnection:: CreateMaterial ()](/cpp/api/remote-rendering/renderingconnection#creatematerial)

## <a name="next-steps"></a>다음 단계

* [PBR 재질](pbr-materials.md)
* [질감](../../concepts/textures.md)
* [메시](../../concepts/meshes.md)