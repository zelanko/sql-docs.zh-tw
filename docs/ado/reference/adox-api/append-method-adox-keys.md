---
description: Append 方法 (ADOX Keys)
title: 附加方法 (ADOX 索引鍵) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae3ef035594b696b829f0f1898e1749a2c33f11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440530"
---
# <a name="append-method-adox-keys"></a>Append 方法 (ADOX Keys)
將新的索引 [鍵](../../../ado/reference/adox-api/key-object-adox.md) 物件加入至索引 [鍵](../../../ado/reference/adox-api/keys-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>參數  
 *索引鍵*  
 要附加的索引 **鍵** 物件，或是要建立和附加的索引鍵名稱。  
  
 *KeyType*  
 選擇性。 指定索引鍵類型的 **Long** 值。 *Key*參數對應到**Key**物件的[Type](../../../ado/reference/adox-api/type-property-key-adox.md)屬性。  
  
 *資料行*  
 選擇性。 指定要編制索引之資料行名稱的 **字串** 值。 *Columns*參數會對應到資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件的[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性值。  
  
 *RelatedTable*  
 選擇性。 指定相關資料表名稱的 **字串** 值。 *RelatedTable*參數對應至[Table](../../../ado/reference/adox-api/table-object-adox.md)物件的**Name**屬性值。  
  
 *RelatedColumn*  
 選擇性。 指定外鍵的相關資料行名稱的 **字串** 值。 *RelatedColumn*參數會對應到資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件的**Name**屬性值。  
  
## <a name="remarks"></a>備註  
 *Columns*參數可以採用資料行的名稱或資料行名稱的陣列。  
  
## <a name="applies-to"></a>套用至  
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [將方法附加至 ADOX 群組 () ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 (ADOX 程式) ](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
