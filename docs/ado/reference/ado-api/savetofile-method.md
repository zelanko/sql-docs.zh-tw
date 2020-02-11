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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917028"
---
# <a name="savetofile-method"></a>SaveToFile 方法
將[資料流程](../../../ado/reference/ado-api/stream-object-ado.md)的二進位內容儲存至檔案。  
  
## <a name="syntax"></a>語法  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **字串**值，其中包含將儲存**資料流程**內容之檔案的完整名稱。 您可以儲存至任何有效的本機位置，或您可透過 UNC 值存取的任何位置。  
  
 *System.xml.linq.saveoptions>*  
 [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md)值，指定是否應該在**SaveToFile**建立新檔案（如果尚未存在的話）。 預設值為**adSaveCreateNotExists**。 您可以使用這些選項指定如果指定的檔案不存在，就會發生錯誤。 您也可以指定**SaveToFile**覆寫現有檔案的目前內容。  
  
> [!NOTE]
>  如果您覆寫現有的檔案（當設定**adSaveCreateOverwrite**時）， **SaveToFile**會從新的[EOS](../../../ado/reference/ado-api/eos-property.md)後面的原始現有檔案截斷任何位元組。  
  
## <a name="remarks"></a>備註  
 **SaveToFile**可以用來將**資料流程**物件的內容複寫到本機檔案。 **資料流程**物件的內容或屬性不會有任何變更。 在呼叫**SaveToFile**之前，必須先開啟**資料流程**物件。  
  
 這個方法不會將**資料流程**物件的關聯變更為其基礎來源。 在開啟時，**資料流程**物件仍會與原始 URL 或其來源的**記錄**相關聯。  
  
 在**SaveToFile**作業之後，資料流程中的目前位置（[位置](../../../ado/reference/ado-api/position-property-ado.md)）會設定為數據流的開頭（0）。  
  
## <a name="applies-to"></a>套用至  
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法（ADO Stream）](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
