---
description: Delete 方法 (ADOX Collections)
title: ) 的 (ADOX 集合刪除方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: rothja
ms.author: jroth
ms.openlocfilehash: f239978dc9d71af81c74de452fefe16efe95d1bf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770627"
---
# <a name="delete-method-adox-collections"></a>Delete 方法 (ADOX Collections)
從集合中移除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **Variant** ，指定要刪除之物件的名稱或序數位置 (索引) 。  
  
## <a name="remarks"></a>備註  
 如果該 *名稱* 不存在於集合中，就會發生錯誤。  
  
 針對 [資料表](./tables-collection-adox.md) 和 [使用者](./users-collection-adox.md) 集合，如果提供者不支援分別刪除資料表或使用者，就會發生錯誤。 若是 [程式](./procedures-collection-adox.md) 和 [Views](./views-collection-adox.md) 集合，如果提供者不支援保存命令， **刪除** 將會失敗。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Columns 集合 (ADOX)](./columns-collection-adox.md)  
        [Groups 集合 (ADOX)](./groups-collection-adox.md)  
        [Indexes 集合 (ADOX)](./indexes-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Keys 集合 (ADOX)](./keys-collection-adox.md)  
        [Procedures 集合 (ADOX)](./procedures-collection-adox.md)  
        [Tables 集合 (ADOX)](./tables-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Users 集合 (ADOX)](./users-collection-adox.md)  
        [Views 集合 (ADOX)](./views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [程式 Delete 方法範例 (VB) ](./procedures-delete-method-example-vb.md)   
 [Views Delete 方法範例 (VB)](./views-delete-method-example-vb.md)