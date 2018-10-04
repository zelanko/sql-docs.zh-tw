---
title: 檢視時間序列公式模型 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c9225b2eb95d267c78caaf7521a8dee0b436db08
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163998"
---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>檢視時間序列模型的公式 (資料採礦)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]時間序列檢視器 inData 採礦設計師提供最簡單的方式，來檢視時間序列模型中使用之迴歸方程式的詳細資料。  
  
 您可以查詢模型內容來擷取時間序列模型的迴歸公式。 不過，若要檢視完整的 ARTXP 或 ARIMA 公式，我們建議您使用**採礦圖例**的[Microsoft 時間序列檢視器](browse-a-model-using-the-microsoft-time-series-viewer.md)，可讀取的格式呈現所有常數。  
  
 如果您建立混合模型，則會在不同的樹狀目錄中建立 ARIMA 和 ARTXP 分析，並且在表示模型的根節點處聯結。 ARIMA 和 ARTXP 樹狀目錄的結構差異很大。 例如，ARTXP 樹狀目錄實際上是一種樹狀結構，類似決策樹，而 ARIMA 樹狀目錄則表示一系列移動平均。 因此，雖然這兩種表示法是為求方便而以單一模型呈現，不過您應該將它們視為兩個獨立的模型。 兩個方程式也完全不同，而且無法結合或比較。  
  
 您也可以使用檢視時間序列模型[Microsoft 一般內容樹狀檢視器](../microsoft-generic-content-tree-viewer-data-mining.md)。 時間序列模型的內容相關資訊，請參閱[時間序列模型的採礦模型內容&#40;Analysis Services-Data Mining&#41;](mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>檢視時間序列模式的 ARTXP 迴歸公式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，選取您要檢視的時間序列模型，然後按一下 [瀏覽]。  
  
     -或-  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，選取時間序列模型，然後按一下 [採礦模型檢視器] 索引標籤。  
  
2.  按一下 [模型] 索引標籤。  
  
3.  如果模型包含多個樹狀結構，請從 [樹狀結構] 下拉式清單中選取一個單一樹狀結構。  
  
    > [!NOTE]  
    >  如果您擁有一個以上的資料數列，模型將永遠包含多個樹狀結構。 不過，您在時間序列檢視器中看到的樹狀結構數目，會比 [Microsoft 一般內容樹狀檢視器](../microsoft-generic-content-tree-viewer-data-mining.md)中的少。 這是因為時間序列檢視器會將每個資料數列的 ARIMA 和 ARTXP 資訊結合為單一表示法。  
  
4.  按一下樹狀結構中的任何分葉節點。  
  
     標示為 [資料數列] 的節點永遠是分葉節點，而且可以包含一個方程式。 如果 **(All)** 節點沒有子節點，它也可以包含一個方程式。  
  
5.  如果沒有可用的 [採礦圖例]，以滑鼠右鍵按一下節點，然後選取 [顯示圖例]。  
  
     ARTXP 公式會顯示在 [採礦圖例] 的前半部，當作 [樹狀節點方程式]。  
  
### <a name="to-view-the-arima-formula-for-a-time-series-model"></a>檢視時間序列模式的 ARIMA 公式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，選取您要檢視的時間序列模型，然後按一下 [瀏覽]。  
  
     -或-  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，選取時間序列模型，然後按一下 [採礦模型檢視器] 索引標籤。  
  
2.  按一下 [模型] 索引標籤。  
  
3.  如果模型包含多個樹狀結構，請從 [樹狀結構] 下拉式清單中選取一個單一樹狀結構。  
  
    > [!NOTE]  
    >  如果您加入一個以上的資料數列，此模型將永遠有多個樹狀結構。  
  
4.  按一下樹狀結構中的任何節點。  
  
     ARIMA 公式會顯示在 [採礦圖例] 的後半部，當作 [ARIMA 方程式]。  
  
5.  如果沒有可用的 [採礦圖例]，以滑鼠右鍵按一下節點，然後選取 [顯示圖例]。  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [瀏覽模型，使用 Microsoft 時間序列檢視器](browse-a-model-using-the-microsoft-time-series-viewer.md)   
 [時間序列模型查詢範例](time-series-model-query-examples.md)  
  
  
