---
description: DefinedSize 屬性
title: DefinedSize 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 35330c6cae4a3450d4a970edddf360296ce33148
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974149"
---
# <a name="definedsize-property"></a>DefinedSize 屬性
表示 [Field](../../../ado/reference/ado-api/field-object.md) 物件的資料容量。  
  
## <a name="return-value"></a>傳回值  
 傳回 **Long** 值，反映欄位所定義的大小，這取決於 field 物件的資料類型;如需詳細資訊，請參閱 [類型](../../../ado/reference/ado-api/type-property-ado.md) 。 如果欄位使用固定長度的資料類型，則傳回值為資料類型的大小（以位元組為單位）。 針對使用可變長度資料類型的欄位，這是下列其中一項：  
  
1.  **AdVarChar**和) **adVarWChar**的字元 (的最大長度（以字元為單位）、 **adVarBinary**的位元組 (，以及如果欄位具有已定義的長度，則為**adVarNumeric**) 。 例如， **adVarChar (5) ** 欄位的最大長度為5。  
  
2.  **AdChar**和**adWChar**) 的資料類型最大長度（以字元為單位） (（如果欄位沒有定義的長度，則為**adBinary**和**adNumeric**) 的位元組 (）。  
  
3.  ~ 0 (位，值不是 0;如果欄位和資料類型都沒有定義的最大長度，則所有位都會設為 1) 。  
  
4.  針對沒有長度的資料類型，這會設定為 ~ 0 (位，該值不是 0;所有位都設定為 1) 。  
  
## <a name="remarks"></a>備註  
 您可以使用 **DefinedSize** 屬性來判斷 **Field** 物件的資料容量。  
  
 **DefinedSize**和[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性不同。 例如，假設有一個 **Field** 物件，其宣告的型別為 **AdVarChar** ，而 **DefinedSize** 屬性值為50，其中包含單一字元。 它所傳回的 **ActualSize** 屬性值是單一字元的長度（以位元組為單位）。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB) ](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 (VC + +) ](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [ActualSize 屬性 (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
