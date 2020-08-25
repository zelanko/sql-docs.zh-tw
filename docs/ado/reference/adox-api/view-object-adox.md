---
description: View 物件 (ADOX)
title: View Object (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: rothja
ms.author: jroth
ms.openlocfilehash: b84873da0c4cacc12d624763b466786eaf1532ae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769017"
---
# <a name="view-object-adox"></a>View 物件 (ADOX)
表示已篩選的一組記錄或虛擬資料表。 當與 ADO [命令](../ado-api/command-object-ado.md) 物件一起使用時， **View** 物件可以用來加入、刪除或修改視圖。  
  
## <a name="remarks"></a>備註  
 View 是從其他資料庫資料表或視圖建立的虛擬資料表。 **View**物件可讓您建立視圖，而不需要知道或使用提供者的「建立視圖」語法。  
  
 使用 **View** 物件的屬性，您可以：  
  
-   識別具有 [Name](./name-property-adox.md) 屬性的視圖。  
  
-   指定可以用來新增、刪除或使用[命令](./command-property-adox.md)屬性來修改視圖的 ADO**命令**物件。  
  
-   傳回具有 [DateCreated](./datecreated-property-adox.md) 和 [DateModified](./datemodified-property-adox.md) 屬性的日期資訊。  
  
 本節包含下列主題。  
  
-   [View 物件屬性、方法和事件](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views 和 Fields 集合範例 (VB) ](./views-and-fields-collections-example-vb.md)   
 [Views 附加方法範例 (VB) ](./views-append-method-example-vb.md)   
 [Views 集合、CommandText 屬性範例 (VB) ](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例 (VB) ](./views-delete-method-example-vb.md)   
 [Views 集合 (ADOX)](./views-collection-adox.md)