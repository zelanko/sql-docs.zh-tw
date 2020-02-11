---
title: DefinedSize 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4bfb0db701801f1853009594b9d6d24aeb41c629
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933217"
---
# <a name="definedsize-property"></a>DefinedSize 屬性
指出[欄位](../../../ado/reference/ado-api/field-object.md)物件的資料容量。  
  
## <a name="return-value"></a>傳回值  
 傳回**Long**值，反映欄位的定義大小，這取決於 field 物件的資料類型。如需詳細資訊，請參閱[類型](../../../ado/reference/ado-api/type-property-ado.md)。 對於使用固定長度資料類型的欄位，傳回值是資料類型的大小（以位元組為單位）。 對於使用可變長度資料類型的欄位，這是下列其中一項：  
  
1.  欄位的最大長度（ **adVarChar**和**adVarWChar**），如果欄位具有已定義的長度，則為以位元組為單位（適用于**adVarBinary**和**adVarNumeric**）。 例如， **adVarChar （5）** 欄位的最大長度為5。  
  
2.  資料類型的最大長度，以字元為單位（ **adChar**和**adWChar**），如果欄位沒有定義的長度，則為位元組（若為**adBinary**和**adNumeric**）。  
  
3.  ~ 0 （位，值不是 0; 如果欄位或資料類型都沒有定義的最大長度，則所有位都會設為1）。  
  
4.  對於長度不是的資料類型，這會設定為 ~ 0 （位，值不是 0; 所有位都設為1）。  
  
## <a name="remarks"></a>備註  
 使用**DefinedSize**屬性來判斷**欄位**物件的資料容量。  
  
 **DefinedSize**和[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性不同。 例如，假設**欄位**物件的宣告類型為**AdVarChar** ，而**DefinedSize**屬性值為50，其中包含單一字元。 它所傳回的**ActualSize**屬性值是單一字元的長度（以位元組為單位）。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例（VB）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例（VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 屬性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
