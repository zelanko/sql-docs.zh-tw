---
title: LoadFromFile 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: b7f4b28a7d63654441d8a66730e729483596b3a8
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754574"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 方法 (ADO)
將現有檔案的內容載入[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 **字串**值，包含要載入至**資料流程**中的檔案名。 *FileName*可以包含 UNC 格式的任何有效路徑和名稱。 如果指定的檔案不存在，就會發生執行階段錯誤。  
  
## <a name="remarks"></a>備註  
 這個方法可以用來將本機檔案的內容載入**資料流程**物件中。 這可以用來將本機檔案的內容上傳至伺服器。  
  
 在呼叫**LoadFromFile**之前，**資料流程**物件必須已經開啟。 這個方法不會變更**資料流程**物件的系結。它仍然會系結至原始開啟**資料流程**的 URL 或**記錄**所指定的物件。  
  
 **LoadFromFile**會使用從檔案讀取的資料，覆寫**資料流程**物件的目前內容。 檔案的內容會覆寫**資料流程**中的任何現有位元組。 在**LoadFromFile**所建立的[EOS](../../../ado/reference/ado-api/eos-property.md)之後，任何先前現有和剩餘的位元組都會遭到截斷。  
  
 呼叫**LoadFromFile**之後，目前的位置會設定為**資料流程**的開頭（[position](../../../ado/reference/ado-api/position-property-ado.md)是0）。  
  
 因為可能會將2個位元組新增至資料流程的開頭以進行編碼，所以資料流程的大小可能不會與載入它的檔案大小完全相符。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
