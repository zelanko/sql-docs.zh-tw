---
description: Name 屬性 (ADOX)
title: 名稱屬性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 0376017e4ab74822a076379385b4b5ab457afca0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769957"
---
# <a name="name-property-adox"></a>Name 屬性 (ADOX)
指出物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值。  
  
## <a name="remarks"></a>備註  
 名稱在集合中不一定是唯一的。  
  
 **Name**屬性是資料[行](./column-object-adox.md)、[群組](./group-object-adox.md)、索引[鍵](./key-object-adox.md)、[索引](./index-object-adox.md)、[資料表](./table-object-adox.md)和[使用者](./user-object-adox.md)物件的讀取/寫入。 [Catalog](./catalog-object-adox.md)、 [Procedure](./procedure-object-adox.md)和[View](./view-object-adox.md)物件的**Name**屬性是唯讀的。  
  
 若為讀取/寫入物件 (資料**行**、**群組**、**索引****鍵**、索引、**資料表**和**使用者**物件) ，則預設值為空字串 ( "" ) 。  
  
> [!NOTE]
>  針對索引鍵，此屬性在已附加至集合的索引 **鍵** 物件上是唯讀的。 針對資料表，這個屬性是唯讀的，適用于已附加至集合的 **資料表** 物件。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Column 物件 (ADOX)](./column-object-adox.md)  
        [Group 物件 (ADOX)](./group-object-adox.md)  
        [Index 物件 (ADOX)](./index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Key 物件 (ADOX)](./key-object-adox.md)  
        [Procedure 物件 (ADOX)](./procedure-object-adox.md)  
        [Property 物件 (ADO)](../ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Table 物件 (ADOX)](./table-object-adox.md)  
        [User 物件 (ADOX)](./user-object-adox.md)  
        [View 物件 (ADOX)](./view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](./parentcatalog-property-example-vb.md)