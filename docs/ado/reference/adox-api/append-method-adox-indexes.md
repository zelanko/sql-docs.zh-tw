---
title: Append 方法 (ADOX Indexes) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7190fa68b8204e6b1cfea68a6571e07fd78a9bbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718954"
---
# <a name="append-method-adox-indexes"></a>Append 方法 (ADOX Indexes)
加入新[Index](../../../ado/reference/adox-api/index-object-adox.md)物件[索引](../../../ado/reference/adox-api/indexes-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 **Index**来附加的物件或建立並附加至索引的名稱。  
  
 *資料行*  
 選擇性。 A **Variant**值，指定要編製索引之資料行的名稱。 *資料行*參數的值對應於[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 *資料行*參數可以接受的資料行名稱，或是資料行名稱的陣列。  
  
 如果提供者不支援建立索引時，會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Indexes Append 方法範例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
