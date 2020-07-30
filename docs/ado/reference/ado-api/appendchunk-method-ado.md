---
title: AppendChunk 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e3d58ae93285accc9cf7a71e43579be4f54b21d
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242458"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
將資料附加至大型文字或二進位資料[欄位](../../../ado/reference/ado-api/field-object.md)或[參數](../../../ado/reference/ado-api/parameter-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>參數  
 *object*  
 **欄位**或**參數**物件。  
  
 *Data*  
 包含要附加至物件之資料的**Variant** 。  
  
## <a name="remarks"></a>備註  
 在**欄位**或**參數**物件上使用**AppendChunk**方法，以完整的二進位或字元資料填滿它。 在系統記憶體有限的情況下，您可以使用**AppendChunk**方法來管理部分中的長值，而不是完整的。  
  
## <a name="field"></a>欄位  
 如果**欄位**物件的[Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性中的**adFldLong**位設定為**true**，您可以針對該欄位使用**AppendChunk**方法。  
  
 **Field**物件上的第一個**AppendChunk**呼叫會將資料寫入欄位，並覆寫任何現有的資料。 後續的**AppendChunk**呼叫會新增至現有的資料。 如果您要將資料附加至一個欄位，然後設定或讀取目前記錄中另一個欄位的值，ADO 會假設您已完成將資料附加至第一個欄位。 如果您再次呼叫第一個欄位上的**AppendChunk**方法，ADO 會將呼叫解讀為新的**AppendChunk**作業，並覆寫現有的資料。 存取不是第一個**記錄集**物件複製之其他[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的欄位，將不會中斷**AppendChunk**作業。  
  
 當您在**欄位**物件上呼叫**AppendChunk**時，如果沒有目前的記錄，就會發生錯誤。  
  
> [!NOTE]
>  **AppendChunk**方法不會在[RECORD 物件（ADO）](../../../ado/reference/ado-api/record-object-ado.md)物件的**欄位**物件上運作。 它不會執行任何作業，而且會產生執行階段錯誤。  
  
## <a name="parameter"></a>參數  
 如果**參數**物件的**Attributes**屬性中的**adParamLong**位設定為**true**，則您可以對該參數使用**AppendChunk**方法。  
  
 **參數**物件上的第一個**AppendChunk**呼叫會將資料寫入至參數，並覆寫任何現有的資料。 後續在**參數**物件上呼叫的**AppendChunk**會新增至現有的參數資料。 傳遞 null 值的**AppendChunk**呼叫會捨棄所有參數資料。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Field 物件](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [AppendChunk 和 GetChunk 方法範例（VB）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法範例（VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 屬性（ADO）](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
