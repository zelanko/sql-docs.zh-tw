---
title: 收集圓形圖上的小配量 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 21c2b8cb-b9ca-4bc0-bf49-50ba432562f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 62c7edcc017dfd43801a2c637f70204075ccb301
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289436"
---
# <a name="collect-small-slices-on-a-pie-chart-report-builder-and-ssrs"></a>收集圓形圖上的小配量 (報表產生器及 SSRS)
配量太多的圓形圖看起來很雜亂。 了解在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中將圓形圖中的許多小配量收集成一個單一配量。
 
 若要將小扇區收集成一個扇區，請先決定收集小扇區的臨界值是以圓形圖的百分比或是以固定值表示。 
 
 [教學課程：將圓形圖新增至報表 (報表產生器)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) 會引導您將許多小配量收集成單一配量 (若您想要先使用範例資料嘗試此功能的話)。
 
 ![report-builder-pie-chart-other-slice](../../reporting-services/report-design/media/report-builder-pie-chart-other-slice.png)
  
 您也可以將小扇區收集成第二個圓形圖，此圖會成為第一個圓形圖的收集扇區的註標。 第二個圓形圖會繪製在原始圓形圖的右方。  
  
 您不能將漏斗圖或金字塔圖的扇區結合成一個扇區。  
  
 
## <a name="to-collect-small-slices-into-a-single-slice-on-a-pie-chart"></a>將小配量收集成圓形圖上的單一配量  
  
1.  開啟 [屬性] 窗格。  
  
2.  在設計介面上按一下圓形圖的任何配量。 數列的屬性會顯示在 [屬性] 窗格中。  
  
3.  在 [一般]  區段中，展開 [CustomAttributes]  節點。  
  
4.  將 CollectedStyle 屬性設定為 **SingleSlice**。  

    ![report-builder-pie-chart-single-slice-property](../../reporting-services/media/report-builder-pie-chart-single-slice-property.png)
  
5.  設定收集的臨界值及臨界值類型。 下列範例是設定收集臨界值的常見方式。  
  
    -   **依百分比。** 例如，將圓形圖上少於 10% 的任何扇區收集成單一扇區：  
  
         將 CollectedThresholdUsePercent 屬性設定為 **True**。  
  
         將 CollectedThreshold 屬性設定為 **10**。  
  
        > [!NOTE]  
        >  如果將 CollectedStyle 設定為 **SingleSlice**、將 CollectedThreshold 設定為大於 **100** 的值，且將 CollectedThresholdUsePercent 設定為 **True**，則圖表會擲回例外狀況；因為它無法計算百分比。 若要解決此問題，請將 CollectedThreshold 設定為小於 **100** 的值。  
  
    -   **依資料值。** 例如，將圓形圖上小於 5000 的任何扇區收集成單一扇區：  
  
         將 CollectedThresholdUsePercent 屬性設定為 **False**。  
  
         將 CollectedThreshold 屬性設定為 **5000**。  
  
6.  將 CollectedLabel 屬性設為字串，代表會在收集的扇形區上顯示的文字標籤。  
  
7.  (選擇性) 設定 CollectedSliceExploded、CollectedColor、CollectedLegendText 和 CollectedToolTip 屬性。 這些屬性會變更單一扇區的外觀、色彩、標籤文字、圖例文字及工具提示層面。  
  
## <a name="to-collect-small-slices-into-a-secondary-callout-pie-chart"></a>將小扇區收集成次要的註標圓形圖  
  
1.  請遵循上述步驟 1 - 3。  
  
2.  將 CollectedStyle 屬性設定為 **CollectedPie**。  
  
3.  將 CollectedThresholdproperty 設為一個代表臨界值的值，達到該值時小扇形區會收集為一個扇形區。 當 CollectedStyle 屬性設為 **CollectedPie**時，CollectedThresholdUsePercentproperty 屬性一律會設定為 **True**，而收集臨界值一律會以百分比測量。  
  
4.  (選擇性) 設定 CollectedColor、CollectedLabel、CollectedLegendText 和 CollectedToolTip 屬性。 所有其他名為 "Collected" 的屬性都不適用於收集的圓形圖。  
  
> [!NOTE]  
>  次要的圓形圖會根據資料中的小扇區而計算，所以只會顯示在預覽中， 而不會出現在設計介面上。  
  
> [!NOTE]  
>  您無法格式化次要圓形圖。 因為這個緣故，所以我們強烈建議您在收集圓形圖扇區時使用第一種方法。  
  
## <a name="see-also"></a>另請參閱  
* [教學課程：將圓形圖新增至報表 (報表產生器)](Tutorial:%20Add%20a%20Pie%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
*  [格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
*  [在圓形圖外部顯示資料點標籤 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
*  [在圓形圖上顯示百分比值 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)     
  
