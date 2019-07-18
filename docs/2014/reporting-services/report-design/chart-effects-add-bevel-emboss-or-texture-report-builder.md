---
title: 將斜面、浮凸與紋理樣式新增至圖表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 737cfc80-b39e-497c-817b-b46693deb58f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b25d12646a2662cb5c6ab8f2a9b510aa02d7c49b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106274"
---
# <a name="add-bevel-emboss-and-texture-styles-to-a-chart-report-builder-and-ssrs"></a>將斜面、浮凸與紋理樣式加入至圖表 (報表產生器及 SSRS)
  使用某些圖表類型時，您可以指定繪製效果來增加圖表的視覺效果。 這些繪製效果僅適用於圖表的數列。 它們對於其他任何圖表元素沒有影響。  
  
 當您使用圓形圖或環圈圖的任何變數時，您可以指定類似於可以套用到影像之斜面或浮凸效果的柔邊或凹面繪製樣式。  
  
 當您使用橫條圖或直條圖的任何變數時，則可以將紋理樣式 (例如，圓柱、楔形和深淺) 套用到個別的橫條圖或直條圖。  
  
 除了這些繪製樣式之外，您也可以在許多圖表元素中加入框線和陰影，以提供深度的幻影。 如需其他格式化圖表方式的詳細資訊，請參閱 [格式化圖表 &#40;報表產生器及 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-bevel-or-emboss-styles-to-a-pie-or-doughnut-chart"></a>若要將斜面或浮凸樣式加入至圓形圖或環圈圖  
  
1.  在 **[檢視]** 索引標籤上，選取 **[屬性]** 來開啟 [屬性] 窗格。  
  
2.  選取您要增強的圓形圖或環圈圖。 在圖表 (而非整個圖表) 中選取一個資料欄位。  
  
3.  在 [屬性] 窗格中，展開 **[CustomAttributes]** 節點。  
  
4.  為 PieDrawingStyle 從下拉式清單中選取一種樣式。  
  
> [!NOTE]  
>  在相同的圖表上，您無法同時擁有 3D 與斜面或浮凸樣式。 如果您已經啟用圖表的 3D 樣式，將無法看到 PieDrawingStyle 屬性。  
  
 ![具有凹面繪製樣式的圓形圖](../media/rs-piedrawingeffects-concave.gif "具有凹面繪製樣式的圓形圖")  
  
### <a name="to-add-texture-styles-to-a-bar-or-column-chart"></a>若要將紋理樣式加入至橫條圖或直條圖  
  
1.  選取您要增強的橫條圖或直條圖。 在圖表 (而非整個圖表) 中選取一個資料欄位。  
  
2.  開啟 [屬性] 窗格。  
  
3.  展開 **CustomAttributes** 節點。  
  
4.  為 DrawingStyle 從下拉式清單中選取一種樣式。  
  
> [!NOTE]  
>  在相同的圖表上，您無法同時擁有 3D 與斜面或浮凸樣式。 如果您已經啟用圖表的 3D 樣式，將無法看到 PieDrawingStyle 屬性。  
  
 ![具有 LightToDark 繪製效果的橫條圖](../media/rs-bardrawingeffects-lighttodark.gif "具有 LightToDark 繪製效果的橫條圖")  
  
## <a name="see-also"></a>另請參閱  
 [橫條圖 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [直條圖 &#40;報表產生器及 SSRS&#41;](column-charts-report-builder-and-ssrs.md)   
 [圓形圖 &#40;報表產生器及 SSRS&#41;](pie-charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器及 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)  
  
  
