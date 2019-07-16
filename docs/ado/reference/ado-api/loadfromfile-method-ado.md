---
title: LoadFromFile 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce90b13a677246fb64462fbe691eb9e3efaa3c7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918274"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
將現有檔案的內容載入[Stream](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 A**字串**值，其中包含要載入的檔案名稱**Stream**。 *檔名*可包含任何有效的路徑以及 UNC 格式的名稱。 如果指定的檔案不存在，就會發生執行階段錯誤。  
  
## <a name="remarks"></a>備註  
 這個方法可用來將本機檔案的內容載入**Stream**物件。 這可用來將本機檔案的內容上傳至伺服器。  
  
 **Stream**物件必須是已開啟，再呼叫**LoadFromFile**。 這個方法不會變更的繫結**Stream**物件，它將仍會繫結至的 URL 所指定的物件或**記錄**與其**Stream**原本開啟。  
  
 **LoadFromFile**會覆寫目前的內容**Stream**物件從檔案讀取的資料。 中的任何現有位元組**Stream**會覆寫檔案的內容。 下列任何先前現有和剩餘的位元組[EOS](../../../ado/reference/ado-api/eos-property.md)由**LoadFromFile**，就會遭到截斷。  
  
 若要在呼叫之後**LoadFromFile**，目前的位置會設定為開頭**Stream** ([位置](../../../ado/reference/ado-api/position-property-ado.md)為 0)。  
  
 編碼的資料流的開頭可能會加入 2 個位元組，因為資料流的大小可能不完全符合的檔案載入它的大小。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
