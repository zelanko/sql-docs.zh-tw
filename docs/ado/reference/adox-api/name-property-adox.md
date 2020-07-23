---
title: Name 屬性（ADOX） |Microsoft Docs
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
ms.openlocfilehash: 24d86b384a1eb2916e488c17c99e4b9b5962dd1a
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942720"
---
# <a name="name-property-adox"></a>Name 屬性 (ADOX)
指出物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 名稱在集合中不需要是唯一的。  
  
 **Name**屬性在[Column](../../../ado/reference/adox-api/column-object-adox.md)、 [Group](../../../ado/reference/adox-api/group-object-adox.md)、 [Key](../../../ado/reference/adox-api/key-object-adox.md)、 [Index](../../../ado/reference/adox-api/index-object-adox.md)、 [Table](../../../ado/reference/adox-api/table-object-adox.md)和[User](../../../ado/reference/adox-api/user-object-adox.md)物件上是讀取/寫入。 **Name**屬性在[Catalog](../../../ado/reference/adox-api/catalog-object-adox.md)、 [Procedure](../../../ado/reference/adox-api/procedure-object-adox.md)和[View](../../../ado/reference/adox-api/view-object-adox.md)物件上是唯讀的。  
  
 對於讀取/寫入物件（**資料行**、**群組**、索引**鍵**、**索引**、**資料表**和**使用者**物件），預設值為空字串（""）。  
  
> [!NOTE]
>  針對索引鍵，此屬性在已附加至集合的索引**鍵**物件上是唯讀的。 對於資料表而言，這個屬性對於已經附加至集合的**資料表**物件而言是唯讀的。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
        [Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
        [Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)  
    :::column-end:::
    :::column:::
        [Key 物件 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)  
        [Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
        [Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
        [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
        [View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
