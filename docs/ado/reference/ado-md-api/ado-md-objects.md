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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c06214d23441782cbe5e14433b16928224d5d48c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709846"
---
# <a name="ado-md-objects"></a>ADO MD 物件

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|表示位置或包含一或多個維度的成員可選取的資料格集的篩選座標軸。|  
|[目錄](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|包含多維度的結構描述特有的資訊 （也就是 cube 和基礎維度、 階層、 層級和成員） 的多維度資料提供者 (MDP)。|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|表示軸座標為單位，包含在資料格集的交集處的資料。|  
|[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|表示多維度查詢的結果。 它是從 cube 或其他資料格集中選取的儲存格的集合。|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|表示從多維度的結構描述，其中包含一組相關的維度的 cube。|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|代表其中一個維度的多維度 cube，其中包含一或多個階層的成員。|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|提供一種方法，在其中維度的成員可以彙總或 「 彙總 」。 維度可以加以彙總一或多個階層。|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|包含一組成員，每個都有相同的陣序，在階層中。|  
|[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)|代表在 cube 中，層級成員的層級、 成員或成員的資料格集沿著座標軸的位置的子系。|  
|[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)|代表一組一個或多個不同的維度成員會定義沿著某個軸點。|  
  
 此外， **Catalog**物件連接至 ADO**連線**物件，它是隨附於標準的 ADO 程式庫：  
  
|Object|描述|  
|------------|-----------------|  
|[[連接]](../../../ado/reference/ado-api/connection-object-ado.md)|表示資料來源的開啟連接。|  
  
 這些物件之間的關聯性如下所示[ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)。  
  
 中對應的集合可包含許多的 ADO MD 物件。 例如， [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)物件中可包含[CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)集合**目錄**。 如需詳細資訊，請參閱 < [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD API 參考](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [ADO MD 程式碼範例](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD 集合](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD 列舉常數](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [ADO MD 方法](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [ADO MD 物件模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO MD 屬性](../../../ado/reference/ado-md-api/ado-md-properties.md)
