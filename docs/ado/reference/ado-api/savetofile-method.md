---
title: "SaveToFile 方法 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2326257da632839c9b60d630f25adb604018272d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="savetofile-method"></a>SaveToFile 方法
將儲存的二進位內容[資料流](../../../ado/reference/ado-api/stream-object-ado.md)至檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 A**字串**值，其中包含之檔案所在的完整限定名稱的內容**資料流**將會儲存。 您可以將它儲存至任何有效的本機位置，或您可以存取透過 UNC 值的任何位置。  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)值，指定是否應該由建立新的檔案**SaveToFile**，如果不存在。 預設值是**adSaveCreateNotExists**。 您可以使用這些選項指定是否指定的檔案不存在，會發生錯誤。 您也可以指定**SaveToFile**覆寫現有檔案的目前內容。  
  
> [!NOTE]
>  如果您覆寫現有的檔案 (當**adSaveCreateOverwrite**設定)， **SaveToFile**會截斷任何位元組從原始的現有檔案，請遵循新[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>備註  
 **SaveToFile**可能用來將內容複製**資料流**到本機檔案的物件。 中的內容或屬性沒有變更**資料流**物件。 **資料流**物件必須為開啟狀態，然後再呼叫**SaveToFile**。  
  
 這個方法不會變更的關聯**資料流**其底層的來源物件。 **資料流**物件仍會與原始的 URL 相關聯或**記錄**，已開啟時，其來源。  
  
 之後**SaveToFile**作業，目前的位置 ([位置](../../../ado/reference/ado-api/position-property-ado.md)) 資料流中設為 (0) 的資料流的開頭。  
  
## <a name="applies-to"></a>適用於  
 [資料流物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 （ADO 資料流）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)

