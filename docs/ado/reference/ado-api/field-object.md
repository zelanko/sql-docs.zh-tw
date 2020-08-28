---
description: Field 物件
title: Field 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4768281228e39ed8eeb6ffc003e463bf8a53450d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973229"
---
# <a name="field-object"></a>Field 物件
表示具有通用資料類型之資料的資料行。  
  
## <a name="remarks"></a>備註  
 每個 **Field** 物件都會對應到 [記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)的資料行。 您可以使用 [**欄位**物件] 的 [[值](../../../ado/reference/ado-api/value-property-ado.md)] 屬性來設定或傳回目前記錄的資料。 視提供者公開的功能而定，可能無法使用 **欄位** 物件的某些集合、方法或屬性。  
  
 使用 **Field** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   傳回具有 [name](../../../ado/reference/ado-api/name-property-ado.md) 屬性之欄位的名稱。  
  
-   使用 **Value** 屬性來查看或變更欄位中的資料。 **Value** 是 **Field** 物件的預設屬性。  
  
-   傳回具有 [Type](../../../ado/reference/ado-api/type-property-ado.md)、 [Precision](../../../ado/reference/ado-api/precision-property-ado.md)和 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 屬性之欄位的基本特性。  
  
-   傳回具有 [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) 屬性之欄位的宣告大小。  
  
-   使用 [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) 屬性，傳回指定欄位中資料的實際大小。  
  
-   使用 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md) （attribute）和 [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) （property）集合，判斷指定欄位支援哪些類型的功能。  
  
-   使用 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 和 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 方法，操作包含長二進位或長字元資料的欄位值。  
  
-   如果提供者支援批次更新，請使用 [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) 和 [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) 屬性來解決批次更新期間域值的不一致。  
  
 所有的中繼資料屬性 (**Name**、 **Type**、 **DefinedSize**、 **Precision**和 **NumericScale**) 都可以在開啟 **Field** 物件的 **記錄集**之前使用。 在該時間設定這些值對於動態地建立表單相當有用。  
  
 本節包含下列主題。  
  
-   [Field 物件屬性、方法和事件](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的欄位集合 ](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [ (ADO) 的屬性集合 ](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
