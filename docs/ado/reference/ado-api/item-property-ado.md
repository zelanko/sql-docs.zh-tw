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
ms.openlocfilehash: 6bea35ef148aa2f5646420a1c2b46197ce66f0d6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774677"
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
        [Axes 集合 (ADO MD)](../ado-md-api/axes-collection-ado-md.md)  
        [Columns 集合 (ADOX)](../adox-api/columns-collection-adox.md)  
        [CubeDefs 集合 (ADO MD)](../ado-md-api/cubedefs-collection-ado-md.md)  
        [Dimensions 集合 (ADO MD)](../ado-md-api/dimensions-collection-ado-md.md)  
        [Errors 集合 (ADO)](./errors-collection-ado.md)  
        [Fields 集合 (ADO)](./fields-collection-ado.md)  
        [Groups 集合 (ADOX)](../adox-api/groups-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Hierarchies 集合 (ADO MD)](../ado-md-api/hierarchies-collection-ado-md.md)  
        [Indexes 集合 (ADOX)](../adox-api/indexes-collection-adox.md)  
        [Keys 集合 (ADOX)](../adox-api/keys-collection-adox.md)  
        [Levels 集合 (ADO MD)](../ado-md-api/levels-collection-ado-md.md)  
        [Members 集合 (ADO MD)](../ado-md-api/members-collection-ado-md.md)  
        [Parameters 集合 (ADO)](./parameters-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Positions 集合 (ADO MD)](../ado-md-api/positions-collection-ado-md.md)  
        [Procedures 集合 (ADOX)](../adox-api/procedures-collection-adox.md)  
        [Properties 集合 (ADO)](./properties-collection-ado.md)  
        [Tables 集合 (ADOX)](../adox-api/tables-collection-adox.md)  
        [Users 集合 (ADOX)](../adox-api/users-collection-adox.md)  
        [Views 集合 (ADOX)](../adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [專案屬性範例 (VB) ](./item-property-example-vb.md)   
 [Item 屬性範例 (VC++)](./item-property-example-vc.md)