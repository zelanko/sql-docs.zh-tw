---
title: View 物件（ADOX） |Microsoft Docs
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
ms.openlocfilehash: b468ccc3edc4cc5453b4f08371cd2b4b962f0c72
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753187"
---
# <a name="view-object-adox"></a>View 物件 (ADOX)
表示一組已篩選的記錄或虛擬資料表。 搭配 ADO [Command](../../../ado/reference/ado-api/command-object-ado.md)物件使用時， **View**物件可以用來新增、刪除或修改 views。  
  
## <a name="remarks"></a>備註  
 View 是從其他資料庫資料表或 views 建立的虛擬資料表。 **View**物件可讓您建立視圖，而不需要知道或使用提供者的「建立視圖」語法。  
  
 使用**View**物件的屬性，您可以：  
  
-   使用[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性來識別此視圖。  
  
-   指定可以用來新增、刪除或修改具有[命令](../../../ado/reference/adox-api/command-property-adox.md)屬性之 VIEWS 的 ADO**命令**物件。  
  
-   傳回具有[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性的日期資訊。  
  
 本章節包含下列主題。  
  
-   [View 物件屬性、方法和事件](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Views 和 Fields 集合範例（VB）](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 方法範例（VB）](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、CommandText 屬性範例（VB）](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例（VB）](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
