---
description: Append 方法 (ADOX Columns)
title: 將方法附加至 ADOX 資料行 () |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: rothja
ms.author: jroth
ms.openlocfilehash: bd33dc71c9adcbe8e6ed25f965b227fbc76d96fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440520"
---
# <a name="append-method-adox-columns"></a>Append 方法 (ADOX Columns)
將新的資料 [行](../../../ado/reference/adox-api/column-object-adox.md) 物件加入至資料 [行](../../../ado/reference/adox-api/columns-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
 要附加的資料 **行** 物件，或是要建立和附加的資料行名稱。  
  
 *型別*  
 選擇性。 **Long**值，指定資料行的資料類型。 *Type*參數對應到資料**行**物件的[type](../../../ado/reference/adox-api/type-property-column-adox.md)屬性。  
  
 *DefinedSize*  
 選擇性。 **Long**值，指定資料行的大小。 *DefinedSize*參數對應至資料**行**物件的[DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)屬性。  
  
> [!NOTE]
>  如果資料行不存在於已附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[資料表](../../../ado/reference/adox-api/table-object-adox.md)中，將資料**行**附加至[索引](../../../ado/reference/adox-api/index-object-adox.md)的資料**行**集合**時，將**會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [將方法附加至 ADOX 群組 () ](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
