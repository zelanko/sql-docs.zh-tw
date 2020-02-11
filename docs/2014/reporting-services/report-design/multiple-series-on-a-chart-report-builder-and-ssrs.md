---
title: 圖表上的多個數列 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b99e4398-1fba-4824-958f-5c75d10485ea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 40c623130b02c082b099938823ccc12950333982
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105556"
---
# <a name="multiple-series-on-a-chart-report-builder-and-ssrs"></a>圖表上的多個數列 (報表產生器及 SSRS)
  當圖表上出現多個數列時，您必須決定比較數列的最好方式。 您可以使用堆疊圖表顯示每個數列的相關比例。 如果您只要比較共用共同類別目錄 (x) 軸的兩個數列，請使用副座標軸。 顯示兩個相關資料數列 (例如，價格和數量，或收入和稅額) 時，這相當實用。 如果圖表變成無法讀取，請考慮使用多個圖表區域，在每個數列之間建立更多視覺上的分隔。  
  
 除了使用圖表功能之外，決定哪種圖表類型應該用於您的資料也相當重要。 如果資料集中的欄位是相關的，請考慮使用範圍圖表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-stacked-and-100-stacked-charts"></a>使用堆疊與 100% 堆疊圖表  
 堆疊圖表通常用於顯示一個圖表區域中的多個數列。 當您嘗試顯示的資料緊密相關時，請考慮使用堆疊圖表。 在堆疊圖表上顯示四個 (包含) 以下的數列也是相當好的作法。 如果您要比較每個數列佔整體的比例，使用 100% 堆疊區域、長條圖或直條圖。 這些圖表會計算每個數列佔類別目錄的相對百分比。 如需詳細資訊，請參閱[區域圖 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)、[橫條圖 &#40;報表產生器及 SSRS&#41;](bar-charts-report-builder-and-ssrs.md) 和[直條圖 &#40;報表產生器及 SSRS&#41;](column-charts-report-builder-and-ssrs.md)。  
  
## <a name="using-the-secondary-axis"></a>使用副座標軸  
 當新的數列加入到圖表時，該數列會使用主要 x 和 y 軸繪製。 當您想要比較屬於不同測量單位的值時，請考慮使用 *「副座標軸」* (Secondary Axis)，讓您可以在個別的軸上繪製兩個數列。 在比較屬於不同測量單位的值時，副座標軸相當實用。 副座標軸繪製在主座標軸的另一側。 此圖表僅支援主座標軸和副座標軸。 副座標軸與主座標軸的屬性相同。 如需詳細資訊，請參閱[繪製副座標軸上的資料 &#40;報表產生器及 SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)。  
  
 如果您想要顯示兩個以上具有不同資料範圍的數列，請考慮將數列放在個別的圖表區域中。  
  
## <a name="using-chart-areas"></a>使用圖表區域  
 此圖表是最上層的容器，其中包含外框、圖表標題和圖例。 依預設，圖表包含一個預設的圖表區域。 在圖表介面上看不到圖表區域，但是您可以將圖表區域視為僅包含軸標籤、軸標題，以及一或多個數列之繪圖區的容器。 下圖顯示單一圖表內圖表區域的概念。  
  
 ![顯示圖表區域的圖表](../media/chartareasdiagram.gif "顯示圖表區域的圖表")  
  
 您可以使用 **[圖表區域屬性]** 對話方塊，指定包含在圖表區域中所有數列的 2D 和 3D 方向、對齊相同圖表內的多個圖表區域，以及格式化繪圖區的色彩。 在僅包含一個預設圖表區域的圖表上定義新的圖表區域時，圖表區域的可用空間會以水平方式分成兩個，而新的圖表區域放置在第一個圖表區域之下。  
  
 每個數列都只能連接到一個圖表區域。 依預設，所有數列都會加入到預設的圖表區域中。 使用區域圖、直條圖、折線圖和散佈圖時，這些數列的任何組合都可以顯示在相同的圖表區域中。 例如，您可以在相同的圖表區域中顯示資料行數列和線條數列。 針對多個數列使用相同圖表區域的優點是，使用者可以輕鬆進行比較。  
  
 長條圖、雷達圖和形狀圖無法與相同圖表區域中的其他任何圖表類型結合。 如果您要比較屬於長條圖、雷達圖或形狀圖類型的多個數列，您需要執行下列其中之一：  
  
-   將圖表區域中的所有數列變更為相同的圖表類型。  
  
-   建立新的圖表區域，然後將一或多個數列從預設的圖表區域移到新建立的圖表區域中。  
  
 如果您要嘗試比較具有不同值刻度的資料，單一圖表上的多個圖表區域功能也相當實用。 例如，如果第一個數列在 10 到 20 的範圍內包含資料，而第二個數列在 400 到 800 的範圍內包含資料，則第一個數列中的值可能會遭到遮蓋。 請考慮將每個數列分隔到不同的圖表區域中。 如需詳細資訊，請參閱[為數列指定圖表區域 &#40;報表產生器及 SSRS&#41;](specify-a-chart-area-for-a-series-report-builder-and-ssrs.md)。  
  
## <a name="using-range-charts"></a>使用範圍圖表  
 範圍圖表的每個資料點都有兩個值。 如果您的圖表包含共用相同類別目錄 (x) 軸的兩個數列，您可以使用範圍圖表顯示兩個數列間的差距。 範圍圖表最適合用於顯示高-低或上-下資訊。 例如，如果第一個數列包含一月每天的最高銷售額，而第二個數列包含一月每天的最低銷售額，則您可以使用範圍圖表顯示每天銷售額中，最高與最低間的差距。 如需詳細資訊，請參閱[範圍圖表 &#40;報表產生器及 SSRS&#41;](range-charts-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [在圖表上顯示具有多個資料範圍的數列 &#40;報表產生器和 SSRS&#41;](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)   
 [圖表類型 &#40;報表產生器及 SSRS&#41;](chart-types-report-builder-and-ssrs.md)  
  
  
