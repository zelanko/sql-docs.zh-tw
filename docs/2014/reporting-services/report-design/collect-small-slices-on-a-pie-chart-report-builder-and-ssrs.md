---
title: 收集圓形圖上的小配量 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: af1a270524d91621cdeb15b56ace7c07ad4a4df7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031802"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>收集圓形圖上的小配量 (報表產生器及 SSRS)
  當圓形圖顯示太多資料點時，看起來會很雜亂。 若要解決這個問題，您可以將落在特定值以下的所有資料顯示為圓形圖上的一個扇區。  
  
 若要將小扇區收集成一個扇區，請先決定收集小扇區的臨界值是以圓形圖的百分比或是以固定值表示。 然後設定 CollectedThreshold 和 CollectedThresholdUsePercent 屬性。將 CollectedThreshold 屬性設定為圖表百分比 (值必須落在這個值以下才會被收集)，或是集合的實際臨界值資料值。 將 CollectedThresholdUsePercent 屬性設定為`True`以使用百分比或`False`使用實際的值。  
  
 您也可以將小扇區收集成第二個圓形圖，此圖會成為第一個圓形圖的收集扇區的註標。 第二個圓形圖會繪製在原始圓形圖的右方。  
  
 您不能將漏斗圖或金字塔圖的扇區結合成一個扇區。  
  
 此圖表的範例可從範例報表取得。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][報表產生器與報表設計師範例報表](http://go.microsoft.com/fwlink/?LinkId=198283)。  
  
### <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>將小配量收集成圓形圖上的單一配量  
  
1.  開啟 [屬性] 窗格。  
  
2.  在設計介面上按一下圓形圖的任何配量。 數列的屬性會顯示在 [屬性] 窗格中。  
  
3.  在 [一般]  區段中，展開 [CustomAttributes]  節點。  
  
4.  將 CollectedStyle 屬性設定為 **SingleSlice**。  
  
5.  設定收集的臨界值及臨界值類型。 下列範例是設定收集臨界值的常見方式。  
  
    -   **依百分比。** 例如，將圓形圖上少於 10% 的任何扇區收集成單一扇區：  
  
         將 CollectedThresholdUsePercent 屬性設定為`True`。  
  
         將 CollectedThreshold 屬性設定為 **10**。  
  
        > [!NOTE]  
        >  如果您將 [collectedstyle] 設定為**SingleSlice**，大於值 CollectedThreshold **100**，而且 CollectedThresholdUsePercent `True`，圖表會擲回例外狀況，因為它無法計算百分比。 若要解決此問題，請將 CollectedThreshold 設定為小於 **100** 的值。  
  
    -   **依資料值。** 例如，將圓形圖上小於 5000 的任何扇區收集成單一扇區：  
  
         將 CollectedThresholdUsePercent 屬性設定為`False`。  
  
         將 CollectedThreshold 屬性設定為 **5000**。  
  
6.  將 CollectedLabel 屬性設為字串，代表會在收集的扇形區上顯示的文字標籤。  
  
7.  (選擇性) 設定 CollectedSliceExploded、CollectedColor、CollectedLegendText 和 CollectedToolTip 屬性。 這些屬性會變更單一扇區的外觀、色彩、標籤文字、圖例文字及工具提示層面。  
  
### <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>將小扇區收集成次要的註標圓形圖  
  
1.  請遵循上述步驟 1 - 3。  
  
2.  將 CollectedStyle 屬性設定為 **CollectedPie**。  
  
3.  將 CollectedThresholdproperty 設為一個代表臨界值的值，達到該值時小扇形區會收集為一個扇形區。 當 [collectedstyle] 屬性設定為**CollectedPie**，CollectedThresholdUsePercentproperty 一定會設定為`True`，而收集臨界值永遠會以百分比測量。  
  
4.  (選擇性) 設定 CollectedColor、CollectedLabel、CollectedLegendText 和 CollectedToolTip 屬性。 所有其他名為 "Collected" 的屬性都不適用於收集的圓形圖。  
  
> [!NOTE]  
>  次要的圓形圖會根據資料中的小扇區而計算，所以只會顯示在預覽中， 而不會出現在設計介面上。  
  
> [!NOTE]  
>  您無法格式化次要圓形圖。 因為這個緣故，所以我們強烈建議您在收集圓形圖扇區時使用第一種方法。  
  
## <a name="see-also"></a>另請參閱  
 [圓形圖&#40;報表產生器和 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [格式化圖表上的資料點&#40;報表產生器和 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [在圓形圖外部顯示資料點標籤&#40;報表產生器和 SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [在圓形圖上顯示百分比值 &#40;報表產生器和 SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)   
 [將 3D 效果新增至圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-3d-effects-report-builder.md)  
  
  