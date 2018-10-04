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
manager: craigg
ms.openlocfilehash: 4267776593637a01aef38a218f7272261fd1d448
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789186"
---
# <a name="definedsize-property"></a>DefinedSize 屬性
表示的資料容量[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，以反映所定義的大小的欄位，欄位的欄位物件的資料類型而定，請參閱[型別](../../../ado/reference/ado-api/type-property-ado.md)如需詳細資訊。 使用的固定長度資料類型的欄位，傳回的值會是資料類型，以位元組為單位的大小。 使用可變長度資料類型的欄位，這是下列其中一項：  
  
1.  以字元為單位的欄位的最大長度 (如**adVarChar**和**adVarWChar**) 或以位元組為單位 (如**adVarBinary**，和**adVarNumeric**) 的欄位是否已定義的長度。 例如， **adVarChar(5)** 欄位的最大長度為 5。  
  
2.  以字元為單位的資料類型的最大長度 (如**adChar**並**adWChar**) 或以位元組為單位 (如**adBinary**和**adNumeric**) 如果欄位沒有定義的長度。  
  
3.  ~ 0 (位元，值不是 0，所有位元會設為 1) 如果欄位和資料類型都不具有已定義的最大長度。  
  
4.  對於沒有長度的資料型別，這會設定為 ~ 0 (位元，值不是 0，所有位元會設為 1)。  
  
## <a name="remarks"></a>備註  
 使用**DefinedSize**屬性來判斷的資料容量**欄位**物件。  
  
 **DefinedSize**並[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性都不同。 例如，請考慮**欄位**宣告類型的物件**adVarChar**並**DefinedSize**屬性值為 50，其中包含單一字元。 **ActualSize**它所傳回的屬性值是單一字元的長度以位元組為單位。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 屬性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
