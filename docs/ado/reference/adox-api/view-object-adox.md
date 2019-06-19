---
title: 檢視物件 (ADOX) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d87b56716ed1876acc6ac139e7804036d5cdfb86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718807"
---
# <a name="view-object-adox"></a>View 物件 (ADOX)
代表已篩選的一份記錄或一份虛擬資料表。 當搭配 ADO[命令](../../../ado/reference/ado-api/command-object-ado.md)物件，**檢視**物件可以用於加入、 刪除或修改檢視。  
  
## <a name="remarks"></a>備註  
 檢視是從其他資料庫資料表或檢視表建立的虛擬資料表。 **檢視**物件可讓您建立的檢視，而不需要知道或使用提供者的 「 建立檢視 」 語法。  
  
 內容一起**檢視**物件時，您可以：  
  
-   識別與檢視[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   指定 ADO**命令**可用來新增、 刪除或修改與檢視的物件[命令](../../../ado/reference/adox-api/command-property-adox.md)屬性。  
  
-   傳回日期資訊[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)並[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性。  
  
 本章節包含下列主題。  
  
-   [View 物件屬性、方法和事件](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [檢視和 Fields 集合範例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、 CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
