---
title: "項目屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 59779714027c0ff619293d01de851daec7bbe158
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
 *索引*  
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
|[Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[維度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[錯誤集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[索引鍵集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[層級集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[成員集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[位置集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[程序集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[資料表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[使用者集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[檢視集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>另請參閱  
 [項目屬性範例 (VB)](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [項目屬性的範例 （VC + +）](../../../ado/reference/ado-api/item-property-example-vc.md)   

