---
title: Name 屬性 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eb367d8ea2ad32037209b37df69c7467246be699
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="name-property-adox"></a>Name 屬性 (ADOX)
表示物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 若要在集合中是唯一沒有名稱。  
  
 **名稱**屬性是讀/寫上[資料行](../../../ado/reference/adox-api/column-object-adox.md)，[群組](../../../ado/reference/adox-api/group-object-adox.md)，[金鑰](../../../ado/reference/adox-api/key-object-adox.md)，[索引](../../../ado/reference/adox-api/index-object-adox.md)， [資料表](../../../ado/reference/adox-api/table-object-adox.md)，和[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件。 **名稱**屬性是唯讀[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)，[程序](../../../ado/reference/adox-api/procedure-object-adox.md)，和[檢視](../../../ado/reference/adox-api/view-object-adox.md)物件。  
  
 讀取/寫入的物件 (**資料行**，**群組**，**金鑰**，**索引**，**資料表**和**使用者**物件)，預設值為空字串 ("")。  
  
> [!NOTE]
>  代表索引鍵，這個屬性是唯讀**金鑰**物件已經附加至集合。 這個屬性是唯讀的資料表，**資料表**物件已經附加至集合。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Key 物件 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料行和資料表附加名稱屬性範例 (VB) 方法](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
