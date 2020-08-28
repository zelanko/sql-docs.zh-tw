---
description: Count 屬性 (ADO)
title: Count 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: rothja
ms.author: jroth
ms.openlocfilehash: b478a9f88d33503c5eda98bda11cfe0e0fcc8d6b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974519"
---
# <a name="count-property-ado"></a>Count 屬性 (ADO)
表示集合中的物件數目。  
  
## <a name="return-value"></a>傳回值  
 傳回 **Long** 值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **Count** 屬性來判斷指定集合中有多少個物件。  
  
 因為集合的成員編號開頭為零，所以您應該一律以零成員開頭的程式碼迴圈，並以 **Count** 屬性的值減1。 如果您使用 Microsoft Visual Basic，而且想要在不檢查 **Count** 屬性的情況下，對集合的成員執行迴圈，請使用 **For Each .。。下一個** 命令。  
  
 如果 **Count** 屬性為零，則集合中沒有任何物件。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Axes 集合 (ADO MD)](../ado-md-api/axes-collection-ado-md.md)  
        [Columns 集合 (ADOX)](../adox-api/columns-collection-adox.md)  
        [CubeDefs 集合 (ADO MD)](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions 集合 (ADO MD)](../ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 集合 (ADO)](./errors-collection-ado.md)  
        [Fields 集合 (ADO)](./fields-collection-ado.md)  
        [Groups 集合 (ADOX)](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies 集合 (ADO MD)](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 集合 (ADOX)](../adox-api/indexes-collection-adox.md)  
        [Keys 集合 (ADOX)](../adox-api/keys-collection-adox.md)  
        [Levels 集合 (ADO MD)](../ado-md-api/levels-collection-ado-md.md)  
        [Members 集合 (ADO MD)](../ado-md-api/members-collection-ado-md.md)  
        [Parameters 集合 (ADO)](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions 集合 (ADO MD)](../ado-md-api/positions-collection-ado-md.md)  
        [Procedures 集合 (ADOX)](../adox-api/procedures-collection-adox.md)  
        [Properties 集合 (ADO)](./properties-collection-ado.md)  
        [Tables 集合 (ADOX)](../adox-api/tables-collection-adox.md)  
        [Users 集合 (ADOX)](../adox-api/users-collection-adox.md)  
        [Views 集合 (ADOX)](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Count 屬性範例 (VB) ](./count-property-example-vb.md)   
 [Count 屬性範例 (VC + +) ](./count-property-example-vc.md)   
 [Refresh 方法 (ADO)](./refresh-method-ado.md)