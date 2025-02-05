---
title: 파일 포함
description: 포함 파일
services: functions
author: craigshoemaker
manager: gwallace
ms.service: azure-functions
ms.topic: include
ms.date: 08/02/2019
ms.author: cshoe
ms.custom: include file
ms.openlocfilehash: 16ab569428510b3b423d6727fd31ee450a8d197e
ms.sourcegitcommit: 867cb1b7a1f3a1f0b427282c648d411d0ca4f81f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2021
ms.locfileid: "100381610"
---
### <a name="default"></a>기본값

트리거 Blob에 대한 다음 매개 변수 형식을 사용할 수 있습니다.

* `Stream`
* `TextReader`
* `string`
* `Byte[]`
* `ICloudBlob`<sup>1</sup>
* `CloudBlockBlob`<sup>1</sup>
* `CloudPageBlob`<sup>1</sup>
* `CloudAppendBlob`<sup>1</sup>

<sup>1</sup>*function.json* 에서 `direction` 또는 C# 클래스 라이브러리에서 `FileAccess.ReadWrite`의 “inout” 바인딩이 필요합니다.

스토리지 SDK 형식 중 하나에 바인딩하려고 하면 오류 메시지가 표시되는 경우 [올바른 Storage SDK 버전](../articles/azure-functions/functions-bindings-storage-blob.md#azure-storage-sdk-version-in-functions-1x)에 대한 참조가 있는지 확인합니다.

`string` 또는 `Byte[]`에 바인딩하는 방식은 전체 Blob 내용이 메모리에 로드되므로 Blob 크기가 작은 경우에만 권장됩니다. 일반적으로 `Stream` 또는 `CloudBlockBlob` 형식을 사용하는 것이 좋습니다. 자세한 내용은 이 문서의 뒷부분에 나오는 [동시성 및 메모리 사용량](../articles/azure-functions/functions-bindings-storage-blob-trigger.md#concurrency-and-memory-usage)을 참조하세요.

### <a name="additional-types"></a>추가 형식

[5.0.0 이상 버전의 스토리지 확장](../articles/azure-functions/functions-bindings-storage-blob.md#storage-extension-5x-and-higher)을 사용하는 앱은 [.NET용 Azure SDK](/dotnet/api/overview/azure/storage.blobs-readme)의 형식을 사용할 수도 있습니다. 이 버전은 다음 형식을 위해 레거시 `ICloudBlob`, `CloudBlockBlob`, `CloudPageBlob` 및 `CloudAppendBlob` 형식에 대한 지원을 중단합니다.

- [BlobClient](/dotnet/api/azure.storage.blobs.blobclient)<sup>1</sup>
- [BlockBlobClient](/dotnet/api/azure.storage.blobs.specialized.blockblobclient)<sup>1</sup>
- [PageBlobClient](/dotnet/api/azure.storage.blobs.specialized.pageblobclient)<sup>1</sup>
- [AppendBlobClient](/dotnet/api/azure.storage.blobs.specialized.appendblobclient)<sup>1</sup>
- [BlobBaseClient](/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)<sup>1</sup>

<sup>1</sup>*function.json* 에서 `direction` 또는 C# 클래스 라이브러리에서 `FileAccess.ReadWrite`의 “inout” 바인딩이 필요합니다.

이러한 형식을 사용하는 예제는 [확장에 대한 GitHub 리포지토리](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs#examples)를 참조하세요.
