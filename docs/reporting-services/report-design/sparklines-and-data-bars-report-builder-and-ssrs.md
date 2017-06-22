---
title: "走勢圖和資料橫條 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.sparklines.f1
- "10544"
ms.assetid: b287436b-fa48-4970-a1a7-1dbcb86e7411
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6021dec1c7d072041710c62a533d4e19ead4aa53
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="sparklines-and-data-bars-report-builder-and-ssrs"></a>走勢圖和資料橫條 (報表產生器和 SSRS)
  走勢圖和資料橫條是簡單的小圖表，在極小空間中傳達大量資訊，通常內嵌於文字。   
    
  在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表中，走勢圖和資料橫條經常用於資料表和矩陣中。 其效用在於同時檢視多個走勢圖，能夠一個跟上一個快速地進行比較，而不是單獨檢視各個圖表。 可輕鬆查看極端值，也就是執行時跟其他資料列不相同的資料列。 圖雖然很小，通常每個走勢圖都代表一段時間的多個資料點。 資料橫條可以代表多個資料點，但通常只顯示一個。 每個走勢圖通常都會呈現單一數列。 您不能將走勢圖加入資料表的詳細資料群組中。 因為走勢圖會顯示彙總的資料，必須放在與群組相關聯的儲存格中。 走勢圖和資料橫條有相同的基本圖表元素：類別、數列和值，但是沒有圖例、座標軸線、標籤或刻度標記。  
  
 ![rs_SparklineExample](../../reporting-services/report-design/media/rs-sparklineexample.gif "rs_SparklineExample")  
  
 若要快速地開始使用走勢圖，請參閱 [教學課程：將走勢圖加入至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md) ，以及 [How to: Create a Sparkline in a Table](http://go.microsoft.com/fwlink/?LinkId=197092) (如何：在資料表中建立走勢圖) 和 [Sparklines, Bar Charts, and Indicators in Report Builder](http://technet.microsoft.com/bi/video/ff877165) (報表產生器中的走勢圖、橫條圖與指標) 影片。  
  
> [!NOTE]  
>  走勢圖和資料橫條及其父資料表、矩陣或清單可以與報表分開發行當做報表組件。 深入了解 [報表組件](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
##  <a name="KindsofSparklines"></a> 走勢圖的類型  
 您幾乎可以建立與一般圖表一樣多的走勢圖類型。 一般而言，您無法建立 3D 走勢圖。 您可以建立這些完整圖表的走勢圖版本：  
  
-   [直條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)︰基本、堆疊與 100% 堆疊直條圖。  
  
-   [折線圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/line-charts-report-builder-and-ssrs.md)：3D 折線圖以外的所有圖表。  
  
-   [區域圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/area-charts-report-builder-and-ssrs.md)：3D 區域圖以外的所有圖表  
  
-   [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)：以及環圈圖 (平面和立體)，但不是漏斗圖和金字塔圖之類的其他形狀。  
  
-   [範圍圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/range-charts-report-builder-and-ssrs.md)︰股票圖、K 線圖、誤差長條圖與盒狀圖。  
  
##  <a name="DataBars"></a> 資料橫條  
 資料橫條通常代表單一資料點，不過也可以代表多個資料點，就像一般的橫條圖一樣。 資料橫條通常都包含多個沒有類別的數列或數列群組。  
  
 ![rs_DataBars](../../reporting-services/report-design/media/rs-databars.gif "rs_DataBars")  
  
 在此範例中，使用堆疊的資料橫條，每個資料橫條 (雖然只有一個橫條) 說明多個資料點。 例如，三個不同色彩的橫條可以代表三個優先權層級的工作，以橫條的長度代表指派給每個人員的工作數。 如果改將這些橫條做成 100% 堆疊資料橫條，則每個橫條都會填滿資料格，而不同的色彩就代表每個優先權層級的整體百分比。  
  
 您可以建立這些完整圖表的資料橫條版本：  
  
-   [橫條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)︰基本、堆疊與 100% 堆疊橫條圖。  
  
-   [直條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)︰基本、堆疊與 100% 堆疊直條圖。 直條圖可以是走勢圖或資料橫條。  
  
##  <a name="AlignDatainTableMatrix"></a> 在資料表或矩陣中對齊走勢圖資料  
 當您將走勢圖插入資料表或矩陣時，每個走勢圖中的資料點通常最好對齊該直條圖中其他走勢圖的資料點。 否則，很難比較不同資料列中的資料。 例如，當您依月份比較公司中不同銷售人員的銷售資料時，您會希望月份能夠對齊。 如果員工四月份外出，該員工就沒有該月份的資料。 您希望看到該月份的間距，並且看到後續月份的資料對齊其他員工的資料。 您可以對齊水平軸達到這個目的。 如需詳細資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) 中關於走勢圖的章節，並參閱[在資料表或矩陣的圖表上對齊資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)。  
  
 同樣地，為了能夠跨資料列進行比較，資料也必須垂直對齊，也就是說，某個走勢圖或資料橫條中的橫條或線條高度必須相對於其他所有走勢圖或資料橫條中的橫條和線條高度。 否則，您無法互相比較資料列。  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 在這個影像中，直條圖會顯示每一個員工的每天銷售量。 請注意，如果是員工沒有任何銷售量的日子，圖表就會留下空白，並將後續的日子對齊。 這是水平對齊的範例。 同時也請注意，某些員工的每個橫條都很短，而且沒有任何橫條達到資料格的頂端。 這是垂直對齊的範例；如果沒有垂直對齊，在沒有高橫條的資料列中，短橫條便會延長，以填滿資料格的高度。  
  
##  <a name="UnderstandScope"></a> 了解提供給走勢圖或資料橫條的資料  
 當您將走勢圖或資料橫條加入至資料表或矩陣時，這表示將一個資料區放到另一個資料區內，成為 *「巢狀結構」* (Nesting)。 巢狀結構指的是提供給走勢圖或資料橫條的資料受到資料表或矩陣所依據的資料集，以及您將其放在資料表或矩陣中的位置所控制。 如需詳細資訊，請參閱 [巢狀資料區 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)。  
  
##  <a name="ConvertSparklinetoChart"></a> 將走勢圖或資料橫條轉換為完整的圖表  
 由於走勢圖和資料橫條只是一種圖表，因此，如果您決定要擁有完整的圖表功能，您可以以滑鼠右鍵按一下某個圖表，然後按一下 **[轉換成完整圖表]**，將該圖表轉換成完整的圖表。 當您這麼做時，便會自動加入軸線、標籤、刻度標記與圖例。  
  
> [!NOTE]  
>  您無法按一下滑鼠，就將完整的圖表轉換成走勢圖或資料橫條。 不過，您只要刪除不在走勢圖和資料橫條中的所有圖表元素，就可以從完整的圖表建立走勢圖或資料橫條。  
  
##  <a name="HowTo"></a> 如何主題  
 [加入走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
 [在資料表或矩陣的圖表上對齊資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs.md)  
  
### <a name="other-how-to-topics-for-charts"></a>圖表的其他如何主題  
 走勢圖和資料橫條都是一種圖表的類型，因此，您可能也會發現下列用於圖表的如何主題相當實用而且有關聯：  
  
 [將圖表加入至報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)  
  
 [將空點加入至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
 [加入或移除圖表中的邊界 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
 [變更圖表類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/change-a-chart-type-report-builder-and-ssrs.md)  
  
 [使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)  
  
 [在數列上顯示工具提示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)  
  
 [指定對數刻度 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)  
  
 [指定軸間隔 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
 [跨多個形狀圖指定一致的色彩 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>請參閱＜  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [教學課程：將走勢圖加入至報表 &#40;報表產生器&#41;](../../reporting-services/tutorial-add-a-sparkline-to-your-report-report-builder.md)   
  
  
