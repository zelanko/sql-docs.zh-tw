---
description: DateCreated 屬性 (ADOX)
title: DateCreated 屬性 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae2c0fcfdc164906f0216abb45f98f705de9cd4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770737"
---
# <a name="datecreated-property-adox"></a>DateCreated 屬性 (ADOX)
指出建立物件的日期。  
  
## <a name="return-values"></a>傳回值  
 傳回 **Variant** 值，指定建立的日期。 如果提供者不支援 **DateCreated** ，則此值為 null。  
  
## <a name="remarks"></a>備註  
 新附加的物件的 **DateCreated** 屬性為 null。 附加新的[視圖](./view-object-adox.md)或[程式](./procedures-collection-adox.md)之後，您必須呼叫[Views](./views-collection-adox.md)或[Procedure](./procedure-object-adox.md)集合的[Refresh](../ado-api/refresh-method-ado.md)方法，以取得**DateCreated**屬性的值。  
  
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
 [DateModified 屬性 (ADOX)](./datemodified-property-adox.md)