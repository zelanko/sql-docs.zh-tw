---
description: Indexes 集合 (ADOX)
title: " (ADOX) 的索引集合 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: 916671fdf9722c7894ee122f3d68167a8047b72c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439910"
---
# <a name="indexes-collection-adox"></a>Indexes 集合 (ADOX)
包含資料表的所有 [索引](../../../ado/reference/adox-api/index-object-adox.md) 物件。  
  
## <a name="remarks"></a>備註  
 針對 ADOX，**索引**集合的[Append](../../../ado/reference/adox-api/append-method-adox-indexes.md)方法是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的索引加入至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 屬性存取集合中的索引。  
  
-   傳回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 屬性的索引數目。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法，從集合中移除索引。  
  
-   使用 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前的資料庫架構。  
  
 本節包含下列主題。  
  
-   [Indexes 集合屬性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的索引附加方法範例) ](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
