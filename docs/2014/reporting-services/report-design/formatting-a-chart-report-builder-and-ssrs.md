---
title: 將圖表格式化 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10214"
- sql12.rtp.rptdesigner.calculatedseriesproperties.fill.f1
- sql12.rtp.rptdesigner.serieslabelproperties.fill.f1
- sql12.rtp.rptdesigner.legendproperties.fill.f1
- "10149"
- sql12.rtp.rptdesigner.seriesproperties.shadow.f1
- sql12.rtp.rptdesigner.seriesproperties.markers.f1
- "10255"
- sql12.rtp.rptdesigner.charttitleproperties.fill.f1
- "10154"
- "10170"
- "10173"
- sql12.rtp.rptdesigner.seriesproperties.fill.f1
- "10169"
- "10158"
- sql12.rtp.rptdesigner.chartareaproperties.fill.f1
- sql12.rtp.rptdesigner.charttitleproperties.shadow.f1
- "10246"
- "10150"
- sql12.rtp.rptdesigner.calculatedseriesproperties.borders.f1
- sql12.rtp.rptdesigner.chartproperties.fill.f1
- "10159"
- sql12.rtp.rptdesigner.majorgridlineproperties.gridlineoptions.f1
- "10160"
- sql12.rtp.rptdesigner.serieslabelproperties.font.f1
- "10182"
- "10163"
- "10164"
- "10253"
- "10216"
- "10171"
- "10257"
- sql12.rtp.rptdesigner.chartareaproperties.border.f1
- sql12.rtp.rptdesigner.calculatedseriesproperties.shadow.f1
- sql12.rtp.rptdesigner.chartproperties.border.f1
- sql12.rtp.rptdesigner.minorgridlineproperties.gridlineoptions.f1
- sql12.rtp.rptdesigner.chartareaproperties.shadow.f1
- sql12.rtp.rptdesigner.charttitleproperties.borders.f1
- sql12.rtp.rptdesigner.charttitleproperties.font.f1
- "10247"
ms.assetid: d3984300-c766-42f8-b7c4-863123d67c99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: af164d4db9b6439f0634d113652b95939827b0f5
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105862"
---
# <a name="formatting-a-chart-report-builder-and-ssrs"></a>格式化圖表 (報表產生器及 SSRS)
  在定義了圖表的資料且資料也以所要的方式顯示之後，您就可以加入格式設定，以改善整體外觀並強調關鍵的資料點。 您可以從 [屬性] 對話方塊修改最常見的格式設定選項，當您以滑鼠右鍵按一下圖表元素以顯示其快速鍵功能表時，此對話方塊就會顯示。 每個圖表元素都有它自己的對話方塊。 如需圖表元素的詳細資訊，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
 所有與圖表相關的屬性都位在 [屬性] 窗格中，但其中許多屬性也可以從對話方塊進行設定。 如果要格式化數列，可以使用自訂屬性 (attribute) 來指定數列特定的屬性 (property)，您只能在 [屬性]\(property) 窗格的 **CustomAttributes** 屬性類別目錄中才能找到這些自訂屬性。  
  
 若要使用最少的步驟有效地進行圖表的格式化，請變更預設的框線樣式、調色盤和繪製樣式。 這三個功能會在圖表上產生最多的可見變更。 繪製樣式只適用於圓形圖、環圈圖、橫條圖和直條圖。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="in-this-section"></a>本節內容  
 [設定圖表上數列色彩的格式 &#40;報表產生器及 SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)  
 討論如何使用調色盤定義顏色、如何定義自己的調色盤，以及如何根據運算式定義顏色。  
  
 [格式化圖表上的軸標籤 &#40;報表產生器及 SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)  
 討論如何顯示格線、刻度及標題，以及如何格式化軸刻度上的數字和日期。  
  
 [在圖表上格式化圖例 &#40;報表產生器及 SSRS&#41;](chart-legend-formatting-report-builder.md)  
 討論如何重新排列及格式化圖表圖例中的項目。  
  
 [格式化圖表上的資料點 &#40;報表產生器及 SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
 討論如何針對圖表上的每個數列放置資料點標籤及格式化資料點標記。  
  
 [圖表中的 3D、浮凸和其他效果 &#40;報表產生器及 SSRS&#41;](chart-effects-3d-bevel-and-other-report-builder.md)  
 討論可套用到圖表的各種 3D 效果。  
  
 [將邊框加入至圖表 &#40;報表產生器及 SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)  
 說明如何將邊框加入至圖表。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [將邊框新增至圖表 &#40;報表產生器及 SSRS&#41;](add-a-border-frame-to-a-chart-report-builder-and-ssrs.md)   
 [使用調色盤定義圖表的色彩 &#40;報表產生器及 SSRS&#41;](define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [將斜面、浮凸與紋理樣式新增至圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  
