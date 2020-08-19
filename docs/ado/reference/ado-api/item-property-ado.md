---
description: Item 屬性 (ADO)
title: 專案屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d2581d0834325d56daa8ea1043ac3915942961eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443400"
---
# <a name="item-property-ado"></a>Item 屬性 (ADO)
以名稱或序數表示集合的特定成員。  
  
## <a name="syntax"></a>語法  
  
```  
Set object = collection.Item ( Index )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回物件參考。  
  
## <a name="parameters"></a>參數  
 *Index*  
 **Variant**運算式，會評估為集合中物件的名稱或序號。  
  
## <a name="remarks"></a>備註  
 使用 **Item** 屬性可傳回集合中的特定物件。 如果 **專案** 在集合中找不到對應至 *索引* 引數的物件，就會發生錯誤。 此外，有些集合不支援命名物件;針對這些集合，您必須使用序數數位參考。  
  
 **Item**屬性是所有集合的預設屬性;因此，下列語法形式可以互換：  
  
```  
collection.Item (Index)  
collection (Index)  
```  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)  
        [Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions 集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 集合 (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)  
        [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
        [Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
        [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [Levels 集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)  
        [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)  
        [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions 集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)  
        [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)  
        [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
        [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
        [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [專案屬性範例 (VB) ](../../../ado/reference/ado-api/item-property-example-vb.md)   
 [Item 屬性範例 (VC++)](../../../ado/reference/ado-api/item-property-example-vc.md)   
