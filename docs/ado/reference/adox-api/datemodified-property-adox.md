---
title: "DateModified 屬性 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f76f2f250ae7a40cdb2184ce29c5e20772f7ccaf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="datemodified-property-adox"></a>DateModified 屬性 (ADOX)
指出上次修改物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回**Variant**值，指定 修改日期。 此值為 null 如果**DateModified**提供者不支援。  
  
## <a name="remarks"></a>備註  
 **DateModified**屬性為 null，新附加的物件。 附加新之後[檢視](../../../ado/reference/adox-api/view-object-adox.md)或[程序](../../../ado/reference/adox-api/procedure-object-adox.md)，您必須呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法[檢視](../../../ado/reference/adox-api/views-collection-adox.md)或[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)要取得的值集合**DateModified**屬性。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[程序物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[檢視物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 屬性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)

