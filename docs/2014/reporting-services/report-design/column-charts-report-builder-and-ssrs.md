---
title: 直條圖 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae8c138b-e356-4ad8-862c-a4a8d0c04149
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9c706bceb09d8637874bc82a5c23a1afa8380034
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56292964"
---
# <a name="column-charts-report-builder-and-ssrs"></a>Column Charts (Report Builder and SSRS)
  直條圖是依據類別目錄群組，將數列顯示為一組垂直線。 直條圖適合顯示一段時間的資料變更，或圖解項目之間的比較。 一般直條圖與橫條圖相當有關聯，後者會將數列顯示為一組水平橫條，而範圍直條圖則會將數列顯示為一組垂直線，其中包含各種起點與終點。 如需詳細資訊，請參閱 [橫條圖 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md) 和 [範圍圖表 &#40;報表產生器及 SSRS&#41;](range-charts-report-builder-and-ssrs.md)。  
  
 直條圖非常適合這個資料，因為全部三個數列都共用一個共同的時間週期，以便進行有效的比較。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations-of-a-column-chart"></a>直條圖的變化  
  
-   **堆疊**： 將多個數列垂直堆疊的直條圖。 如果您的圖表中只有一個數列，堆疊直條圖的顯示將與直條圖相同。  
  
-   **百分之百堆疊**： 將多個數列垂直堆疊以便百分之百符合圖表區域的直條圖。 如果您的圖表中只有一個數列，所有直條圖都會百分之百符合圖表區域。  
  
-   **立體群組**： 以立體圖表的個別資料列顯示各個數列的直條圖。  
  
-   **立體圓柱圖**： 其直條形狀類似立體圖表圓柱的直條圖。  
  
-   `Histogram`. 圖表會執行計算，讓其直條以常態分佈排列的直條圖。  
  
-   `Pareto`. 其直條從高而低排列的直條圖。  
  
## <a name="data-considerations-for-a-column-chart"></a>直條圖的資料考量  
  
-   橫條圖與直條圖通常用於顯示群組之間的比較。 如果在圖表上出現三個以上的數列，請考慮使用堆疊橫條圖或直條圖。 如果在圖表上有多個數列，您也可以將堆疊橫條圖或直條圖收集到多個群組中。 如需詳細資訊，請參閱 <<c0> [ 橫條圖&#40;報表產生器及 SSRS&#41; ](charts-report-builder-and-ssrs.md)並*直條圖*。</c0>  
  
-   在直條圖中，用於水平顯示類別目錄軸標籤的空間較少。 如果您的類別目錄標籤比較長，請考慮使用橫條圖，或變更標籤的旋轉角度。  
  
-   您可以在直條圖的個別直條上加入特殊的繪製樣式來增加其視覺效果。 繪製樣式包括楔形、浮凸、圓柱及深淺。 這些效果的設計可以改善平面圖表的外觀。 如果要使用立體圖表，您仍然可以套用繪製樣式，但是可能不會有相同的效果。 如需如何將繪製樣式加入橫條圖的詳細資訊，請參閱 [將斜面、浮凸與紋理樣式加入至圖表 &#40;報表產生器及 SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)。  
  
-   直條圖的特點是，可以將您的圖表顯示為長條圖或帕累托圖。 若要這樣做，請將 ShowColumnAs 屬性設定為`Histogram`或是`Pareto`到 [屬性] 視窗中`true`。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [橫條圖 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [範圍圖表 &#40;報表產生器及 SSRS&#41;](range-charts-report-builder-and-ssrs.md)   
 [教學課程：橫條圖加入至報表&#40;報表產生器&#41;](../tutorial-add-a-bar-chart-to-your-report-report-builder.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
