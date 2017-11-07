---
title: "檢視時間序列公式模型 （資料採礦） |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], how-to topics
- ARTXP
- time series algorithms [Analysis Services]
- ARIMA
- time series [Analysis Services]
- Time Series Viewer [Analysis Services]
ms.assetid: 825ef719-2f44-4979-be01-5a81f54e1a53
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3d33c91d9e9ed1cfd6bc58e8d44041d0e5f43c96
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="view-the-formula-for-a-time-series-model-data-mining"></a>檢視時間序列模型的公式 (資料採礦)
  如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦建立時間序列模型，要看到模型迴歸方程式，最簡單的方法是使用 [Microsoft 時間序列檢視器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)的 [採礦圖例]，它會以可閱讀的格式呈現所有常數。  
  
### <a name="to-view-the-artxp-regression-formula-for-a-time-series-model"></a>檢視時間序列模式的 ARTXP 迴歸公式  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，選取您要檢視的時間序列模型，然後按一下 [瀏覽]。  
  
     -或-  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，選取時間序列模型，然後按一下 [採礦模型檢視器] 索引標籤。  
  
2.  按一下 [模型] 索引標籤。  
  
3.  如果模型包含多個樹狀結構，請從 [樹狀結構] 下拉式清單中選取一個單一樹狀結構。  
  
    > [!NOTE]  
    >  如果您擁有一個以上的資料數列，模型將永遠包含多個樹狀結構。 不過，您在時間序列檢視器中看到的樹狀結構數目，會比 [Microsoft 一般內容樹狀檢視器](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)中的少。 這是因為時間序列檢視器會將每個資料數列的 ARIMA 和 ARTXP 資訊結合為單一表示法。  
  
4.  按一下樹狀結構中的任何分葉節點。  
  
     標示為 [資料數列] 的節點永遠是分葉節點，而且可以包含一個方程式。 如果 **(All)** 節點沒有子節點，它也可以包含一個方程式。  
  
5.  如果沒有可用的 [採礦圖例]，以滑鼠右鍵按一下節點，然後選取 [顯示圖例]。  
  
     ARTXP 公式會顯示在 [採礦圖例] 的前半部，當作 [樹狀節點方程式]。  
  
     ![在圖例中檢視時間序列公式](../../analysis-services/data-mining/media/ssdm-timeserieslegend.png "圖例中檢視時間序列公式")  
  
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
  
### <a name="to-get-the-coefficients-and-terms-for-the-equation"></a>取得方程式的係數和項  
  
1.  您也可以藉由建立模型內容的 **內容查詢** 來取得時間序列模型迴歸公式的係數和項。  
  
     如需詳細資訊，請參閱 [時間序列模型查詢範例](../../analysis-services/data-mining/time-series-model-query-examples.md)  
  
2.  您也可以使用 [Microsoft 一般內容樹狀檢視器](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)，瀏覽時間序列模型，以及尋找項和係數。  
  
     如需詳細資訊，請參閱[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
    > [!NOTE]  
    >  如果您瀏覽混合模型的內容，且該模型同時使用 ARIMA 和 ARTXP 模型，則兩個模型會位於個別的樹狀結構，並在代表模型的根節點聯結。 即使為了方便起見，ARIMA 和 ARTXP 模型顯示在一個檢視器中，結構和方程式是非常不同的，它們無法進行結合或比較。 ARTXP 樹狀目錄更像是決策樹，而 ARIMA 樹狀目錄則代表一系列的移動平均。  
  
## <a name="see-also"></a>請參閱＜  
 [採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [使用 Microsoft 時間序列檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-time-series-viewer.md)  
  
  

