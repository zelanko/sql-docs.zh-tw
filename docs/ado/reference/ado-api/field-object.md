---
title: 欄位物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 04dbf3069896b9a7668d64a2f1d322f0b17ca5f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918678"
---
# <a name="field-object"></a>Field 物件
代表具有通用的資料類型的資料行。  
  
## <a name="remarks"></a>備註  
 每個**欄位**物件中的資料行對應[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 您使用[值](../../../ado/reference/ado-api/value-property-ado.md)屬性**欄位**設定或傳回目前的記錄資料的物件。 某些集合、 方法或屬性會提供者依據其功能的公開**欄位**物件可能無法使用。  
  
 使用集合、 方法和屬性的**欄位**物件時，您可以執行下列動作：  
  
-   傳回的欄位名稱[名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性。  
  
-   檢視或變更的欄位中的資料**值**屬性。 **值**是預設屬性**欄位**物件。  
  
-   傳回欄位的基本特性[型別](../../../ado/reference/ado-api/type-property-ado.md)，[有效位數](../../../ado/reference/ado-api/precision-property-ado.md)，並[NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md)屬性。  
  
-   傳回具有欄位宣告的大小[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)屬性。  
  
-   使用指定的欄位中傳回資料的實際大小[ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)屬性。  
  
-   判斷指定的欄位，以支援何種類型的功能[屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性並[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
-   管理包含長的二進位或長度字元資料欄位的值[AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)並[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)方法。  
  
-   如果提供者支援批次更新，批次更新期間，解決欄位值不一致的地方[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)並[UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)屬性。  
  
 所有中繼資料屬性 (**名稱**，**型別**， **DefinedSize**，**精確度**，和**NumericScale**) 可用開始前**欄位**物件的**資料錄集**。 在該時間設定它們適合用來以動態方式建構表單。  
  
 本章節包含下列主題。  
  
-   [Field 物件屬性、 方法和事件](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
