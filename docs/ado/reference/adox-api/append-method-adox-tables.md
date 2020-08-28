---
description: Append 方法 (ADOX Tables)
title: 附加方法 (ADOX 資料表) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: rothja
ms.author: jroth
ms.openlocfilehash: ffd2ef32cae3fafb7179568d1342606d32236657
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985469"
---
# <a name="append-method-adox-tables"></a>Append 方法 (ADOX Tables)
將新的 [資料表](./table-object-adox.md) 物件加入至 [資料表](./tables-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>參數  
 *Table*  
 **Variant**值，包含要附加之**資料表**的參考，或是要建立和附加之資料表的名稱。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援建立資料表，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Tables 集合 (ADOX)](./tables-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](./append-method-adox-procedures.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)