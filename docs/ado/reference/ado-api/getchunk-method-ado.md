---
title: GetChunk 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: 43c5fef08d22364b9842c58fc82d46ba4bfa00bd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918558"
---
# <a name="getchunk-method-ado"></a>GetChunk 方法 (ADO)
傳回大型文字或二進位資料[欄位](../../../ado/reference/ado-api/field-object.md)物件的所有或部分內容。  
  
## <a name="syntax"></a>語法  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**Variant**。  
  
#### <a name="parameters"></a>參數  
 *大小*  
 **長**運算式，等於您要抓取的位元組或字元數。  
  
## <a name="remarks"></a>備註  
 請在**Field**物件上使用**GetChunk**方法，以取出部分或整個完整的二進位或字元資料。 在系統記憶體受到限制的情況下，您可以使用**GetChunk**方法來管理部分中的長數值，而不是完整的值。  
  
 **GetChunk**呼叫傳回的資料會指派給*變數*。 如果*大小*大於剩餘的資料， **GetChunk**方法只會傳回剩餘的資料，而不含空格的填補*變數*。 如果欄位是空的，則**GetChunk**方法會傳回 null 值。  
  
 每個後續的**GetChunk**呼叫都會從先前的**GetChunk**呼叫停止的位置，抓取開始的資料。 不過，如果您要從某個欄位抓取資料，然後設定或讀取目前記錄中另一個欄位的值，ADO 會假設您已完成從第一個欄位抓取資料。 如果您再次呼叫第一個欄位上的**GetChunk**方法，ADO 會將呼叫解讀為新的**GetChunk**作業，並開始讀取資料的開頭。 存取不是第一個**記錄集**物件複製之其他[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的欄位，將不會中斷**GetChunk**作業。  
  
 如果**欄位**物件的[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性中的**adFldLong**位設定為**True**，您可以針對該欄位使用**GetChunk**方法。  
  
 當您在**欄位**物件上使用**GetChunk**方法時，如果沒有目前的記錄，則會發生錯誤3021（沒有目前的記錄）。  
  
> [!NOTE]
>  **GetChunk**方法不會在[Record](../../../ado/reference/ado-api/record-object-ado.md)物件的**欄位**物件上操作。 它不會執行任何作業，而且會產生執行階段錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [AppendChunk 和 GetChunk 方法範例（VB）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法範例（VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [AppendChunk 方法（ADO）](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
