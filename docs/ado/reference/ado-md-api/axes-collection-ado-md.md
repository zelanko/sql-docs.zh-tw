---
description: Axes 集合 (ADO MD)
title: 軸集合 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axes
- Cellset::Axes
helpviewer_keywords:
- Axes collection [ADO MD]
ms.assetid: 072fb21a-ec0f-4b02-9022-1cef3ad4bfff
author: rothja
ms.author: jroth
ms.openlocfilehash: cc93e9ea8568a535067addbd51258074945200db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441312"
---
# <a name="axes-collection-ado-md"></a>Axes 集合 (ADO MD)
包含定義儲存格集的 [座標軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md) 物件。  
  
## <a name="remarks"></a>備註  
 [儲存格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件包含**座標軸**集合。 一旦開啟了 **儲存格** ，此集合就會包含至少一個 **座標軸**。 如需如何使用**軸**物件的詳細說明，請參閱[axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)物件。  
  
> [!NOTE]
>  **儲存格**集的篩選軸不包含在**軸**集合中。 如需詳細資訊，請參閱 [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) 屬性。  
  
 **軸** 是標準的 ADO 集合。 使用集合的屬性和方法，您可以執行下列動作：  
  
-   使用 [Count](../../../ado/reference/ado-api/count-property-ado.md) 屬性取得集合中的物件數目。  
  
-   從集合中傳回具有預設 [專案](../../../ado/reference/ado-api/item-property-ado.md) 屬性的物件。  
  
-   使用 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法，從提供者更新集合中的物件。  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/axes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的集格範例 ](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axis 物件 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)
