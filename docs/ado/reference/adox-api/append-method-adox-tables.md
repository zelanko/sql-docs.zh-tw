---
title: Append 方法（ADOX Tables） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8c16ac4d18806b670c8b3e27dc09c9019d7ecdeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967243"
---
# <a name="append-method-adox-tables"></a>Append 方法 (ADOX Tables)
將新的[資料表](../../../ado/reference/adox-api/table-object-adox.md)物件加入至[Tables](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>參數  
 *Table*  
 **Variant**值，其中包含要附加之**資料表**的參考，或要建立和附加之資料表的名稱。  
  
## <a name="remarks"></a>備註  
 如果提供者不支援建立資料表，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [ParentCatalog 屬性範例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Users）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
