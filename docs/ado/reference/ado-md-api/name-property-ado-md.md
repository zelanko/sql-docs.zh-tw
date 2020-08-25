---
description: Name 屬性 (ADO MD)
title: 名稱屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 83207cd13db790d645bea146b2a031604e598256
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777947"
---
# <a name="name-property-ado-md"></a>Name 屬性 (ADO MD)
指出物件的名稱。  
  
## <a name="return-values"></a>傳回值  
 傳回 **字串** ，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 您可以藉由序數參考抓取物件的 **name** 屬性，之後您可以直接依名稱參考該物件。 例如，如果 `cdf.CubeDefs(0).Name` 產生 "Bobs-machine Video Store"，您可以將這個 [CubeDef](./cubedef-object-ado-md.md) 參考為 `cdf.CubeDefs("Bobs Video Store")` 。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Axis 物件 (ADO MD)](./axis-object-ado-md.md)  
        [Catalog 物件 (ADO MD)](./catalog-object-ado-md.md)  
        [CubeDef 物件 (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Dimension 物件 (ADO MD)](./dimension-object-ado-md.md)  
        [Hierarchy 物件 (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Level 物件 (ADO MD)](./level-object-ado-md.md)  
        [Member 物件 (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB) 的目錄範例 ](./catalog-example-vb.md)   
 [Caption 屬性 (ADO MD) ](./caption-property-ado-md.md)   
 [描述屬性 (ADO MD) ](./description-property-ado-md.md)   
 [UniqueName 屬性 (ADO MD)](./uniquename-property-ado-md.md)