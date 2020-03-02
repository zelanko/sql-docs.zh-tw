---
title: 形狀圖 (報表產生器) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4b8404c1-aa89-4350-8bd6-203bc0446ee4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4e1d8d10837708b7cde4f83056a23a0e143662ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080990"
---
# <a name="shape-charts-report-builder-and-ssrs"></a>形狀圖 (報表產生器及 SSRS)
  形狀圖會將值資料顯示為整體所佔的百分比。 形狀圖通常用於顯示集合中不同值之間成比例的比較。 類別目錄是以個別的形狀區段表示。 區段的大小取決於值。 形狀圖在用途上類似於圓形圖，差別在於後者排序類別目錄時是從最大到最小。  
  
 漏斗圖會將值顯示為逐漸減少的比例。 區域的大小取決於所有值總計中所佔百分比的數列值。 例如，您可能會使用漏斗圖來顯示網站訪客的趨勢。 漏斗圖在頂端可能會顯示一個寬廣的區域，表示訪客點擊首頁的次數，而其他區域在比例上會比較小。 如需如何將資料加入漏斗圖中的詳細資訊，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)。  
  
 下圖顯示漏斗圖的範例。  
  
 ![漏斗圖](../../reporting-services/report-design/media/rs-funnelchart.gif "漏斗圖")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>變化  
  
-   **金字塔圖**： 金字塔圖會顯示成比例的資料，讓圖表看起來像金字塔一樣。  
  
## <a name="data-considerations-for-shape-charts"></a>形狀圖的資料考量  
  
-   形狀圖因為其視覺效果而在報表上相當普遍。 不過，形狀圖是非常簡化的圖表類型，在表示資料時可能不是最適合。 只有在資料已彙整為七個資料點 (含) 以下後，才考慮使用形狀圖。 一般而言，使用形狀圖只能在每個資料區域顯示一個類別目錄。  
  
-   形狀圖會將每個資料群組顯示為圖表的個別區段。 您至少必須加入一個資料欄位和一個類別目錄欄位。 如果將一個以上的資料欄位加入到形狀圖中，形狀圖將會在相同的圖表中同時顯示兩個資料欄位。  
  
-   形狀圖在按照排序順序顯示成比例的百分比時最有效。 不過，為了維持一致性，圖表預設不會排序資料集中的值。 若要最精確地將資料表示成漏斗圖或金字塔圖，請考慮從最高至最低排序值。 如需詳細資訊，請參閱 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)(將互動式排序加入資料表或矩陣 (報表產生器及 SSRS))。  
  
-   計算比例時，Null、空值、負值與零值沒有效用。 因此，這些值不會顯示在形狀圖上。 如果您要在圖表上，以視覺方式表示這些值的類型，請將圖表類型變更為形狀圖之外的其他類型。 如需如何將空點新增至非形狀圖中的詳細資訊，請參閱[將空點新增至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)。  
  
-   如果您要在形狀圖上使用自訂調色盤定義自己的色彩，請確認您的調色盤上有足夠的色彩，才能以其獨特的色彩反白顯示每個資料點。 如需詳細資訊，請參閱 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
-   形狀圖不像其他所有的圖表類型，它會在其圖例中顯示個別的資料點，而不會顯示個別的數列。  
  
-   漏斗圖會忽略值和類別目錄軸的設定。 如果您有多個類別目錄或序列群組，則群組標籤會在圖表圖例中顯示。  
  
-   形狀圖類型無法與相同圖表區域中的其他任何圖表類型結合。 如果您必須顯示形狀圖顯示之資料以及其他圖表類型顯示之資料間的比較，您必須加入另一個圖表區域。  
  
-   您可以在圓形圖和環圈圖上套用其他繪製樣式來增加視覺效果。 如需詳細資訊，請參閱[格式化圖表上的數列色彩 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
