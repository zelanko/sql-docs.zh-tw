---
title: 屬性物件 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Property
helpviewer_keywords:
- Property object [ADO]
ms.assetid: b2a4767c-03c7-4935-a3bc-df3e1a38a009
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b646b698f8d14e6440368dbffb6e472360c2832d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="property-object-ado"></a>屬性物件 (ADO)
代表動態 ADO 物件提供者所定義的特性。  
  
## <a name="remarks"></a>備註  
 ADO 物件有兩種類型的屬性： 內建和動態。  
  
 內建屬性是在 ADO 中實作並立即提供給任何這些屬性新物件，使用`MyObject.Property`語法。 它們不會顯示成**屬性**物件中的物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，因此您可以變更其值，雖然您無法修改它們的特性。  
  
 動態屬性是由定義基礎資料提供者，而會出現在**屬性**適當 ADO 物件的集合。 例如，提供者特定的屬性可能表示如果[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件支援交易，或更新。 這些額外的屬性會顯示為**屬性**中的物件**資料錄集**物件的**屬性**集合。 動態屬性可以參考集合中，只能透過使用`MyObject.Properties(0)`或`MyObject.Properties("Name")`語法。  
  
 您無法刪除任何一種屬性。  
  
 動態**屬性**物件都有自己的四個內建屬性：  
  
-   [名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性是一個字串，識別屬性。  
  
-   [類型](../../../ado/reference/ado-api/type-property-ado.md)屬性是整數，指定屬性資料型別。  
  
-   [值](../../../ado/reference/ado-api/value-property-ado.md)屬性是包含的屬性設定為 variant。 **值**是預設屬性**屬性**物件。  
  
-   [屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性是長值，指出提供者特定屬性的特性。  
  
 本章節包含下列主題。  
  
-   [屬性的物件屬性、 方法和事件](../../../ado/reference/ado-api/property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Field 物件](../../../ado/reference/ado-api/field-object.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
