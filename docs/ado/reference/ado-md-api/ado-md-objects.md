---
title: ADO MD 物件 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ae297d189b03af51c73a98e6f273601e805b25c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="ado-md-objects"></a>ADO MD 物件
|||  
|-|-|  
|[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示位置或包含一或多個維度的成員可選取的資料格集的篩選座標軸。|  
|[目錄](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含多維度結構描述特有的資訊 （也就是 cube 和基礎維度、 階層、 層級和成員） 的多維度資料提供者 (MDP)。|  
|[資料格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|表示資料格集中所包含的軸座標交集處的資料。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|代表多維度查詢的結果。 它是從 cube 或其他資料格集中選取的儲存格的集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|代表多維度結構描述，其中包含一組相關維度的 cube。|  
|[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|代表其中一個多維度 cube，其中包含一或多個成員階層的維度。|  
|[階層架構](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|提供一種方法中維度的成員可以彙總或 「 彙總 」。 維度可彙總一或多個階層中。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一組成員，每一個都有相同的陣序，在階層中。|  
|[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)|代表在 cube 中，層級成員的層級、 成員或成員的資料格集沿座標軸的位置的子系。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|代表一組不同維度之一個或多個成員會定義沿著軸的點。|  
  
 此外，**目錄**物件連接到 ADO**連接**物件，它是隨附於標準的 ADO 程式庫：  
  
|物件|Description|  
|------------|-----------------|  
|[連接](../../../ado/reference/ado-api/connection-object-ado.md)|代表資料來源的開啟連接。|  
  
 這些物件之間的關聯性所示[ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)。  
  
 許多 ADO MD 物件可以包含在對應的集合。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)物件可以包含在[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合**目錄**。 如需詳細資訊，請參閱[ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD 應用程式開發介面參考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 程式碼範例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 列舉常數](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 屬性](../../../ado/reference/ado-md-api/ado-md-properties.md)
