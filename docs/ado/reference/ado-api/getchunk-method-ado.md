---
title: GetChunk 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 538ccfd71375521bf0ba035ccfa55746c4d76af9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028045"
---
# <a name="getchunk-method-ado"></a>GetChunk 方法 (ADO)
傳回全部或部分，大型文字或二進位資料的內容[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**。  
  
#### <a name="parameters"></a>參數  
 *大小*  
 A**長**等於您想要擷取的字元或位元組數目的運算式。  
  
## <a name="remarks"></a>備註  
 使用**GetChunk**方法**欄位**擷取部分或所有長二進位或字元資料的物件。 在其中的系統記憶體是有限的情況下，您可以使用**GetChunk**方法來操作部分，而不是完整的長值。  
  
 資料可**GetChunk**呼叫會傳回指派給*變數*。 如果*大小*大於剩餘的資料， **GetChunk**方法會傳回只剩餘的資料沒有填補*變數*空白空間。 如果欄位是空的**GetChunk**方法會傳回 null 值。  
  
 每個後續**GetChunk**呼叫會擷取從何處開始的資料先前**GetChunk**離開的呼叫。 不過，如果您要擷取的資料從一個欄位，然後您可以設定或讀取目前的記錄中的另一個欄位的值，ADO 會假設您已完成擷取第一個欄位的資料。 如果您呼叫**GetChunk**方法的第一個欄位，ADO 會解譯為新的呼叫**GetChunk**作業，並讀取資料的開頭開始。 存取其他欄位[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)不是複製程式碼的第一個物件**資料錄集**物件並不會影響**GetChunk**作業。  
  
 如果**adFldLong**位元[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性**欄位**物件設定為**True**，您可以使用**GetChunk**該欄位的方法。  
  
 如果當您使用會有任何目前的資料錄**GetChunk**方法**欄位**物件時，就會發生錯誤 3021 （沒有目前的記錄）。  
  
> [!NOTE]
>  **GetChunk**方法上無法運作**欄位**的物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 它不會執行任何作業，並會在產生執行階段錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [AppendChunk 和 GetChunk 方法範例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法範例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 方法 (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
