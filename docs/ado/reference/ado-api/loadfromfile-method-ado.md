---
description: LoadFromFile 方法 (ADO)
title: " (ADO) 的 LoadFromFile 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f07bd7bc6b04dac8c5b352cc6281ce4eb851d3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443350"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
將現有檔案的內容載入至 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 **字串**值，包含要載入**資料流程**中的檔案名。 *檔案名* 可以包含 UNC 格式的任何有效路徑和名稱。 如果指定的檔案不存在，就會發生執行階段錯誤。  
  
## <a name="remarks"></a>備註  
 這個方法可以用來將本機檔案的內容載入 **資料流程** 物件中。 這可以用來將本機檔案的內容上傳到伺服器。  
  
 在呼叫**LoadFromFile**之前，**資料流程**物件必須已經開啟。 這個方法不會變更**資料流程**物件的系結。它仍會系結至原始用來開啟**資料流程**的 URL 或**記錄**所指定的物件。  
  
 **LoadFromFile** 會使用從檔案讀取的資料來覆寫 **資料流程** 物件的目前內容。 檔案的內容會覆寫 **資料流程** 中的任何現有位元組。 在**LoadFromFile**所建立的[EOS](../../../ado/reference/ado-api/eos-property.md)之後，任何先前存在和剩餘的位元組都會遭到截斷。  
  
 呼叫 **LoadFromFile**之後，目前的位置會設定為 **資料流程** 的開頭 ([位置](../../../ado/reference/ado-api/position-property-ado.md) 是 0) 。  
  
 因為可能會將2個位元組新增至資料流程的開頭以進行編碼，所以資料流程的大小可能不會完全符合載入該資料流程的檔案大小。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
