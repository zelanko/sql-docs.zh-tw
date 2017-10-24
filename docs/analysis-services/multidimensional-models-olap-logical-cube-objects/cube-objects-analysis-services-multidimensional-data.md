---
title: "Cube 物件 (Analysis Services-多維度資料) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 018739c4f8da237c1a90a101b96888a8583349be
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Cube 物件 (Analysis Services - 多維度資料)
    
## <a name="introducing-cube-objects"></a>Cube 物件簡介  
 簡單的 <xref:Microsoft.AnalysisServices.Cube> 物件是由以下項目所組成：基本資訊、維度和量值群組。 基本資訊包括 Cube 的名稱、Cube 的預設量值、資料來源、儲存模式等等。  
  
 Dimensions 集合包含在 Cube 中使用的一組來自資料庫維度集合的實際維度。 所有維度都必須先定義在資料庫的維度集合中，才能在 Cube 中參考。 私用維度都無法使用[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 量值群組是 Cube 中的量值集合。 量值群組是具有共同資料來源檢視及共同一組維度的量值集合。 量值群組是量值的處理單位；量值群組可以個別處理，然後進行瀏覽。  
  
## <a name="in-this-section"></a>本節內容  
  
|||  
|-|-|  
|主題||  
|[動作 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[彙總和彙總設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)||  
|[計算](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md)||  
|[Cube 資料格子集 &#40;Analysis Services-多維度資料 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-cells-analysis-services-multidimensional-data.md)||  
|[Cube 內容-多維度模型程式設計](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-properties-multidimensional-model-programming.md)||  
|[Cube 儲存體 &#40;Analysis Services-多維度資料 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)||  
|[Cube 翻譯](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md)||  
|[維度關聯性](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)||  
|[多維度模型中的關鍵效能指標 &#40;KPI&#41;](../../analysis-services/multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[量值和量值群組](../../analysis-services/multidimensional-models/measures-and-measure-groups.md)||  
|[資料分割 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)||  
|[檢視方塊](../../analysis-services/multidimensional-models-olap-logical-cube-objects/perspectives.md)||  
  
  

