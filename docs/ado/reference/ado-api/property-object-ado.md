---
title: Property 物件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: af077c1606148eacb4f93ba6cfb52c3bb5eeefce
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702951"
---
# <a name="property-object-ado"></a>Property 物件 (ADO)
表示提供者會定義於 ADO 物件的動態特性。  
  
## <a name="remarks"></a>備註  
 ADO 物件有兩種類型的屬性： 內建和動態。  
  
 內建屬性可讓您為這些屬性，在 ADO 中實作和立即提供給任何新物件，使用`MyObject.Property`語法。 它們不會出現**屬性**物件中的物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，因此雖然您可以變更其值，您無法修改它們的特性。  
  
 動態屬性由基礎資料提供者所定義，並會出現在**屬性**適當的 ADO 物件的集合。 例如，提供者特有的屬性可能表示如果[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件支援交易，或更新。 這些額外的屬性會成為**屬性**中的物件**Recordset**物件的**屬性**集合。 動態屬性可以參考只能透過集合中，使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`語法。  
  
 您無法刪除屬性的其中一種。  
  
 動態**屬性**物件都有自己的四個內建的屬性：  
  
-   [名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性是字串，識別屬性。  
  
-   [型別](../../../ado/reference/ado-api/type-property-ado.md)屬性是一個整數，指定屬性資料型別。  
  
-   [值](../../../ado/reference/ado-api/value-property-ado.md)屬性是變化，其中包含的屬性設定。 **值**是預設屬性，如**屬性**物件。  
  
-   [屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性是很長的值，指出屬性提供者特有的特性。  
  
 本章節包含下列主題。  
  
-   [Property 物件屬性、 方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
