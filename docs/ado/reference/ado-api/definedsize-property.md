---
title: DefinedSize 屬性 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b78fe75314e6e2aacf5c6f0d9c599f5cb6db6292
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="definedsize-property"></a>DefinedSize 屬性
表示的資料容量[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，反映所定義的大小的欄位，這取決於資料類型的欄位物件，請參閱 <<c4> [ 類型](../../../ado/reference/ado-api/type-property-ado.md)如需詳細資訊。 使用的固定長度資料類型的欄位，傳回值會是資料類型，以位元組為單位的大小。 使用可變長度資料類型的欄位，這是下列其中一項：  
  
1.  以字元為單位的欄位的最大長度 (如**adVarChar**和**adVarWChar**) 或以位元組為單位 (如**adVarBinary**，和**adVarNumeric**) 如果欄位有定義的長度。 例如， **adVarChar(5)** 欄位的最大長度為 5。  
  
2.  以字元為單位的資料類型的最大長度 (如**adChar**和**adWChar**) 或以位元組為單位 (如**adBinary**和**adNumeric**) 如果欄位沒有定義的長度。  
  
3.  ~ 0 (位元，值不是 0，則所有位元會設為 1) 如果不欄位和資料類型已定義的最大長度。  
  
4.  沒有長度的資料類型，這會設定為 ~ 0 (位元，值不是 0，則所有位元會設為 1)。  
  
## <a name="remarks"></a>備註  
 使用**DefinedSize**屬性來判斷的資料容量**欄位**物件。  
  
 **DefinedSize**和[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性不相同。 例如，請考慮**欄位**物件宣告類型為**adVarChar**和**DefinedSize**屬性值為 50，其中包含單一字元。 **ActualSize**它所傳回的屬性值是單一字元的長度以位元組為單位。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 屬性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
