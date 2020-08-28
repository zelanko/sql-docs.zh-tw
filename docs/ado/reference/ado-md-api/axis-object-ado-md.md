---
description: Axis 物件 (ADO MD)
title: 軸物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: 6206ee753e42853dc0f209cb80fb9571806f68d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987389"
---
# <a name="axis-object-ado-md"></a>Axis 物件 (ADO MD)
代表一或多個維度的選定成員之儲存格的位置或篩選軸。  
  
## <a name="remarks"></a>備註  
 **軸**物件可以包含在[座標軸](./axes-collection-ado-md.md)集合中，或由[儲存格集](./cellset-object-ado-md.md)的[FilterAxis](./filteraxis-property-ado-md.md)屬性傳回。  
  
 透過 **Axis** 物件的集合和屬性，您可以執行下列動作：  
  
-   使用[Name](./name-property-ado-md.md)屬性來識別**軸**。  
  
-   使用[position](./positions-collection-ado-md.md)集合逐一查看**軸**中的每個位置。  
  
-   使用[DimensionCount](./dimensioncount-property-ado-md.md)屬性取得**軸**上的維度數目。  
  
-   使用標準的 ADO[屬性](../ado-api/properties-collection-ado.md)集合，取得**軸**的提供者特定屬性。  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](./axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的座標軸範例 ](./axis-example-vbscript.md)   
 [軸集合 (ADO MD) ](./axes-collection-ado-md.md)   
 [位置集合 (ADO MD) ](./positions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)