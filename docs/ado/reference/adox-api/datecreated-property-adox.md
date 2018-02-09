---
title: "DateCreated 屬性 (ADOX) |Microsoft 文件"
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
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7f405958cdd28e6dd4ae285c29ce806c2a61074
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="datecreated-property-adox"></a>DateCreated 屬性 (ADOX)
指出物件已建立的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回**Variant**值，指定建立的日期。 此值為 null 如果**DateCreated**提供者不支援。  
  
## <a name="remarks"></a>備註  
 **DateCreated**屬性為 null，新附加的物件。 附加新之後[檢視](../../../ado/reference/adox-api/view-object-adox.md)或[程序](../../../ado/reference/adox-api/procedure-object-adox.md)，您必須呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法[檢視](../../../ado/reference/adox-api/views-collection-adox.md)或[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)要取得的值集合**DateCreated**屬性。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 屬性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
