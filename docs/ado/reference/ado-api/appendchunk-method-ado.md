---
title: "AppendChunk 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords: AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 733dbd43501211c631fad51f993b8d663da0d844
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="appendchunk-method-ado"></a>AppendChunk 方法 (ADO)
將資料附加至大型文字或二進位資料[欄位](../../../ado/reference/ado-api/field-object.md)，或[參數](../../../ado/reference/ado-api/parameter-object.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>參數  
 *物件*  
 A**欄位**或**參數**物件。  
  
 *資料*  
 A **Variant** ，其中包含要附加至物件的資料。  
  
## <a name="remarks"></a>備註  
 使用**AppendChunk**方法**欄位**或**參數**填入長二進位或字元資料的物件。 在系統記憶體的限制狀況下，您可以使用**AppendChunk**方法來處理部分中，而不是完整的長值。  
  
## <a name="field"></a>欄位  
 如果**adFldLong**位元[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性**欄位**物件設定為**true**，您可以使用**AppendChunk**該欄位的方法。  
  
 第一個**AppendChunk**上呼叫**欄位**物件會將資料寫入欄位，並覆寫任何現有的資料。 後續**AppendChunk**呼叫加入至現有的資料。 如果您將資料附加到一個欄位，然後設定或讀取目前記錄中的另一個欄位的值，ADO 會假設您已完成將資料附加到第一個欄位。 如果您呼叫**AppendChunk**方法上的第一個欄位，ADO 會解譯為新的呼叫**AppendChunk**作業，並覆寫現有的資料。 存取其他欄位[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)不是複製程式碼的第一個物件**資料錄集**物件不會破壞**AppendChunk**作業。  
  
 如果當您呼叫會有無目前記錄**AppendChunk**上**欄位**物件時，發生錯誤。  
  
> [!NOTE]
>  **AppendChunk**方法不能進行**欄位**物件[記錄 Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)物件。 它不會執行任何作業，並會產生執行階段錯誤。  
  
## <a name="parameter"></a>參數  
 如果**adParamLong**位元**屬性**屬性**參數**物件設定為**true**，您可以使用**AppendChunk**該參數的方法。  
  
 第一個**AppendChunk**上呼叫**參數**物件會將資料寫入至參數，覆寫任何現有的資料。 後續**AppendChunk**上呼叫**參數**物件加入至現有的參數資料。 **AppendChunk**傳遞 null 值的呼叫就會捨棄所有參數的資料。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Field 物件](../../../ado/reference/ado-api/field-object.md)|[Parameter 物件](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>請參閱  
 [AppendChunk 和 GetChunk 方法範例 (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 和 GetChunk 方法範例 （VC + +）](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [屬性的內容 (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [GetChunk 方法 (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
