---
description: GetChunk 方法 (ADO)
title: " (ADO) 的 GetChunk 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 38e1375f0439cbc17d19c3a416bbc51cea01239b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443590"
---
# <a name="getchunk-method-ado"></a>GetChunk 方法 (ADO)
傳回大型文字或二進位資料 [欄位](../../../ado/reference/ado-api/field-object.md) 物件的所有或部分內容。  
  
## <a name="syntax"></a>語法  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **Variant**。  
  
#### <a name="parameters"></a>參數  
 *大小*  
 **長**運算式，等於您要取出的位元組數或字元數。  
  
## <a name="remarks"></a>備註  
 在**欄位**物件上使用**GetChunk**方法，以取出部分或所有的完整二進位或字元資料。 在系統記憶體受限的情況下，您可以使用 **GetChunk** 方法，在部分（而不是整個）中操作長值。  
  
 **GetChunk**呼叫傳回的資料會指派給*變數*。 如果 *大小* 大於剩餘的資料， **GetChunk** 方法只會傳回剩餘的資料，但不含空格的填補 *變數* 。 如果欄位是空的， **GetChunk** 方法會傳回 null 值。  
  
 每個後續的 **GetChunk** 呼叫都會從先前的 **GetChunk** 呼叫離開的位置開始抓取資料。 但是，如果您要從某個欄位抓取資料，然後設定或讀取目前記錄中另一個欄位的值，則 ADO 會假設您已完成從第一個欄位中取出資料。 如果您再次在第一個欄位上呼叫 **GetChunk** 方法，則 ADO 會將呼叫解讀為新的 **GetChunk** 作業，並開始從資料的開頭開始讀取。 存取其他 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件中非第一個 **記錄集** 物件的欄位，將不會中斷 **GetChunk** 作業。  
  
 如果**field**物件的[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性中的**adFldLong**位設為**True**，則您可以針對該欄位使用**GetChunk**方法。  
  
 當您在**欄位**物件上使用**GetChunk**方法時，如果沒有目前的記錄，則會發生錯誤 3021 (不會) 發生目前的記錄。  
  
> [!NOTE]
>  **GetChunk**方法不會在[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的**欄位**物件上運作。 它不會執行任何作業，而且會產生執行階段錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [AppendChunk 和 GetChunk 方法範例 (VB) ](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法範例 (VC + +) ](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [ (ADO) 的 AppendChunk 方法 ](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Attributes 屬性 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
