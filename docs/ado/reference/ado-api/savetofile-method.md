---
title: SaveToFile 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2e56178ad306d5b39c2445c391c3bbabe4fc424
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917028"
---
# <a name="savetofile-method"></a>SaveToFile 方法
將儲存的二進位內容[Stream](../../../ado/reference/ado-api/stream-object-ado.md)至檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>參數  
 *FileName*  
 A**字串**值，其中包含之檔案的完整限定名稱的內容**Stream**會儲存。 您可以將它儲存至任何有效的本機位置，或您可以存取透過 UNC 值的任何位置。  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)值，指定是否應該藉由建立新的檔案**SaveToFile**，如果不存在。 預設值是**adSaveCreateNotExists**。 您可以使用這些選項，指定是否指定的檔案不存在，會發生錯誤。 您也可以指定**SaveToFile**覆寫現有檔案的目前內容。  
  
> [!NOTE]
>  如果您要覆寫現有檔案 (當**adSaveCreateOverwrite**設定)， **SaveToFile**截斷任何位元組從原始的現有檔案，請遵循新[EOS](../../../ado/reference/ado-api/eos-property.md)。  
  
## <a name="remarks"></a>備註  
 **SaveToFile**可用來將內容複製**Stream**到本機檔案的物件。 沒有任何內容或屬性中的變更**Stream**物件。 **Stream**物件必須為開啟狀態，然後再呼叫**SaveToFile**。  
  
 這個方法不會變更的關聯**Stream**其基礎來源的物件。 **Stream**物件仍然會與原始的 URL 相關聯或是**記錄**，已開啟時，其來源。  
  
 在後**SaveToFile**作業，目前的位置 ([位置](../../../ado/reference/ado-api/position-property-ado.md)) 資料流中設為 (0) 的資料流的開頭。  
  
## <a name="applies-to"></a>適用於  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
