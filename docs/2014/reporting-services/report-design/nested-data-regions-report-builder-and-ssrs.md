---
title: 巢狀資料區域 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 15c2bc9b-428a-47ac-9630-8dde925d0595
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 58d065632faae49515217fdb9811430188b0f784
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210798"
---
# <a name="nested-data-regions-report-builder-and-ssrs"></a>巢狀資料區 (報表產生器及 SSRS)
  您可以在一個資料區域 (例如矩陣) 內巢狀另一個資料區域 (例如圖表)，這樣通常可以透過精確的方式顯示資料摘要，或提供視覺化顯示以及資料表或矩陣顯示。  
  
 例如，針對包含以 Store 資料列和 Quarter 資料行分組之銷售訂單的矩陣 (也稱為 *Tablix*) 資料區域，您可以將資料表或圖表加入到邊角資料格來摘要所有商店的銷售額，或將圖表加入到矩陣資料行標頭，將資料在資料行中的銷售比重顯示為所有銷售額的百分比。  
  
 ![rs_NestedDataRegion](../media/rs-nesteddataregion.gif "rs_NestedDataRegion")  
  
 在此圖中，邊角資料格中的圓形圖和資料列中的走勢圖都是巢狀資料區域。  
  
 根據定義，巢狀資料區域是以相同的報表資料集為基礎。 您無法巢狀以不同資料集為基礎的資料區域。 若要顯示來自不同資料集的資料，請考慮使用鑽研報表或子報表。 如需詳細資訊，請參閱[鑽研、向下鑽研、子報表和巢狀資料區 &#40;報表產生器及 SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-scope-for-a-nested-data-region"></a>了解巢狀資料區域的範圍  
 資料在巢狀資料區域中的範圍會透過其在父資料區域中的放置位置自動定義。 例如，在 Tablix 邊角資料格中巢狀之圖表的資料範圍為套用資料集、Tablix 資料區與圖表資料區域的篩選後，繫結至 Tablix 資料區之資料集中的資料。 在 Tablix 資料格中巢狀之 Tablix 的範圍與邊角資料格的範圍相同，但是會在套用對應群組篩選的情況下，產生所巢狀資料格之資料列和資料行群組成員資格的額外範圍。 如需範圍的詳細資訊，請參閱[總計、彙總與內建集合的運算式範圍 &#40;報表產生器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 下列清單描述資料格在下列 Tablix 區域中的範圍：  
  
-   **Tablix 邊角** ：此範圍為套用資料集和外部 Tablix 的篩選與排序運算式後，連結至 Tablix 資料區域之資料區域中的資料。  
  
-   **Tablix 資料行群組** ：套用資料集、外部 Tablix 與資料行群組的篩選與排序運算式後，最內部資料行群組中的資料。  
  
-   **Tablix 資料列群組** ：套用資料集、外部 Tablix 與資料列群組的篩選與排序運算式後，最內部資料列群組中的資料。  
  
-   **Tablix 主體** ：套用資料集、外部 Tablix 與資料列和資料行群組的篩選與排序運算式後，最內部群組中以資料列群組和資料行群組之交集表示的資料。  
  
 如需詳細資訊，請參閱 [Tablix 資料區的區域 &#40;報表產生器及 SSRS&#41;](tablix-data-region-areas-report-builder-and-ssrs.md)。  
  
## <a name="nesting-a-chart-sparkline-or-data-bar-in-a-tablix"></a>將圖表、走勢圖或資料橫條以巢狀方式置於 Tablix 中  
 當您將圖表 (包括走勢圖或資料橫條) 加入到 Tablix 資料行群組頭或群組尾資料列時，或加入到 Tablix 主體資料格時，傳遞到圖表中的資料範圍為該資料格的資料子集。 根據預設，當您將圖表加入到 Tablix 資料格時，圖表維度會擴充以填滿資料格。  
  
> [!NOTE]  
>  為能更佳掌控 Tablix 資料格中的圖表大小，先將圖表加入到矩形中，然後將矩形加入到 Tablix 資料格中。  
  
 根據預設，圖表圖例色彩取決於圖表數列中資料點的色彩。 若要控制色彩，讓巢狀圖表資料區域針對相同的資料類別目錄，全部使用相同的色彩，您必須使用自訂色彩，並針對資料設定排序運算式。 如需詳細資訊，請參閱[跨多個形狀圖指定一致的色彩 &#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md) 和[在資料區域中排序資料 &#40;報表產生器和 SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)。  
  
## <a name="nesting-a-gauge-or-an-indicator-in-a-tablix"></a>將量測計或指標以巢狀方式置於 Tablix 中  
 您可以在資料表、矩陣或清單內部巢狀量測計或指標，藉以顯示關鍵效能指標 (KPI)。 當您在資料表內部放置量測計或指標時，會出現在 Tablix 的每個資料列中。 如需將指標新增 Tablix 的詳細資訊，請參閱[指標 &#40;報表產生器和 SSRS&#41;](indicators-report-builder-and-ssrs.md)。  
  
### <a name="adding-a-gauge-to-a-tablix"></a>將量測計加入到 Tablix  
 將量測計加入到 Tablix 資料區域有兩種方式：  
  
-   按一下 Tablix 資料格內部，然後插入量測計。 **[選取量測計類型]** 對話方塊隨即出現。 選取量測計類型後，量測計資料區域就會放置在選取的 Tablix 資料格內部。 您可能需要調整 Tablix 的大小，才能設定量測計格式。  
  
-   按一下資料表外部，然後插入量測計。 **[選取量測計類型]** 對話方塊隨即出現。 選取量測計類型後，量測計資料區域就會放置在報表的左上角。 加入資料並設定此量測計格式之後，將其拖放到 Tablix 資料格內部。  
  
 如同圖表般，傳遞到量測計中的資料集範圍為該資料格的資料子集。 當量測計放置在 Tablix 資料格內部之後，量測計永遠只會彙總一個資料列。  
  
 當 Tablix 中的資料包含群組時，Tablix 內部巢狀的量測計資料區域不會自動繼承此群組。 您必須將相符的群組運算式加入到量測計中，才能顯示 Tablix 上所顯示的相同資訊。 例如，如果 Tablix 中的資料依 Product 分組，您必須將 Product 群組運算式加入到量測計，才能顯示相同的資料。 如需詳細資訊，請參閱[量測計 &#40;報表產生器和 SSRS&#41;](gauges-report-builder-and-ssrs.md) 和[在資料區中新增或刪除群組 &#40;報表產生器和 SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
 您必須設定將會顯示在量測計標尺上的最小值與最大值。 若要指定量測計的最大值，您可以使用運算式，例如 `=Max!MyField.Value`。 不過，因為此運算式僅會在資料格中資料的範圍內進行評估，對於 Tablix 中的所有資料列而言，每個量測計的最大值都不會相同。 這在 Tablix 中的量測計間進行比較時，可能會更難以了解。 或者，您可以為最大值指定一個靜態值。 Tablix 內部的所有資料列都會顯示包含此最大值的量測計。 如需詳細資訊，請參閱[設定量測計的最小值或最大值 &#40;報表產生器和 SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md)。  
  
 如果量測計上的資料變得太大，請考慮使用標尺乘數減少所顯示的位數。 若要指定乘數，您可以用滑鼠右鍵按一下標尺，然後選取 [標尺屬性]。 當 **[標尺屬性]** 對話方塊開啟時，針對 **[乘數]** 指定一個值。  
  
## <a name="nesting-a-table-or-matrix-and-a-chart-in-a-list"></a>在清單中巢狀資料表或矩陣與圖表  
 若要在清單中巢狀多個資料區域，請先加入矩形，然後將資料區域加入到該矩形中。  
  
 您可以針對清單資料區域定義一個群組，然後加入 Tablix 和圖表，就可以提供相同資料的不同檢視。 若要達成這個效果，您必須針對內嵌的 Tablix 和圖表，定義相同的群組與排序運算式。 根據定義，Tablix 和圖表會使用來自父清單資料區域之資料集的資料。  
  
> [!NOTE]  
>  依預設，當您將清單資料區域加入到設計介面時，該清單包含一個詳細資料列。 您可以加入群組資料列並移除詳細資料列來變更此預設值。 如需詳細資訊，請參閱[探索 Tablix 資料區的彈性 &#40;報表產生器及 SSRS&#41;](exploring-the-flexibility-of-a-tablix-data-region-report-builder-and-ssrs.md)。  
  
 如需詳細資訊，請參閱[了解群組 &#40;報表產生器和 SSRS&#41;](understanding-groups-report-builder-and-ssrs.md) 和[新增、移動或刪除資料表、矩陣或清單 &#40;報表產生器和 SSRS&#41;](add-move-or-delete-a-table-matrix-or-list-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [篩選、分組和排序資料 &#40;報表產生器及 SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [清單 &#40;報表產生器及 SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [量測計&#40;報表產生器及 SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [運算式 &#40;報表產生器及 SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [設定報表項目的格式 &#40;報表產生器及 SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)   
 [教學課程：將 KPI 新增至報表 &#40;報表產生器&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md)   
 [格式化量測計的標尺&#40;報表產生器及 SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)  
  
  
