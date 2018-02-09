---
title: "檢視物件 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: af414c302459f093441f5f0f3fd0e60c1a95d973
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="view-object-adox"></a>檢視物件 (ADOX)
代表已篩選的一組記錄或一份虛擬資料表。 使用 ADO 搭配使用時[命令](../../../ado/reference/ado-api/command-object-ado.md)物件**檢視**物件可用於加入、 刪除或修改檢視。  
  
## <a name="remarks"></a>備註  
 檢視是從其他資料庫資料表或檢視表建立的虛擬資料表。 **檢視**物件可讓您建立的檢視，而不需要知道或使用提供者的 「 建立檢視表 」 語法。  
  
 內容**檢視**物件，您可以：  
  
-   識別與檢視[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   指定 ADO**命令**物件，可用來新增、 刪除或修改與檢視[命令](../../../ado/reference/adox-api/command-property-adox.md)屬性。  
  
-   傳回日期資訊與[DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性。  
  
 本章節包含下列主題。  
  
-   [View 物件屬性、方法和事件](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [檢視和欄位集合範例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [檢視附加方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [檢視集合，CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [檢視刪除方法的範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
