---
title: "將圖表上的資料點格式化 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10248"
- sql13.rtp.rptdesigner.serieslabelproperties.general.f1
ms.assetid: 08ec3818-f63a-4e89-b52c-750e47f48b85
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: bf3c5c3a2a9603f996a2a66e51367b56669b12ff
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="formatting-data-points-on-a-chart-report-builder-and-ssrs"></a>格式化圖表上的資料點 (報表產生器及 SSRS)
在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 編頁報表中，資料點是圖表上最小的個別實體。 在非形狀圖上，資料點的表示取決於其圖表類型。 例如，線條數列由一個或多個已連接的資料點所組成。 在形狀圖上，資料點會以加入到整個圖表的個別配量或區段表示。 例如，在圓形圖上，每一塊都是一個資料點。 如需詳細資訊，請參閱 [圖表類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)。  
  
 一個或多個資料點會形成一個數列。 根據預設，系統會將所有格式選項套用到數列中的所有資料點。 如果您要指定個別資料點的屬性，可以針對數列指定在執行階段根據資料集格式化個別資料點的欄位或運算式。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-tooltips-and-drillthrough-actions-to-data-points"></a>將工具提示和鑽研動作加入到資料點中  
 您可以在數列上設定 **ToolTip** 屬性的值，以便將工具提示加入到每個資料點中。 您可以透過顯示工具提示，讓使用者能夠看到與資料點相關的任何資訊，例如，群組名稱、資料點的值，以及相對於數列總數之資料點的百分比。 如需詳細資訊，請參閱 [在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)。  
  
 您也可以在數列上指定資料點的鑽研動作來顯示其他報表或 URL。 您可以傳遞參數來顯示與已經按下之資料點相關的資訊。 如需詳細資訊，請參閱[在報表上新增鑽研動作 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)。  
  
## <a name="highlighting-individual-data-points-in-a-series"></a>反白顯示數列中的個別資料點  
 在任何非形狀圖上，您可以指定 Color 屬性的運算式，藉以反白顯示個別的資料點。 例如，若要在名稱為 `MyField` 的數列中，以不同於其他資料點的色彩反白顯示資料點的最高值，其運算式類似如下：  
  
 `=Iif(Fields!MyField.Value >= Max(Fields!MyField.Value, "MyDataSet"), "Red", "Green")`  
  
 在此範例中， `MyField` 的最高值色彩將為紅色，而其他所有資料點的色彩則為綠色。 當您使用數列的 **Fill** 屬性指定數列的色彩時，圖表將會覆寫在調色盤中指定的色彩。 如需詳細資訊，請參閱 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="positioning-data-point-labels-on-a-chart"></a>在圖表上放置資料點標籤  
 針對所有圖表類型，當您以滑鼠右鍵按一下圖表，然後選取 **[顯示資料標籤]**時，可以顯示資料點標籤。 資料點標籤的位置會根據圖表類型而指定：  
  
-   在橫條圖上，您可以使用 **BarLabelStyle** 自訂屬性重新放置資料點標籤的位置。 可能的位置有四個：Outside、Left、Center 與 Right。 當橫條標籤樣式設定為 Outside 時，只要圖表區域能夠容納，標籤就會放置在橫條外部。 如果無法將標籤放置在橫條外部與圖表區域內部，標籤就會放在橫條內部。  
  
-   在圓形圖上，您可以使用 **PieLabelStyle** 自訂屬性重新放置資料點標籤的位置。 在圓形圖周圍放置資料點標籤時有許多考量，包括圓形圖的大小、圓形圖及其對應圖例間的可用空間以及標籤的大小。 如需詳細資訊，請參閱 [在圓形圖外部顯示資料點標籤 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)。  
  
-   在金字塔圖或漏斗圖上，您可以使用 **FunnelLabelStyle** 和 **PyramidLabelStyle** 自訂屬性重新放置資料點標籤的位置。 當您已經選取金字塔或漏斗圖表類型後，可以在 **[屬性]** 窗格中設定這些屬性。  
  
-   在堆疊圖上，資料點標籤永遠會放置在數列的內部，而且數列標籤上的 **Position** 屬性會遭到忽略。  
  
-   在其他所有圖表類型上，您可以使用數列標籤上的 **Position** 屬性重新放置資料點標籤的位置。 根據預設，圖表會自動計算資料點標籤的位置以避免標籤衝突。 當您設定 **Position**的值時，所有資料點標籤都會以相同的方式放置，這可能會造成標籤重疊。 請僅在資料點較少時，考慮使用此方法。  
  
 如需詳細資訊，請參閱[圖表中的位置標籤 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/position-labels-in-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="adding-keywords-for-data-point-labels-tooltips-and-legend-text"></a>為資料點標籤、工具提示和圖例文字加入關鍵字  
 您可以使用區分大小寫的圖表專用關鍵字來表示存在於圖表中的項目。 這些關鍵字僅適用於工具提示、自訂圖例文字與資料點標籤屬性。 在許多情況下，圖表關鍵字擁有相等的簡單運算式，但是關鍵字輸入時更快、更容易。 下列是圖表關鍵字的清單。  
  
|圖表關鍵字|說明|適用於圖表類型|相等簡單運算式的範例|  
|-------------------|-----------------|------------------------------|------------------------------------------------|  
|#VALY|資料點的 Y 值。|全部|`=Fields!MyDataField.Value`|  
|#VALY2|資料點的 Y 值 #2。|範圍圖、泡泡圖|無|  
|#VALY3|資料點的 Y 值 #3。|股票圖、K 線圖|無|  
|#VALY4|資料點的 Y 值 #4。|股票圖、K 線圖|無|  
|#SERIESNAME|數列名稱。|全部|無|  
|#LABEL|資料點標籤。|全部|無|  
|#AXISLABEL|軸資料點標籤。|形狀圖|`=Fields!MyDataField.Value`|  
|#INDEX|資料點索引。|全部|無|  
|#PERCENT|資料點 Y 值的百分比。|全部|`=FormatPercent(Fields!MyDataField.Value/Sum(Fields!MyDataField.Value, "MyDataSet"),2)`|  
|#TOTAL|數列中所有 Y 值的總計。|全部|`=Sum(Fields!MyDataField.Value)`|  
|#LEGENDTEXT|對應到圖例項目文字的文字。|全部|無|  
|#AVG|數列中所有 Y 值的平均值。|全部|`=Avg(Fields!MyDataField.Value)`|  
|#MIN|數列中所有 Y 值的最小值。|全部|`=Min(Fields!MyDataField.Value)`|  
|#MAX|數列中所有 Y 值的最大值。|全部|`=Max(Fields!MyDataField.Value)`|  
|#FIRST|數列中所有 Y 值的第一個。|全部|`=First(Fields!MyDataField.Value)`|  
  
 若要格式化關鍵字，請以括號括住 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 格式字串。 例如，若要將工具提示中資料點的值指定為包含兩位小數的數字，請以大括弧包含格式字串 "N2"，例如 "#VALY{N2}" 表示數列的 **ToolTip** 屬性。 如需有關 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 格式字串的詳細資訊，請參閱 MSDN 上的＜ [格式化型別](http://go.microsoft.com/fwlink/?LinkId=112024) ＞。 如需在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中將數字格式化的詳細資訊，請參閱[將數字和日期格式化 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)。  
  
 如需將關鍵字新增至圖表的詳細資訊，請參閱[在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md) 和[變更圖例項目的文字 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/chart-legend-change-item-text-report-builder.md)。  
  
## <a name="increasing-readability-in-a-chart-with-multiple-data-points"></a>在圖表中以多個資料點增加可讀性  
 如果您在圖表上有多個數列，可能會降低圖表資料點的可讀性。 將多個數列加入到圖表時，請考慮使用可區別如何在圖表中有效讀取及了解每個數列的技術。 如需詳細資訊，請參閱 [圖表上的多個數列 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md)：  
  
 為了簡化的目的，當您使用形狀圖時，請考慮僅加入一個資料欄位和一個類別目錄欄位。 如需詳細資訊，請參閱[形狀圖 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)。 如果您的圖表需要一個以上的資料欄位和類別目錄欄位，請考慮變更圖表類型。 您可以用滑鼠右鍵按一下此數列，並選取 **[變更圖表類型]**。  
  
## <a name="inserting-data-point-markers"></a>插入資料點標記  
 資料點標記是一種視覺指標，用於吸引使用者注意數列中的每個資料點。 在散佈圖上，標記用於決定個別資料點的形狀與大小。 標記的大小會根據圖表類型而指定。 您可以變更標記的大小、色彩或樣式。 標記不適用於範圍和形狀圖表類型，也不適用於任何堆疊子類型。  
  
## <a name="in-this-section"></a>本節內容  
 [在數列上顯示工具提示 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [在圓形圖外部顯示資料點標籤 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)  
  
 [在圓形圖上顯示百分比值 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>另請參閱  
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [將軸標籤格式化成日期或貨幣 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [教學課程：將圓形圖新增至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-pie-chart-to-your-report-report-builder.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
