---
description: Property 物件 (ADOX)
title: 屬性物件 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a836b5b0778aea77732036d1951db81aa790198
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439600"
---
# <a name="property-object-adox"></a>Property 物件 (ADOX)
表示 ADOX 物件的特性。  
  
## <a name="remarks"></a>備註  
 ADOX 物件有兩種類型的屬性：內建和動態。  
  
 內建屬性是使用 MyObject 語法，立即可供任何新物件使用的屬性。 它們不會在物件的 [屬性集合](../../../ado/reference/ado-api/properties-collection-ado.md)中顯示為屬性物件，因此雖然您可以變更其值，但無法修改其特性。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADOX 物件的 Properties 集合中。  只能透過集合參考動態屬性，使用 MyObject 的屬性 (0) 或 MyObject ( "Name" ) 語法。  
  
 您無法刪除任一種類型的屬性。  
  
 動態屬性物件有四個內建的屬性：  
  
 [Name](../../../ado/reference/ado-api/name-property-ado.md)屬性是識別屬性的字串。  
  
 [Type](../../../ado/reference/ado-api/type-property-ado.md)屬性是指定屬性資料類型的整數。  
  
 [Value](../../../ado/reference/ado-api/value-property-ado.md)屬性是包含屬性設定的變數。 Value 是屬性物件的預設屬性。  
  
 [屬性](../../../ado/reference/ado-api/attributes-property-ado.md)（attribute）屬性（attribute）是 long 值，指出提供者特定屬性的特性。  
  
 本節包含下列主題。  
  
-   [ADOX Property 物件屬性、方法和事件](../../../ado/reference/adox-api/adox-property-object-properties-methods-and-events.md)
