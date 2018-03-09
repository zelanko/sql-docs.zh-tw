---
title: "Append 方法 （ADOX 索引） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00c0f00c1c5de2e049742603c08d323e2978d3fd
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-indexes"></a>Append 方法 （ADOX 索引）
將新[索引](../../../ado/reference/adox-api/index-object-adox.md)物件[索引](../../../ado/reference/adox-api/indexes-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>參數  
 *Index*  
 **索引**来附加物件或建立並附加至索引的名稱。  
  
 *資料行*  
 選擇性。 A **Variant**值，指定要編製索引的資料行的名稱。 *資料行*參數會對應至另一端的[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 *資料行*參數可以採用資料行的名稱或資料行名稱的陣列。  
  
 如果提供者不支援建立索引時，會發生錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引附加方法範例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Append 方法 （ADOX 資料行）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 群組）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引鍵）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 程序）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 資料表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 使用者）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
