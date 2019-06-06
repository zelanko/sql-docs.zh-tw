---
title: Append 方法 (ADOX Keys) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ea4e06fa790e8a360cfb1254b3064b3b540e7842
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708343"
---
# <a name="append-method-adox-keys"></a>Append 方法 (ADOX Keys)
加入新[金鑰](../../../ado/reference/adox-api/key-object-adox.md)物件[金鑰](../../../ado/reference/adox-api/keys-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>參數  
 *索引鍵*  
 **金鑰**来附加的物件或建立並附加索引鍵的名稱。  
  
 *KeyType*  
 選擇性。 A**長**值，指定索引鍵的類型。 *金鑰*參數會對應至[型別](../../../ado/reference/adox-api/type-property-key-adox.md)屬性**金鑰**物件。  
  
 *資料行*  
 選擇性。 A**字串**值，指定要編製索引的資料行名稱。 *資料行*參數的值會對應[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
 *RelatedTable*  
 選擇性。 A**字串**值，指定相關的資料表名稱。 *RelatedTable*參數的值會對應**名稱**屬性[表格](../../../ado/reference/adox-api/table-object-adox.md)物件。  
  
 *RelatedColumn*  
 選擇性。 A**字串**值，指定外部索引鍵相關的資料行的名稱。 *RelatedColumn*參數的值會對應**名稱**屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 *資料行*參數可以接受的資料行名稱，或是資料行名稱的陣列。  
  
## <a name="applies-to"></a>適用於  
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Users)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
