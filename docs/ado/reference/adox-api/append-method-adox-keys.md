---
description: Append 方法 (ADOX Keys)
title: 附加方法 (ADOX 索引鍵) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2531031808c16db4892fb0b759a8a8d819a2222d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985479"
---
# <a name="append-method-adox-keys"></a>Append 方法 (ADOX Keys)
將新的索引 [鍵](./key-object-adox.md) 物件加入至索引 [鍵](./keys-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>參數  
 *索引鍵*  
 要附加的索引 **鍵** 物件，或是要建立和附加的索引鍵名稱。  
  
 *KeyType*  
 選擇性。 指定索引鍵類型的 **Long** 值。 *Key*參數對應到**Key**物件的[Type](./type-property-key-adox.md)屬性。  
  
 *資料行*  
 選擇性。 指定要編制索引之資料行名稱的 **字串** 值。 *Columns*參數會對應到資料[行](./column-object-adox.md)物件的[Name](./name-property-adox.md)屬性值。  
  
 *RelatedTable*  
 選擇性。 指定相關資料表名稱的 **字串** 值。 *RelatedTable*參數對應至[Table](./table-object-adox.md)物件的**Name**屬性值。  
  
 *RelatedColumn*  
 選擇性。 指定外鍵的相關資料行名稱的 **字串** 值。 *RelatedColumn*參數會對應到資料[行](./column-object-adox.md)物件的**Name**屬性值。  
  
## <a name="remarks"></a>備註  
 *Columns*參數可以採用資料行的名稱或資料行名稱的陣列。  
  
## <a name="applies-to"></a>套用至  
 [Keys 集合 (ADOX)](./keys-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [Append 方法 (ADOX 程式) ](./append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](./append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)