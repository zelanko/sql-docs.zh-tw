---
title: 將斜面、浮凸與紋理樣式新增至圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 34f69e4c8c1b62e01f8cb73e26f84d05e427a9ed
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581659"
---
# <a name="chart-effects---add-bevel-emboss-or-texture-report-builder"></a>圖表效果 - 新增斜面、浮凸或紋理 (報表產生器)
  使用某些圖表類型時，您可以指定繪製效果來增加圖表的視覺效果。 這些繪製效果僅適用於圖表的數列。 它們對於其他任何圖表元素沒有影響。  
  
 當您使用圓形圖或環圈圖的任何變數時，您可以指定類似於可以套用到影像之斜面或浮凸效果的柔邊或凹面繪製樣式。  
  
 當您使用橫條圖或直條圖的任何變數時，則可以將紋理樣式 (例如，圓柱、楔形和深淺) 套用到個別的橫條圖或直條圖。  
  
 除了這些繪製樣式之外，您也可以在許多圖表元素中加入框線和陰影，以提供深度的幻影。 如需其他格式化圖表方式的詳細資訊，請參閱 [格式化圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>若要將斜面或浮凸樣式加入至圓形圖或環圈圖  
  
1.  在 **[檢視]** 索引標籤上，選取 **[屬性]** 來開啟 [屬性] 窗格。  
  
2.  選取您要增強的圓形圖或環圈圖。 在圖表 (而非整個圖表) 中選取一個資料欄位。  
  
3.  在 [屬性] 窗格中，展開 **[CustomAttributes]** 節點。  
  
4.  為 PieDrawingStyle 從下拉式清單中選取一種樣式。  
  
> [!NOTE]  
>  在相同的圖表上，您無法同時擁有 3D 與斜面或浮凸樣式。 如果您已經啟用圖表的 3D 樣式，將無法看到 PieDrawingStyle 屬性。  
  
 ![具有凹面繪製樣式的圓形圖](../../reporting-services/report-design/media/rs-piedrawingeffects-concave.gif "具有凹面繪製樣式的圓形圖")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>若要將紋理樣式加入至橫條圖或直條圖  
  
1.  選取您要增強的橫條圖或直條圖。 在圖表 (而非整個圖表) 中選取一個資料欄位。  
  
2.  開啟 [屬性] 窗格。  
  
3.  展開 **CustomAttributes** 節點。  
  
4.  為 DrawingStyle 從下拉式清單中選取一種樣式。  
  
> [!NOTE]  
>  在相同的圖表上，您無法同時擁有 3D 與斜面或浮凸樣式。 如果您已經啟用圖表的 3D 樣式，將無法看到 PieDrawingStyle 屬性。  
  
 ![具有 LightToDark 繪製效果的橫條圖](../../reporting-services/report-design/media/rs-bardrawingeffects-lighttodark.gif "具有 LightToDark 繪製效果的橫條圖")  
  
## <a name="see-also"></a>另請參閱  
 [橫條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/bar-charts-report-builder-and-ssrs.md)   
 [直條圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/column-charts-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
