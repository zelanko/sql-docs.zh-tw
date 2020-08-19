---
description: Append 方法 (ADOX Tables)
title: 附加方法 (ADOX 資料表) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 6069b3d99e021be01d8fd2d724b7c25868167bd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440470"
---
# <a name="append-method-adox-tables"></a>Append 方法 (ADOX Tables)
將新的 [資料表](../../../ado/reference/adox-api/table-object-adox.md) 物件加入至 [資料表](../../../ado/reference/adox-api/tables-collection-adox.md) 集合。  
  
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
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [ (ADOX 使用者的 Append 方法) ](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
