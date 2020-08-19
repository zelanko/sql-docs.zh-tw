---
description: Description 屬性 (ADO MD)
title: Description 屬性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: rothja
ms.author: jroth
ms.openlocfilehash: 262d83f37157af43a91c508daaa31127247588d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441120"
---
# <a name="description-property-ado-md"></a>Description 屬性 (ADO MD)
傳回目前物件的文字說明。  
  
## <a name="return-values"></a>傳回值  
 傳回 **字串** ，而且是唯讀的。  
  
## <a name="remarks"></a>備註  
 若為 [成員](../../../ado/reference/ado-md-api/member-object-ado-md.md) 物件， **描述** 只適用于 measure 和 formula 成員。 **描述** 會針對所有其他類型的成員，傳回空字串 ( "" ) 。 如需各種類型成員的詳細資訊，請參閱 [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) 屬性。  
  
 只有屬於[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件的**成員**物件才支援這個屬性。 從屬於[Position](../../../ado/reference/ado-md-api/position-object-ado-md.md)物件的**成員**物件參考這個屬性時，就會發生錯誤。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [CubeDef 物件 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)  
        [Dimension 物件 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Hierarchy 物件 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)  
        [Level 物件 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Member 物件 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
    :::column-end:::
:::row-end:::
