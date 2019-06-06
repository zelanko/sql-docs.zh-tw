---
title: DateModified 屬性 (ADOX) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 5d0cd8a6196bdc0f933470a52dbb3567f64df05e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718917"
---
# <a name="datemodified-property-adox"></a>DateModified 屬性 (ADOX)
表示上次修改物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回**Variant**值，指定修改的日期。 此值為 null 如果**DateModified**提供者不支援。  
  
## <a name="remarks"></a>備註  
 **DateModified**屬性為 null，新附加的物件。 之後附加新[檢視](../../../ado/reference/adox-api/view-object-adox.md)或是[程序](../../../ado/reference/adox-api/procedure-object-adox.md)，您必須呼叫[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法[檢視](../../../ado/reference/adox-api/views-collection-adox.md)或[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)以取得值的集合**DateModified**屬性。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例 (VB)](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 屬性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)
