---
title: Append 方法（ADOX Keys） |Microsoft Docs
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
ms.openlocfilehash: fd66edb75bec4f4b7e35c53c9ebeabd9b3c75d83
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967296"
---
# <a name="append-method-adox-keys"></a>Append 方法 (ADOX Keys)
將新的索引[鍵](../../../ado/reference/adox-api/key-object-adox.md)物件加入至索引[鍵](../../../ado/reference/adox-api/keys-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>參數  
 *關鍵*  
 要附加的索引**鍵**物件，或要建立和附加的索引鍵名稱。  
  
 *KeyType*  
 選擇性。 指定索引鍵類型的**Long**值。 *Key*參數會對應至索引**鍵**物件的[Type](../../../ado/reference/adox-api/type-property-key-adox.md)屬性。  
  
 *資料行*  
 選擇性。 **字串**值，指定要編制索引的資料行名稱。 *Columns*參數會對應至資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件的[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性值。  
  
 *RelatedTable*  
 選擇性。 指定相關資料表之名稱的**字串**值。 *RelatedTable*參數會對應到[Table](../../../ado/reference/adox-api/table-object-adox.md)物件的**Name**屬性值。  
  
 *RelatedColumn*  
 選擇性。 **字串**值，指定外鍵之相關資料行的名稱。 *RelatedColumn*參數會對應至資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件的**Name**屬性值。  
  
## <a name="remarks"></a>備註  
 *Columns*參數可以接受資料行的名稱或資料行名稱的陣列。  
  
## <a name="applies-to"></a>套用至  
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX Users）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
