---
description: ADO MD 物件
title: ADO MD 物件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a75672db242d5b7388eb625bc028728c8522b11c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987429"
---
# <a name="ado-md-objects"></a>ADO MD 物件

|Object|描述|  
|-|-|  
|[軸](./axis-object-ado-md.md)|代表一或多個維度的選定成員之儲存格的位置或篩選軸。|  
|[目錄](./catalog-object-ado-md.md)|包含多維度架構資訊 (也就是，cube 和基礎維度、階層、層級和成員) 多維度資料提供者 (MDP) 。|  
|[資料格](./cell-object-ado-md.md)|表示軸座標交集（包含在資料格集內）的資料。|  
|[Cellset](./cellset-object-ado-md.md)|表示多維度查詢的結果。 它是從 cube 或其他資料格集選取的儲存格集合。|  
|[CubeDef](./cubedef-object-ado-md.md)|表示多維架構中的 cube，其中包含一組相關的維度。|  
|[維度](./dimension-object-ado-md.md)|表示多維度 cube 的其中一個維度，其中包含一或多個成員階層。|  
|[階層](./hierarchy-object-ado-md.md)|表示維度成員可以匯總或「匯總」的一種方式。 維度可以沿著一或多個階層進行匯總。|  
|[Level](./level-object-ado-md.md)|包含一組成員，其中每個成員在階層內都有相同的順位。|  
|[成員](./member-object-ado-md.md)|表示 cube 中層級的成員、層級成員的子系，或是沿著資料格集軸的位置成員。|  
|[位置](./position-object-ado-md.md)|表示一組不同維度的一或多個成員，這些成員會沿著軸定義點。|  
  
 此外， **目錄** 物件也會連接到包含在標準 ado 程式庫中的 ado **連接** 物件：  
  
|Object|描述|  
|------------|-----------------|  
|[[連接]](../ado-api/connection-object-ado.md)|表示資料來源的開啟連接。|  
  
 這些物件之間的關聯性會在 [ADO MD 物件模型](./ado-md-object-model.md)中說明。  
  
 許多 ADO MD 物件都可以包含在對應的集合中。 例如， [CubeDef](./cubedef-object-ado-md.md)物件可以包含在**目錄**的[CubeDefs](./cubedefs-collection-ado-md.md)集合中。 如需詳細資訊，請參閱 [ADO MD 集合](./ado-md-collections.md)。  
  
## <a name="see-also"></a>另請參閱  
 [ADO MD API 參考](./ado-md-object-model.md?view=sql-server-ver15)   
 [ADO MD 程式碼範例](./ado-md-code-examples.md)   
 [ADO MD 集合](./ado-md-collections.md)   
 [ADO MD 列舉常數](./ado-md-enumerated-constants.md)   
 [ADO MD 方法](./ado-md-methods.md)   
 [ADO MD 物件模型](./ado-md-object-model.md)   
 [ADO MD 屬性](./ado-md-properties.md)