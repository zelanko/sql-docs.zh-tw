---
description: Views 集合 (ADOX)
title: Views 集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: rothja
ms.author: jroth
ms.openlocfilehash: a024f21e83a25a82a226428835215a8cba9e21e9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768917"
---
# <a name="views-collection-adox"></a>Views 集合 (ADOX)
包含目錄的所有 [View](./view-object-adox.md) 物件。  
  
## <a name="remarks"></a>備註  
 **Views**集合的[APPEND](./append-method-adox-views.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的視圖新增至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 屬性存取集合中的 view。  
  
-   傳回集合中包含 [Count](../ado-api/count-property-ado.md) 屬性的視圖數目。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法，從集合中移除一個 view。  
  
-   使用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前的資料庫架構。  
  
 本節包含下列主題。  
  
-   [Views 集合屬性、方法和事件](./views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views 和 Fields 集合範例 (VB) ](./views-and-fields-collections-example-vb.md)   
 [Views 附加方法範例 (VB) ](./views-append-method-example-vb.md)   
 [Views 集合、CommandText 屬性範例 (VB) ](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例 (VB) ](./views-delete-method-example-vb.md)   
 [Views Refresh 方法範例 (VB) ](./views-refresh-method-example-vb.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [View 物件 (ADOX)](./view-object-adox.md)