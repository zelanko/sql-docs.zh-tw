---
description: Append 方法 (ADOX Columns)
title: 將方法附加至 ADOX 資料行 () |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 1c959f6d822724ee6e7480cf00941aaa1fc8012a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985499"
---
# <a name="append-method-adox-columns"></a>Append 方法 (ADOX Columns)
將新的資料 [行](./column-object-adox.md) 物件加入至資料 [行](./columns-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>參數  
 *資料行*  
 要附加的資料 **行** 物件，或是要建立和附加的資料行名稱。  
  
 *類型*  
 選擇性。 **Long**值，指定資料行的資料類型。 *Type*參數對應到資料**行**物件的[type](./type-property-column-adox.md)屬性。  
  
 *DefinedSize*  
 選擇性。 **Long**值，指定資料行的大小。 *DefinedSize*參數對應至資料**行**物件的[DefinedSize](./definedsize-property-adox.md)屬性。  
  
> [!NOTE]
>  如果資料行不存在於已附加至[資料表](./tables-collection-adox.md)集合的[資料表](./table-object-adox.md)中，將資料**行**附加至[索引](./index-object-adox.md)的資料**行**集合**時，將**會發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Columns 集合 (ADOX)](./columns-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](./append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](./append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)