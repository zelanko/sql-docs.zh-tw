---
title: DateModified 屬性（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateModified
- _Table::DateModified
- _Table::GetDateModified
helpviewer_keywords:
- DateModified property [ADOX]
ms.assetid: fed09266-1547-4bda-9088-c254d81cc738
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc41c630b8201651e933f5d6538e6887e7933c95
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966509"
---
# <a name="datemodified-property-adox"></a>DateModified 屬性 (ADOX)
表示上次修改物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回指定修改日期的**Variant**值。 如果提供者不支援**DateModified** ，則此值為 null。  
  
## <a name="remarks"></a>備註  
 新附加之物件的**DateModified**屬性為 null。 附加新的[視圖](../../../ado/reference/adox-api/view-object-adox.md)或[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)之後，您必須呼叫[Views](../../../ado/reference/adox-api/views-collection-adox.md)或[Procedure](../../../ado/reference/adox-api/procedure-object-adox.md)集合的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，才能取得**DateModified**屬性的值。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例（VB）](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 屬性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
