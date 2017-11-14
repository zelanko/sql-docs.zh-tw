---
title: "LoadFromFile 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bbb4b032f3cb386c0915e04b949b3244edbb1c4a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
載入到現有的檔案內容[資料流](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 A**字串**值，包含要載入之檔案的名稱**資料流**。 *檔名*可以包含任何有效的路徑和 UNC 格式的名稱。 如果指定的檔案不存在，就會發生執行階段錯誤。  
  
## <a name="remarks"></a>備註  
 這個方法可以用來載入到本機檔案的內容**資料流**物件。 這可以用於本機檔案的內容上傳至伺服器。  
  
 **資料流**物件必須是已開啟，然後再呼叫**LoadFromFile**。 這個方法不會變更的繫結**資料流**物件; 它會仍繫結至由 URL 指定的物件或**記錄**與其**資料流**原本開啟。  
  
 **LoadFromFile**會覆寫目前的內容**資料流**物件從檔案讀取的資料。 中的任何現有位元組**資料流**會覆寫檔案的內容。 下列任何先前現有和剩餘的位元組[EOS](../../../ado/reference/ado-api/eos-property.md)由**LoadFromFile**，會被截斷。  
  
 若要在呼叫之後**LoadFromFile**，目前的位置會設定為開頭**資料流**([位置](../../../ado/reference/ado-api/position-property-ado.md)為 0)。  
  
 編碼的資料流的開頭，可能會增加 2 個位元組，因為資料流的大小可能不完全相同的檔案載入它的大小。  
  
## <a name="applies-to"></a>適用於  
 [資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

