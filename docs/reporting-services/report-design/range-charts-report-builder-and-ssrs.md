---
title: "範圍圖表 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 48e351d3-ac5b-4eda-a4bd-32a0de206a30
caps.latest.revision: "5"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 3a78c52aacd68919cf6cd3a07bb05da319468ce6
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="range-charts-report-builder-and-ssrs"></a>範圍圖表 (報表產生器及 SSRS)
  範圍圖表類型會顯示一組資料點，每個點都是由相同類別的多個值所定義。 這些值會以值軸所測量的標記高度來表示。 類別標籤會顯示在類別軸上。 一般範圍圖表會針對每個資料點，填滿上界值和下界值之間的區域。  
  
 下圖顯示的是包含三個數列的一般範圍圖表。  
  
 ![範圍圖表](../../reporting-services/report-design/media/rs-rangechart.gif "範圍圖表")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>變數  
  
-   **平滑範圍圖表**： 平滑範圍圖表會顯示曲線而不是直線。  
  
-   **資料行範圍**： 資料行範圍圖表會使用資料行 (而非區域) 來顯示範圍。  
  
-   **橫條範圍**： 橫條範圍圖表會使用橫條 (而非區域) 來顯示範圍。  
  
## <a name="data-considerations-for-range-charts"></a>範圍圖表的資料考量  
  
-   範圍圖表類型的每個資料點都需要兩個值。 這些值會與定義每個資料點範圍的最高值和最低值相對應。  
  
-   只有在上界值永遠高於下界值時，範圍圖表才適用於分析。 否則，請考慮使用折線圖。 如果最高值低於最低值，範圍圖表將會顯示這些值之間之差異的絕對值。  
  
-   如果只有指定一個值，範圍圖表將會當做一般區域圖表顯示，其中每個資料點都有一個值。  
  
-   範圍圖表通常用於圖形資料，其中資料集中包含每個類別目錄群組的最小值與最大值。  
  
-   在範圍圖表上，不支援顯示每個資料點的標記。  
  
-   如果在多個數列中的值相似，這些數列將會重疊，就像一般範圍圖表中的區域圖表一樣。 在此狀況下，您可能會想要使用資料行範圍圖表或橫條範圍圖表，而非一般範圍圖表。  
  
-   甘特圖可以使用範圍橫條圖建立。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [格式化圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)  
  
  
