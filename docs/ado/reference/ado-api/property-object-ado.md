---
title: Property 物件（ADO） |Microsoft Docs
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
ms.openlocfilehash: 43bfa816a9ca8a93cdc1188a98e54d3e0d9111b1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917548"
---
# <a name="property-object-ado"></a>Property 物件 (ADO)
表示由提供者定義之 ADO 物件的動態特性。  
  
## <a name="remarks"></a>備註  
 ADO 物件有兩種屬性類型：內建和動態。  
  
 內建屬性是在 ADO 中實和使用`MyObject.Property`語法立即提供給任何新物件的屬性。 它們不會在物件的[Properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合中顯示為**屬性**物件，因此，雖然您可以變更其值，但無法修改其特性。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADO 物件的**properties**集合中。 例如，提供者特定的屬性可能會指出[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是否支援交易或更新。 這些額外的屬性會以**屬性**物件的形式顯示在該**記錄集**物件的**properties**集合中。 只能透過集合使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`語法來參考動態屬性。  
  
 您不能刪除任何一種屬性。  
  
 動態**屬性**物件有四個本身的內建屬性：  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md)屬性是可識別屬性的字串。  
  
-   [Type](../../../ado/reference/ado-api/type-property-ado.md)屬性是指定屬性資料類型的整數。  
  
-   [Value](../../../ado/reference/ado-api/value-property-ado.md)屬性是包含屬性設定的 variant。 **Value**是**屬性**物件的預設屬性。  
  
-   [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性是 long 值，指出提供者特定屬性的特性。  
  
 本章節包含下列主題。  
  
-   [Property 物件屬性、方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
