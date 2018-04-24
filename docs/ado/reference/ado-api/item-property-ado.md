---
title: 項目屬性 (ADO) |Microsoft 文件
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
- Parameters::GetItem
- Indexes::GetItem
- Parameters::Item
- Tables::Item
- Procedures::Item
- Users::GetItem
- Tables::GetItem
- Procedures::GetItem
- Users::get_Item
- Users::Item
- Views::GetItem
- Groups::Item
- Groups::get_Item
- Columns::Item
- Indexes::Item
- Fields15::GetItem
- Columns::GetItem
- Fields::Item
- Indexes::get_Item
- Columns::get_Item
- Fields15::Item
- Views::get_Item
- Groups::GetItem
- Errors::get_Item
- Fields15::get_Item
- Tables::get_Item
- Views::Item
- Errors::GetItem
- Parameters::get_Item
- Errors::Item
- Procedures::get_Item
helpviewer_keywords:
- Item property [ADO]
ms.assetid: e11484bb-c5c7-42d8-9bb8-21572125d727
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f41925b97564c608c66b33aa611c73bfd163386e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="item-property-ado"></a>項目屬性 (ADO)
依名稱或序數數字，指出特定集合的成員。  
  
## <a name="syntax"></a>語法  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回的物件參考。  
  
## <a name="parameters"></a>參數  
 *Index*  
 A **Variant**運算式評估的名稱或物件集合中的序號。  
  
## <a name="remarks"></a>備註  
 使用**項目**屬性，以傳回集合中的特定物件。 如果**項目**對應至集合中找不到物件*索引*引數，就會發生錯誤。 此外，某些集合不支援具名的物件。對於這些集合中，您必須使用序數編號參考。  
  
 **項目**屬性是所有集合的預設屬性; 因此，下列語法形式是可互換的：  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Dimensions 集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Levels 集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Positions 集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另請參閱  
 [項目屬性範例 (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Item 屬性範例 (VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
