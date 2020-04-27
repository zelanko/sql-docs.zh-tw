---
title: 極座標圖 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c9402d8f-202a-4cdf-949e-50f5b1d2b885
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a790f3951ce37e714346b8d280547e603cf48c23
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105446"
---
# <a name="polar-charts-report-builder-and-ssrs"></a>極座標圖 (報表產生器及 SSRS)
  極座標圖是在 360 度的圓形上，依據類別目錄群組，將數列顯示為一組點。 這些值是以點的長度 (從圓心開始測量) 表示。 從圓心到點的距離越遠，其值越大。 類別目錄標籤會顯示在圖表的周長上。 如需如何將資料新增至極座標圖的詳細資訊，請參閱 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>變化  
  
-   **雷達圖**： 雷達圖會將數列顯示為弧線或區域。 雷達圖不像極座標圖，不會根據極座標顯示資料。  
  
## <a name="data-considerations-for-polar-charts"></a>極座標圖的資料考量  
  
-   雷達圖適用於比較多個類別目錄資料的數列。  
  
-   極座標圖通常用於圖形的極線資料，其中每個資料點都是由角度和距離來決定。  
  
-   極座標圖無法與相同圖表區域中的其他任何圖表類型結合。  
  
## <a name="example"></a>範例  
 下列範例顯示如何使用雷達圖。 下表提供圖表的範例資料。  
  
|名稱|Sales|  
|----------|-----------|  
|灌木|61|  
|種子|78|  
|燈泡|60|  
|樹木|38|  
|花朵|81|  
  
 在此範例中，[名稱] 欄位放置在 [類別目錄群組] 區域中。 [銷售量] 欄位放置在 [值] 區域中。 當您放置 [銷售量] 欄位時，系統會自動彙總圖表的 [銷售量] 欄位。 雷達圖會根據 [銷售量] 欄位中的值個數，計算放置標籤的位置，例如，[銷售量] 欄位中包含 5 個值，因此會將標籤放置在圓形上 5 個等距離點的位置。 如果 [銷售量] 欄位包含 3 個值，則會將標籤放置在圓形上 3 個等距離點的位置。  
  
 下圖根據呈現的資料，顯示雷達圖的範例。  
  
 ![雷達圖](../media/rs-radarchart.gif "雷達圖")  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器和 SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](chart-types-report-builder-and-ssrs.md)   
 [折線圖 &#40;報表產生器及 SSRS&#41;](line-charts-report-builder-and-ssrs.md)   
 [圖表中的空白和 Null 資料點 &#40;報表產生器及 SSRS&#41;](empty-and-null-data-points-in-charts-report-builder-and-ssrs.md)  
  
  
