---
description: Keys 集合 (ADOX)
title: 金鑰集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 95d1b5b927f03a0592f25cc4cc79c0ffe78cee74
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770057"
---
# <a name="keys-collection-adox"></a>Keys 集合 (ADOX)
包含[資料表](./table-object-adox.md)的所有索引[鍵](./key-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 索引[鍵集合]()的[APPEND](./append-method-adox-keys.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 [Append](./append-method-adox-keys.md) 方法將新的索引鍵新增至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 屬性存取集合中的索引鍵。  
  
-   傳回包含在集合中的索引鍵數目與 [Count](../ado-api/count-property-ado.md) 屬性。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法，從集合中移除索引鍵。  
  
-   使用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前資料庫的架構。  
  
 本節包含下列主題。  
  
-   [Indexes 集合屬性、方法和事件](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Keys 集合屬性、方法和事件](./keys-collection-properties-methods-and-events.md)   
 [Key 物件 (ADOX)](./key-object-adox.md)