---
title: Cube 物件 (Analysis Services-多維度資料) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- cubes [Analysis Services], objects
ms.assetid: 5cee362e-3f95-4467-bc6c-29b1518ecbf3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47befc9fb80f84318cd090bb673b6b6906da6508
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047607"
---
# <a name="cube-objects-analysis-services---multidimensional-data"></a>Cube 物件 (Analysis Services - 多維度資料)
    
## <a name="introducing-cube-objects"></a>Cube 物件簡介  
 簡單的 <xref:Microsoft.AnalysisServices.Cube> 物件是由以下項目所組成：基本資訊、維度和量值群組。 基本資訊包括 Cube 的名稱、Cube 的預設量值、資料來源、儲存模式等等。  
  
 Dimensions 集合包含在 Cube 中使用的一組來自資料庫維度集合的實際維度。 所有維度都必須先定義在資料庫的維度集合中，才能在 Cube 中參考。 私用維度不適用於[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
 量值群組是 Cube 中的量值集合。 量值群組是具有共同資料來源檢視及共同一組維度的量值集合。 量值群組是量值的處理單位；量值群組可以個別處理，然後進行瀏覽。  
  
## <a name="in-this-section"></a>本節內容  
  
|||  
|-|-|  
|主題||  
|[動作&#40;Analysis Services-多維度資料&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)||  
|[彙總和彙總設計](aggregations-and-aggregation-designs.md)||  
|[計算](calculations.md)||  
|[Cube 資料格&#40;Analysis Services-多維度資料&#41;](cube-cells-analysis-services-multidimensional-data.md)||  
|[Cube 屬性](cube-properties-multidimensional-model-programming.md)||  
|[Cube 儲存區&#40;Analysis Services-多維度資料&#41;](cube-storage-analysis-services-multidimensional-data.md)||  
|[Cube 翻譯](cube-translations.md)||  
|[維度關聯性](dimension-relationships.md)||  
|[關鍵效能指標&#40;Kpi&#41;多維度模型中](../multidimensional-models/key-performance-indicators-kpis-in-multidimensional-models.md)||  
|[量值和量值群組](../multidimensional-models/measures-and-measure-groups.md)||  
|[資料分割&#40;Analysis Services-多維度資料&#41;](partitions-analysis-services-multidimensional-data.md)||  
|[檢視方塊](perspectives.md)||  
  
  
