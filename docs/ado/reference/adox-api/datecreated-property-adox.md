---
title: DateCreated 屬性（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::get_DateCreated
- _Table::DateCreated
- _Table::GetDateCreated
helpviewer_keywords:
- DateCreated property [ADOX]
ms.assetid: 2bf4b00d-045c-444e-8af7-8af6297ed418
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0151b6388a19fc95227cbfa55a571e0a797d0acc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966578"
---
# <a name="datecreated-property-adox"></a>DateCreated 屬性 (ADOX)
表示建立物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回指定建立日期的**Variant**值。 如果提供者不支援**DateCreated** ，則此值為 null。  
  
## <a name="remarks"></a>備註  
 新附加之物件的**DateCreated**屬性為 null。 附加新的[視圖](../../../ado/reference/adox-api/view-object-adox.md)或[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)之後，您必須呼叫[Views](../../../ado/reference/adox-api/views-collection-adox.md)或[Procedure](../../../ado/reference/adox-api/procedure-object-adox.md)集合的[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法，才能取得**DateCreated**屬性的值。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例（VB）](../../../ado/reference/adox-api/datecreated-and-datemodified-properties-example-vb.md)   
 [DateModified 屬性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)
