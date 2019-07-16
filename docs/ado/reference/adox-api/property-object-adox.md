---
title: Property 物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Property object [ADOX]
ms.assetid: 6a56def6-dbe6-4ccc-a491-8d076889f019
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7911608970e9860d7eddcf3e83156ac99645c3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965390"
---
# <a name="property-object-adox"></a>Property 物件 (ADOX)
表示 ADOX 物件的特性。  
  
## <a name="remarks"></a>備註  
 ADOX 物件有兩種類型的屬性： 內建和動態。  
  
 內建的屬性是立即提供給任何新的物件，使用 MyObject.Property 語法這些屬性。 它們不會出現為物件的屬性物件[屬性集合](../../../ado/reference/ado-api/properties-collection-ado.md)，因此，雖然您可以變更其值，您無法修改它們的特性。  
  
 動態屬性由基礎資料提供者所定義，並會出現在適當的 ADOX 物件的屬性集合。  動態屬性可以參考只能透過使用 MyObject.Properties(0) 或 MyObject.Properties("Name") 語法的集合。  
  
 您無法刪除屬性的其中一種。  
  
 屬性的動態物件有四個內建自己的屬性：  
  
 [名稱](../../../ado/reference/ado-api/name-property-ado.md)屬性是字串，識別屬性。  
  
 [型別](../../../ado/reference/ado-api/type-property-ado.md)屬性是一個整數，指定屬性資料型別。  
  
 [值](../../../ado/reference/ado-api/value-property-ado.md)屬性是變化，其中包含的屬性設定。 屬性物件的預設屬性值。  
  
 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md)屬性是很長的值，指出屬性提供者特有的特性。  
  
 本章節包含下列主題。  
  
-   [ADOX Property 物件屬性、方法和事件](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
