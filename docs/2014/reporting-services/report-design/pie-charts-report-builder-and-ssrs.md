---
title: 圓形圖 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 536efa9c-c6fb-4cdd-b41f-ff5382910bd7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f10e941ef5acd180e8b279762e84535bad5689e4
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043219"
---
# <a name="pie-charts-report-builder-and-ssrs"></a>圓形圖 (報表產生器及 SSRS)
  圓形圖和環圈圖會將資料顯示為整體所佔的百分比。 圓形圖最常用於在群組之間進行比較。 圓形圖和環圈圖以及金字塔圖和漏斗圖是由一組所謂形狀圖的圖表所組成。 形狀圖沒有軸。 在形狀圖上放置數值欄位時，圖表會計算出每個值佔整體的百分比。 如需形狀圖的詳細資訊，請參閱[形狀圖 &#40;報表產生器及 SSRS &#41;](charts-report-builder-and-ssrs.md)。  
  
 下圖顯示的是包含百分比格式之資料標籤的立體圓形圖。  圖例會位於中間靠右。  
  
 ![圓形圖](../media/piechart.gif "圓形圖")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>變數  
  
-   **分裂式圓形圖**： 一種圓形圖，其中所有的扇區會從圓形圖的中央向外移動。 除了所有扇區都分離的分裂式圓形圖之外，您也可以建立只有一個扇區的分裂式扇形圖。  
  
-   **環圈圖**： 中央具有開放空間的一種圓形圖。  
  
-   **分裂式環圈圖**： 一種環圈圖，其中所有的扇區會從環圈圖的中央向外移動。  
  
-   **立體圓形圖**： 套用立體樣式的一種圓形圖。  
  
-   **立體分裂式圓形圖**： 套用立體樣式的一種分裂式圓形圖。  
  
## <a name="data-considerations-for-display-on-a-pie-chart"></a>在圓形圖上顯示的資料考量  
  
-   圓形圖因為其視覺效果而在報表上相當普遍。 不過，圓形圖是非常簡化的圖表類型，在表示資料時可能不是最適合。 只有在資料已彙整為七個資料點 (含) 以下後，才考慮使用圓形圖。  
  
-   圓形圖會將每個資料群組顯示為圖表上的個別扇區。 您至少必須將一個資料欄位和一個類別目錄欄位加入至圓形圖中。 如果將一個以上的資料欄位加入到圓形圖中，圓形圖將會在相同的圖表中同時顯示兩個資料欄位。  
  
-   計算比例時，Null 值、空值、負值與零值沒有效用。 因此，這些值不會顯示在圓形圖上。 如果您要在圖表上，以視覺方式表示這些值的類型，請將圖表類型變更為圓形圖之外的其他類型。  
  
-   如果您要在圓形圖上使用自訂調色盤定義自己的色彩，請確認您的調色盤上有足夠的色彩，才能以其獨特的色彩顯示每個資料點。 如需詳細資訊，請參閱 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
-   圓形圖不像其他大部分的圖表類型，它會在其圖例中顯示個別的資料點，而不會顯示個別的數列。  
  
-   圓形圖至少需要兩個值，才能在比例之間進行有效的比較。 如果您的圓形圖只包含一種色彩，請確認您已經在群組依據加入類別目錄欄位。 當圓形圖不包含類別目錄時，它會將來自您資料欄位的值彙總為一個值來顯示。  
  
-   圓形圖就像其他所有圖表類型一樣，會根據預設調色盤中所包含的色彩值，產生色彩。 當您在報表中使用多個圓形圖時，這個方法可能會使不同的圓形圖以不同的色彩顯示資料點。 如果您的報表中有數個圓形圖，您可能會想要為每個類別目錄群組手動設定色彩，才能在不同的圖表上保留相同的色彩。 如需如何在圖表上定義色彩的詳細資訊，請參閱 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="applying-drawing-styles-to-a-pie-chart"></a>將繪製樣式套用至圓形圖  
 您可以在圓形圖上加入特殊的繪製樣式來增加其視覺效果。 繪製樣式包括斜面 (Bevel) 和凹面效果。 這些效果僅適用平面圓形圖。 下圖顯示圓形圖的斜面和凹面繪製樣式範例。  
  
 ![圓形圖繪製樣式](../media/rs-piedrawingeffects-concave2.gif "圓形圖繪製樣式")  
  
 如需詳細資訊，請參閱[將斜面、浮凸與紋理樣式加入圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)。  
  
## <a name="displaying-percentage-values-on-a-pie-chart"></a>在圓形圖上顯示百分比值  
 圓形圖就像其他形狀圖一樣，可以表示整體的比例。 因此，將圓形圖標籤的格式設定為百分比相當常見。 為與其他圖表類型保持一致，圓形圖預設不顯示百分比標籤。 如需如何以百分比在圖表上顯示值的詳細資訊，請參閱 [在圓形圖上顯示百分比值 &#40;報表產生器及 SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)。 如需如何在報表中將數字格式設定為百分比的詳細資訊，請參閱[格式化數字和日期 &#40;報表產生器及 SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)。  
  
 ![以資料點標籤來表示百分比的圓形圖](../media/rs-piechartpercentages.gif "以資料點標籤來表示百分比的圓形圖")  
  
## <a name="preventing-overlapped-labels-on-a-pie-chart"></a>防止圓形圖上的標籤重疊  
 如果圓形圖上有許多資料點，資料標籤將會重疊。 有一些方式可以防止標籤重疊：  
  
-   減少資料點標籤的字型大小。  
  
-   增加圖表的寬度和高度，讓標籤有更多的空間。  
  
-   在圖表區域外部顯示圓形圖標籤。 如需詳細資訊，請參閱 [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)。  
  
-   將小圓形圖扇區收集成一個扇區。  
  
## <a name="consolidating-small-slices-on-a-pie-chart"></a>在圓形圖上合併小配量  
 當圓形圖有太多點時，資料會被遮住而且難以讀取。 如果您的資料有許多小資料點，有兩種方式可以收集多個圓形圖配量：  
  
-   將小資料配量收集成圓形圖上的一個配量。 例如，當您想要讓圓形圖擁有只收集剩餘資料的「其他」資料點時，此作法相當實用。 如需詳細資訊，請參閱 [收集圓形圖上的小配量 &#40;報表產生器及 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)。  
  
-   將小配量收集成補充的圓形圖。 第二個圓形圖不會顯示在設計工具中。 但是在報表處理期間，圖表會根據資料點的值，計算是否需要顯示另一個圓形圖。 如果需要，這些值會加入到另一個圓形圖中。  
  
## <a name="see-also"></a>另請參閱  
 [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [收集圓形圖上的小配量 &#40;報表產生器及 SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [在圓形圖上顯示百分比值 &#40;報表產生器和 SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [教學課程：將圓形圖加入至報表&#40;報表產生器&#41;](../tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
  
  
