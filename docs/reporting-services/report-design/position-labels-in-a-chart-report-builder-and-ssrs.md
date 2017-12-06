---
title: "在圖表中放置標籤 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 22bc8a6e1a29eb5ed4f2ddefd7ee875eb3ffb327
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>在圖表中放置標籤 (報表產生器及 SSRS)
  因為 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 每種圖表類型都有不同的形狀，所以資料點標籤會放置於最佳位置，避免影響圖表。 標籤的預設位置會因圖表類型而不同：  
  
-   在堆疊圖表上，標籤只能放置於數列內部。  
  
-   在漏斗圖或金字塔圖上，標籤會位於直條外部。  
  
-   在圓形圖上，標籤會位於圓形圖上的個別配量內部。  
  
-   在橫條圖上，標籤會位於代表資料點的橫條外部。  
  
-   在極座標圖上，標籤會位於代表資料點的圓形區域外部。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>若要變更點標籤在圓形圖內的位置  
  
1.  建立圓形圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]。  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 圓形圖的屬性清單隨即顯示。  
  
6.  選取 PieLabelStyle 屬性的值。  
  
## <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>變更點標籤在漏斗圖或金字塔圖內的位置  
  
1.  建立漏斗圖或金字塔圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 漏斗圖的屬性清單隨即顯示。  
  
6.  若為漏斗圖，請選取 FunnelLabelStyle 屬性的值。 若為金字塔圖，請選取 PyramidLabelStyle 屬性的值。  
  
    > [!NOTE]  
    >  當這個屬性設定為 **OutsideInColumn**值時，標籤就會繪製在垂直直條中。 您無法變更直條的位置。  
  
## <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>若要變更點標籤在橫條圖內的位置  
  
1.  建立橫條圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 橫條圖的屬性清單隨即顯示。  
  
6.  選取 BarLabelStyle 屬性的值。  
  
 當橫條標籤樣式設定為 **Outside**時，只要圖表區域能夠容納，標籤就會位於橫條外部。 如果標籤無法位於橫條外部，但位於圖表區域內部，此標籤就會位於橫條內部最接近橫條結尾的位置。  
  
## <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>變更點標籤在區域圖、直條圖、折線圖或散佈圖內的位置  
  
1.  建立區域圖、直條圖、折線圖或散佈圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下數列。 數列的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [資料] 區段中，展開 [DataPoint] 節點，然後展開 [Label] 節點。  
  
6.  選取 Position 屬性的值。  
  
## <a name="see-also"></a>另請參閱  
 [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [橫條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
