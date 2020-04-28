---
title: Property 物件（ADOX） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965390"
---
# <a name="property-object-adox"></a>Property 物件 (ADOX)
表示 ADOX 物件的特性。  
  
## <a name="remarks"></a>備註  
 ADOX 物件有兩種類型的屬性：內建和動態。  
  
 內建屬性是任何新物件立即可用的屬性，其方式是使用 MyObject. Property 語法。 它們不會在物件的[Properties 集合](../../../ado/reference/ado-api/properties-collection-ado.md)中顯示為屬性物件，因此，雖然您可以變更其值，但無法修改其特性。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADOX 物件的 Properties 集合中。  動態屬性只能透過集合參考，使用 MyObject. Properties （0）或 MyObject （"Name"）語法。  
  
 您不能刪除任何一種屬性。  
  
 動態屬性物件有四個本身的內建屬性：  
  
 [Name](../../../ado/reference/ado-api/name-property-ado.md)屬性是可識別屬性的字串。  
  
 [Type](../../../ado/reference/ado-api/type-property-ado.md)屬性是指定屬性資料類型的整數。  
  
 [Value](../../../ado/reference/ado-api/value-property-ado.md)屬性是包含屬性設定的 variant。 Value 是屬性物件的預設屬性。  
  
 [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md)屬性是 long 值，指出提供者特定屬性的特性。  
  
 本章節包含下列主題。  
  
-   [ADOX Property 物件屬性、方法和事件](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
