---
title: Append 方法（ADOX 索引） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: rothja
ms.author: jroth
ms.openlocfilehash: 6996f3a0a3ad9f2ffa727a6cbd7b48d3fbf32777
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764059"
---
# <a name="append-method-adox-indexes"></a>Append 方法 (ADOX Indexes)
將新的[索引](../../../ado/reference/adox-api/index-object-adox.md)物件加入至[索引](../../../ado/reference/adox-api/indexes-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>參數  
 *索引*  
 要附加的**索引**物件，或要建立和附加之索引的名稱。  
  
 *資料行*  
 選擇性。 **Variant**值，指定要編制索引之資料行的名稱。 *Columns*參數會對應至資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件之[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性的值。  
  
## <a name="remarks"></a>備註  
 *Columns*參數可以接受資料行的名稱或資料行名稱的陣列。  
  
 如果提供者不支援建立索引，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引附加方法範例（VB）](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX Users）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
