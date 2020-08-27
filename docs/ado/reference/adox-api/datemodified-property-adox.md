---
description: DateModified 屬性 (ADOX)
title: DateModified 屬性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 613dbf829009e4e471844b0d49285817d75316b6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984739"
---
# <a name="datemodified-property-adox"></a>DateModified 屬性 (ADOX)
表示上次修改物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回指定修改日期的 **變數** 值。 如果提供者不支援 **DateModified** ，則此值為 null。  
  
## <a name="remarks"></a>備註  
 新附加的物件的 **DateModified** 屬性為 null。 附加新的[視圖](./view-object-adox.md)或[程式](./procedures-collection-adox.md)之後，您必須呼叫[Views](./views-collection-adox.md)或[Procedure](./procedure-object-adox.md)集合的[Refresh](../ado-api/refresh-method-ado.md)方法，以取得**DateModified**屬性的值。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Procedure 物件 (ADOX)](./procedure-object-adox.md)  
    :::column-end:::
    :::column:::
        [Table 物件 (ADOX)](./table-object-adox.md)  
    :::column-end:::
    :::column:::
        [View 物件 (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [DateCreated 和 DateModified 屬性範例 (VB) ](./datecreated-and-datemodified-properties-example-vb.md)   
 [DateCreated 屬性 (ADOX)](./datecreated-property-adox.md)