---
title: "Append 方法 （ADOX 索引鍵） |Microsoft 文件"
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
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d1f8938adf51ee1f38de29b85753095d55d7703
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="append-method-adox-keys"></a>Append 方法 （ADOX 索引鍵）
將新[金鑰](../../../ado/reference/adox-api/key-object-adox.md)物件[金鑰](../../../ado/reference/adox-api/keys-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>參數  
 *索引鍵*  
 **金鑰**来附加物件或建立並附加至索引鍵的名稱。  
  
 *KeyType*  
 選擇性。 A**長**值，指定索引鍵的類型。 *金鑰*參數會對應至[類型](../../../ado/reference/adox-api/type-property-key-adox.md)屬性**金鑰**物件。  
  
 *[資料行]*  
 選擇性。 A**字串**值，指定要編製索引的資料行名稱。 *資料行*參數對應至值[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
 *RelatedTable*  
 選擇性。 A**字串**值，指定相關資料表的名稱。 *RelatedTable*參數對應至值**名稱**屬性[資料表](../../../ado/reference/adox-api/table-object-adox.md)物件。  
  
 *RelatedColumn*  
 選擇性。 A**字串**值，指定外部索引鍵相關的資料行的名稱。 *RelatedColumn*參數對應至值**名稱**屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 *資料行*參數可以採用資料行的名稱或資料行名稱的陣列。  
  
## <a name="applies-to"></a>適用於  
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 方法 （ADOX 資料行）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 群組）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 程序）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 資料表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 使用者）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
