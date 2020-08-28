---
description: Property 物件 (ADO)
title: " (ADO) 的屬性物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7edc57495968cb94dbf8714e3b519acac578775f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989979"
---
# <a name="property-object-ado"></a>Property 物件 (ADO)
代表提供者所定義之 ADO 物件的動態特性。  
  
## <a name="remarks"></a>備註  
 ADO 物件有兩種類型的屬性：內建和動態。  
  
 內建屬性是在 ADO 中執行的屬性，而且可以使用語法立即提供給任何新的物件使用 `MyObject.Property` 。 它們不會在物件的[屬性](./properties-collection-ado.md)集合中顯示為**屬性**物件，因此雖然您可以變更其值，但無法修改其特性。  
  
 動態屬性是由基礎資料提供者所定義，而且會出現在適當 ADO 物件的 **properties** 集合中。 例如，提供者特定的屬性可能會指出 [記錄集](./recordset-object-ado.md) 物件是否支援交易或更新。 這些額外的屬性會在該**記錄集**物件的**properties**集合中顯示為**屬性**物件。 您只能使用或語法，透過集合參考動態屬性 `MyObject.Properties(0)` `MyObject.Properties("Name")` 。  
  
 您無法刪除任一種類型的屬性。  
  
 動態 **屬性** 物件有四個內建的屬性：  
  
-   [Name](./name-property-ado.md)屬性是識別屬性的字串。  
  
-   [Type](./type-property-ado.md)屬性是指定屬性資料類型的整數。  
  
-   [Value](./value-property-ado.md)屬性是包含屬性設定的變數。 **Value** 是 **屬性** 物件的預設屬性。  
  
-   [屬性](./attributes-property-ado.md)（attribute）屬性（attribute）是 long 值，指出提供者特定屬性的特性。  
  
 本節包含下列主題。  
  
-   [Property 物件屬性、方法和事件](./property-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的命令物件 ](./command-object-ado.md)   
 [ (ADO) 的 Connection 物件 ](./connection-object-ado.md)   
 [Field 物件](./field-object.md)   
 [ (ADO) 的屬性集合 ](./properties-collection-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)