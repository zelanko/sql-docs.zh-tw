---
title: Name 屬性 (ADOX) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f7b61dd2c1dc5899852234d23148969dad9c3dc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706381"
---
# <a name="name-property-adox"></a>Name 屬性 (ADOX)
表示物件的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值。  
  
## <a name="remarks"></a>備註  
 若要在集合中是唯一沒有名稱。  
  
 **名稱**屬性是讀取/寫入上[資料行](../../../ado/reference/adox-api/column-object-adox.md)，[群組](../../../ado/reference/adox-api/group-object-adox.md)，[鍵](../../../ado/reference/adox-api/key-object-adox.md)，[索引](../../../ado/reference/adox-api/index-object-adox.md)， [表格](../../../ado/reference/adox-api/table-object-adox.md)，並[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件。 **名稱**屬性是唯讀[類別目錄](../../../ado/reference/adox-api/catalog-object-adox.md)，[程序](../../../ado/reference/adox-api/procedure-object-adox.md)，以及[檢視](../../../ado/reference/adox-api/view-object-adox.md)物件。  
  
 讀取/寫入物件 (**資料行**，**群組**，**金鑰**，**索引**，**資料表**和**使用者**物件)，預設值為空字串 ("")。  
  
> [!NOTE]
>  代表索引鍵，這個屬性是唯讀**金鑰**已經附加到集合的物件。 對於資料表，這個屬性是唯讀**資料表**已經附加到集合的物件。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)|[Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)|  
|[Key 物件 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)|[Procedure 物件 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)|[Property 物件 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
|[Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|[User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)|[View 物件 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、 Name 屬性範例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
