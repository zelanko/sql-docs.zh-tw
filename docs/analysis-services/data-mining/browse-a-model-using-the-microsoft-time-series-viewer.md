---
title: 瀏覽模型，使用 Microsoft 時間序列檢視器 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd57ae140adee0909c0f00647a334bd62f26c170
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62671336"
---
# <a name="browse-a-model-using-the-microsoft-time-series-viewer"></a>使用 Microsoft 時間序列檢視器瀏覽模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 時間序列檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法建立的採礦模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列演算法是一種迴歸演算法，在預測狀況下用來建立資料採礦模型，以預測連續的資料行，例如產品銷售。 這些時間序列模型可依照不同的演算法而包含資訊：  
  
-   ARTxp 演算法 (已針對短期預測而最佳化)。  
  
-   ARIMA 演算法 (已針對長期預測而最佳化)。  
  
-   混用 ARTxp 和 ARIMA 演算法。  
  
 如需這些演算法的詳細資訊，請參閱 [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md) 和 [Microsoft 時間序列演算法技術參考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
> [!NOTE]  
>  若要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
##  <a name="BKMK_ViewerTabs"></a> 檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時間序列檢視器會提供下列索引標籤：  
  
-   [模型](#BKMK_Tree)  
  
-   [圖表](#BKMK_Charts)  
  
 **注意**：模型內容以及採礦圖例中所顯示的資訊，會依模型所使用的演算法而異。 不過，不論使用了哪些演算法，[模型]  和 [圖表]  索引標籤都相同。  
  
###  <a name="BKMK_Tree"></a> 模型  
 在建立時間序列模型時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將完成的模型顯示為樹狀結構。 如果資料包含多個案例序列， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會針對每個序列建立個別的樹狀結構。 例如，假設您要針對太平洋、北美及歐洲地區預測銷售量， 每一個地區的預測都是案例數列。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會針對每個數列建立個別的樹狀結構。 若要檢視特定的序列，請從 [樹狀結構]  清單選取序列。  
  
 在時間序列模型中，會針對每個樹狀結構包含一個 [全部]  節點，這個節點會再進一部分割成一序列的節點，代表演算法所發現的週期性結構。 您可以按一下每個節點，即可顯示案例及方程式數目等統計資料。  
  
 如果僅使用 ARTxp 建立模型，則根節點的 [採礦圖例]  僅會包含案例總數。 對於每個非根的節點，[採礦圖例]  則會包含更多有關樹狀結構分岔的詳細資訊：例如，採礦圖例會顯示節點方程式和案例數目。 圖例中的「規則」  包含識別規則所適用之數列及時間配量的資訊。 例如，圖例文字 `M200 Europe Amount -2` 表示此節點代表 M200 Europe 數列的模型，其週期為兩個時間配量前。  
  
 如果僅使用 ARIMA 建立模型，則 [模型]  索引標籤會包含具有 [全部]  標題的單一節點。 根節點的 [採礦圖例]  包含 ARIMA 方程式。  
  
 如果建立了混合的模型，則根節點僅包含案例數和 ARIMA 方程式。 在根節點之後，樹狀結構會針對週期性的結構分岔成個別的節點。 對於每個非根的節點，採礦圖例會包含 ARTxp 和 ARIMA 演算法、節點的方程式以及節點中的案例數。 ARTxp 方程式會先列出，並標示為樹狀節點方程式。 後面則接著 ARIMA 方程式。 如需如何解譯此資訊的詳細資訊，請參閱 [Microsoft 時間序列演算法技術參考](../../analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
 一般而言，決策樹圖形會在檢視器的左側顯示最重要的分岔：[全部]  節點。 在決策樹中，[全部]  節點之後的分岔最重要，因為它包含的條件最能分隔定型資料中的案例。 在時間序列模型中，主要分支代表最可能的季節週期。 在 [全部]  節點之後的分岔會出現在分支的右側。  
  
 您可以展開或摺疊樹狀結構中的個別節點，以顯示或隱藏在每一個節點之後發生的分割。 您也可以使用 **[決策樹]** 索引標籤上的選項，影響樹狀結構的顯示方式。 使用 **[顯示層級]** 滑桿，來調整樹狀結構所顯示的層級數目。 使用 **[預設展開]** ，來設定模型中所有樹狀結構所顯示的預設層級數目。  
  
 每一個節點的背景色彩陰影表示節點中存在的案例數目。 若要尋找節點中確切的案例數目，請將指標暫停在節點上，以檢視該節點的資訊提示。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Charts"></a> 圖表  
 [圖表]  索引標籤會顯示圖表，顯示預測的屬性經過一段時間的行為，也會顯示五個預測的未來值。 圖表的垂直軸代表序列的值，而水平軸代表時間。  
  
> [!NOTE]  
>  在時間軸上使用的時間配量取決於資料中所使用的單位：這些單位可能代表天、月，甚至秒。  
  
 請使用 [Abs]  按鈕，在絕對與相對曲線之間切換。 如果圖表包含多個模型，則每一個模型的資料比例可能會有極大差異。 如果使用絕對曲線，一個模型可能會顯示為平穩直線，而其他模型會顯示劇烈變動。 這是因為一個模型的比例比其他模型的比例大而導致。 藉由切換為相對曲線，您可以將比例變更為顯示變更百分比，而非絕對值。 這樣就可以輕鬆地比較以不同比例為依據的模型。  
  
 如果採礦模型包含多個時間序列，則您可以選取一或多個序列以顯示在圖表中。 只需按一下檢視器右側的清單，然後從清單選取所要的序列即可。 如果圖形變得太過複雜，可以選取或清除圖例中的序列核取方塊以篩選顯示的序列。  
  
 圖表會顯示記錄資料和未來的資料。 未來的資料會有陰影，以便與記錄資料有所區別。 資料值會以實線表示歷程記錄資料，而以虛線表示預測。 您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中設定屬性，以變更用於每一個數列的線條色彩。 如需詳細資訊，請參閱 [變更資料採礦檢視器中使用的色彩](../../analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md)。  
  
 您可以使用顯示比例選項，來調整顯示的時間範圍。 您也可以按一下圖表，在圖表上拖曳時間選取範圍，然後再按一下圖表在選取的範圍上放大，以檢視特定的時間範圍。  
  
 您可以使用 [預測步驟]  ，選取要在模型中查看多少個未來的時間**步驟**。 如果您選取 [顯示偏差]  核取方塊，檢視器會提供誤差線，讓您可以看出預測值的精確度。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 時間序列演算法](../../analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)   
 [資料採礦模型檢視器](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
  
