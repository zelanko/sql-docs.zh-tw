---
title: ADO MD 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 01a35a38812d105a1e26454022321e57448efadd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765249"
---
# <a name="ado-md-objects"></a>ADO MD 物件

|||  
|-|-|  
|[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示儲存格集的位置或篩選軸，其中包含一或多個維度的選取成員。|  
|[目錄](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含多維度資料提供者（MDP）特有的多維度架構資訊（也就是 cube 和基礎維度、階層、層級和成員）。|  
|[格值](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|代表資料格集內所含軸座標交集的資料。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|表示多維度查詢的結果。 這是從 cube 或其他資料格集中選取的資料格集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|代表多維架構中的 cube，其中包含一組相關維度。|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|表示多維度 cube 的其中一個維度，其中包含一或多個成員的階層。|  
|[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|表示維度成員可以匯總或「匯總」的一種方式。 維度可以沿著一或多個階層匯總。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一組成員，其中每一個都在階層內具有相同的次序。|  
|[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)|代表 cube 中層級的成員、層級成員的子系，或沿著資料格集軸之位置的成員。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|代表一組不同維度的一或多個成員，定義沿著軸的點。|  
  
 此外，**目錄**物件也會連接到包含在標準 ado 程式庫中的 ado**連接**物件：  
  
|Object|描述|  
|------------|-----------------|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|表示資料來源的開啟連接。|  
  
 這些物件之間的關聯性會在[ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)中說明。  
  
 許多 ADO MD 物件可以包含在對應的集合中。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)物件可以包含在**目錄**的[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合中。 如需詳細資訊，請參閱[ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD API 參考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 程式碼範例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 列舉常數](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 屬性](../../../ado/reference/ado-md-api/ado-md-properties.md)
