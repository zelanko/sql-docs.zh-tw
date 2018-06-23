---
title: 在圖表中放置標籤 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 4b7782cb836f437aa61064d64d084859dedf97ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144876"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>在圖表中放置標籤 (報表產生器及 SSRS)
  因為每種圖表類型都有不同的形狀，所以資料點標籤會放置於最佳位置，避免影響圖表。 標籤的預設位置會因圖表類型而不同：  
  
-   在堆疊圖表上，標籤只能放置於數列內部。  
  
-   在漏斗圖或金字塔圖上，標籤會位於直條外部。  
  
-   在圓形圖上，標籤會位於圓形圖上的個別配量內部。  
  
-   在橫條圖上，標籤會位於代表資料點的橫條外部。  
  
-   在極座標圖上，標籤會位於代表資料點的圓形區域外部。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>若要變更點標籤在圓形圖內的位置  
  
1.  建立圓形圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]。  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 圓形圖的屬性清單隨即顯示。  
  
6.  選取 PieLabelStyle 屬性的值。  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>變更點標籤在漏斗圖或金字塔圖內的位置  
  
1.  建立漏斗圖或金字塔圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 漏斗圖的屬性清單隨即顯示。  
  
6.  若為漏斗圖，請選取 FunnelLabelStyle 屬性的值。 若為金字塔圖，請選取 PyramidLabelStyle 屬性的值。  
  
    > [!NOTE]  
    >  當這個屬性設為值`OutsideInColumn`，標籤就會繪製在垂直欄中。 您無法變更直條的位置。  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>若要變更點標籤在橫條圖內的位置  
  
1.  建立橫條圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下圖表。 圖表的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [一般]  區段中，展開 [CustomAttributes]  節點。 橫條圖的屬性清單隨即顯示。  
  
6.  選取 BarLabelStyle 屬性的值。  
  
 當橫條標籤樣式設定為`Outside`，標籤會位於外部資料列，只要圖表區域能夠容納。 如果標籤無法位於橫條外部，但位於圖表區域內部，此標籤就會位於橫條內部最接近橫條結尾的位置。  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>變更點標籤在區域圖、直條圖、折線圖或散佈圖內的位置  
  
1.  建立區域圖、直條圖、折線圖或散佈圖。  
  
2.  在設計介面上，以滑鼠右鍵按一下圖表，然後選取 [顯示資料標籤]。  
  
3.  開啟 [屬性] 窗格。 在 [檢視] 索引標籤上，按一下 [屬性]  
  
4.  在設計介面上，按一下數列。 數列的屬性會顯示在 [屬性] 窗格中。  
  
5.  在 [資料] 區段中，展開 [DataPoint] 節點，然後展開 [Label] 節點。  
  
6.  選取 Position 屬性的值。  
  
## <a name="see-also"></a>另請參閱  
 [圓形圖&#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [橫條圖&#40;報表產生器和 SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [在圓形圖外部顯示資料點標籤&#40;報表產生器和 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  