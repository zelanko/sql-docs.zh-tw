---
title: 圖表類型 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10423"
ms.assetid: 57b00017-69ae-4e71-8d78-44744e208ac7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9c041a300e9d64e5446f43a68f675f2290dd8963
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581650"
---
# <a name="chart-types-report-builder-and-ssrs"></a>圖表類型 (報表產生器及 SSRS)

針對您要呈現的資料類型選擇適當的圖表類型相當重要。 因為這可以決定以圖表形式放入資料時可以解譯資料的程度。 例如，如果您的資料集包含多個相對於圖表大小的資料點，最好使用區域、線條或散佈圖呈現。 如需如何根據選取的圖表類型準備資料的相關討論，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="choosing-a-chart-type"></a>選擇圖表類型  
 每個圖表類型都有獨特的特性，可協助您將資料集視覺化。 您可以使用任何圖表類型來顯示資料，但是，根據您嘗試要在報表中顯示的項目使用適合您資料的圖表類型時，將會更容易讀取資料。 下表摘要說明影響特定資料集之圖表適合度的圖表功能。  
  
 您可以在建立圖表類型之後再加以變更。 如需詳細資訊，請參閱[變更圖表類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)。  
  
 其中許多圖表類型的範例可從範例報表取得。 如需有關下載範例報表的詳細資訊，請參閱 [報表產生器與報表設計師範例報表](https://go.microsoft.com/fwlink/?LinkId=198283)。  
  
|圖表類型|顯示比例資料|顯示庫存資料|顯示線性資料|顯示多重值資料|  
|----------------|------------------------|------------------------|-------------------------|-------------------------------|  
|[區域圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[橫條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[資料橫條](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[直條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[折線圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||||  
|[極座標圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/polar-charts-report-builder-and-ssrs.md)|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||||  
|[範圍圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)|||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  
|[散佈圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/scatter-charts-report-builder-and-ssrs.md)|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||  
|[形狀圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||||  
|[走勢圖](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  
|[股票圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/stock-charts-report-builder-and-ssrs.md)||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")||![可用](../../reporting-services/report-data/media/greencheck.gif "可用")|  

## <a name="next-steps"></a>後續步驟

[圖表](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[圖表中的空白和 Null 資料點](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
[將圖表新增至報表](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
