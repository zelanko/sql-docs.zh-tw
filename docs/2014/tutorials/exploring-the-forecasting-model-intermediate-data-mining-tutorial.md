---
title: 探索預測模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 0a00f409-050f-4b92-9763-ba31a6aa3052
caps.latest.revision: 52
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f3e41c8060a007e52af23c0637c744e72f0d1fb4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167761"
---
# <a name="exploring-the-forecasting-model-intermediate-data-mining-tutorial"></a>探索預測模型 (中繼資料採礦教學課程)
  既然您已建立預測的採礦模型，您可以使用來探索結果**採礦模型檢視器**資料採礦設計師 索引標籤。 [!INCLUDE[msCoName](../includes/msconame-md.md)]時間序列檢視器包含兩個索引標籤：**圖表**並**模型**。  
  
 此外，您可以對所有模型使用 Microsoft 一般內容樹狀檢視器。 每個檢視針對時間序列模型中的資訊呈現略為不同的面貌。  
  
-   [圖表 索引標籤](#bkmk_Charts)  
  
-   [模型索引標籤](#bkmk_Model)  
  
-   [Microsoft 一般內容檢視器](#bkmk_Content)  
  
##  <a name="bkmk_Charts"></a> 圖表 索引標籤  
 **圖表**索引標籤[!INCLUDE[msCoName](../includes/msconame-md.md)]時間序列檢視器以圖形方式顯示每個序列，包括歷程記錄資料和預測。 時間序列圖形中的每個線條代表由產品、區域和可預測屬性構成的唯一組合。  
  
 檢視器右側的圖例會根據下拉式清單中的選取項目列出時間序列。 您可以選取和清除圖例中的核取方塊，來控制圖形中所顯示的時間序列。  
  
 您也可以變更顯示選項，例如各時間序列所用的色彩，或值是否顯示在圖表中的資料點。  
  
#### <a name="to-select-a-time-series"></a>若要選取時間序列  
  
1.  按一下 **圖表**索引標籤**採礦模型檢視器**索引標籤上，如果看不到。  
  
2.  按一下圖表檢視右側的下拉式清單，選取所有核取方塊。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     圖表現在應包含 24 個不同的序列線條。  
  
3.  在圖表右側的核取方塊中，清除所有有關 [金額] 的方塊，以便暫時隱藏以金額為基礎的所有序列線條。  
  
     接著，清除與 R750 和 R250 自行車有關的核取方塊。  
  
     此圖表現在只包含下列六個序列線條，方便您比較 M200 和 T1000 自行車的趨勢。  
  
    -   **M200 Europe: Quantity**  
  
    -   **M200 North America： 數量**  
  
    -   **M200 Pacific： 數量**  
  
    -   **T1000 Europe: Quantity**  
  
    -   **T1000 North America： 數量**  
  
    -   **T1000 Pacific： 數量**  
  
 ![序列預測 M200 與 T1000 數量](../../2014/tutorials/media/6series-defaultforecasting.gif "序列預測 M200 與 T1000 數量")  
  
 此檢視器中顯示的圖表會包含歷程記錄資料和預測的資料。 預測的資料會加上陰影，以便和歷程記錄資料有所區別。 若要更輕鬆地比較不同序列，您也可以變更圖表中各線條的色彩。 如需詳細資訊，請參閱 [變更資料採礦檢視器中使用的色彩](../../2014/analysis-services/data-mining/change-the-colors-used-in-the-data-mining-viewer.md)。  
  
 從趨勢線，可以看到所有區域的總銷售量整體都在增加，且每 12 個月會有一個出現在 12 月的高峰。 此外，您還可以從圖表中看出 T1000 自行車資料的開始時間，比其他產品序列資料晚的多。 因為它是新產品，但此序列是以較少的資料為基礎，因此預測可能不準確。  
  
 根據預設，每個時間序列 (以點線表示) 顯示五個預測步驟。 您可以變更這個值，檢視更多或更少的預測。 您也可以在圖表中加入誤差線，以圖形方式檢視預測的標準差。  
  
#### <a name="to-change-prediction-and-display-options-in-the-chart-view"></a>變更圖表檢視中的預測和顯示選項  
  
1.  請嘗試變更的值**預測步驟**逐漸增加從**5**來**10**，然後再設回**6**。  
  
     當歷程記錄資料中有大幅波動時，其波動通常會隨著預測數目增加而重複或甚至幅度加大。 這時您可能需要探究歷程記錄資料中暴增的原因，然後決定是要接受這些結果、尋求來源資料中的某種更正，還是在模型中套用某種平滑效果。  
  
2.  選取 **顯示偏差**核取方塊。  
  
     此選項會顯示每個預測值的預估錯誤。  
  
3.  請注意 X 軸的小數位數。 歷程記錄和預測資料的變更永遠是以百分比表示，但實際值會自動調整，以便將所有值放在圖形上。 因此，在比較模型時需要特別小心，不要只依賴視覺項目。 若要取得實際值或百分比增量和值的預測，將滑鼠暫時放在點線或實線，或按一下線條以檢視中的值**採礦圖例**。  
  
     **祕訣**： 如果**採礦圖例**不可見，切換至**模型**檢視，以滑鼠右鍵按一下任何節點，然後選取**顯示圖例**。  
  
 檢視這些趨勢後，您關切某些序列缺少資料，想知道是否可根據模型或地區計算平均銷售量，取得更可靠的預測。 稍後在本教學課程中將探索此方法。  
  
 [回到頁首](#bkmk_Charts)  
  
##  <a name="bkmk_Model"></a> 模型索引標籤  
 **模型**索引標籤[!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦設計師中的時間序列檢視器可讓您檢視以樹狀圖形表單中的預測模型。  
  
 首先，請注意，因為資料針對三個不同區域 (Europe、North America 和 Pacific) 中多個產品線 (T1000 等等) 的銷售描述兩個不同的量值 (Amount 和 Quantity)，所以建立的模型實際上包含 24 個不同的樹狀目錄，每個樹狀目錄代表不同區域、產品和可預測屬性之組合的銷售模式模型。  
  
 您可以選擇哪一種產品線、 區域和銷售您想要檢視選取的一系列的度量組合**樹狀**下拉式清單中的上**模型** 索引標籤。  
  
 從樹狀檢視的模型中可學到什麼？ 舉例來說，假設要比較兩個模型，其中一個有數個樹狀層級，另一個有單一節點。  
  
-   當樹狀圖形包含單一節點時，這表示模型中的趨勢在一段時間後通常是同質性的。 您可以使用這個單一節點上，標示**所有**，若要檢視描述輸入的變數與結果之間的關聯性的公式。  
  
-   當時間序列的樹狀圖形有多個分支時，這表示偵測到的時間序列太複雜，無法以單一方程式表示。 相反地，樹狀圖形中可以包含多個分支，加上造成樹狀結構的每個分支*分割*。 當樹狀目錄分割時，每個分支表示不同的時間區段，其中的趨勢可用單一方程式描述。  
  
     例如，如果您查看圖表圖形，並看到銷售量從 9 月某個時間，一直到年底假期中，您可以切換到**模型**檢視來查看確切的日期變更趨勢的地方。 樹狀目錄中代表「9 月前」和「9 月後」的分支會包含不同的公式：一個公式以數學方式描述分割前的銷售趨勢，另一個公式則描述 9 月到年底假期的銷售趨勢。  
  
#### <a name="to-explore-the-decision-tree-for-a-time-series-model"></a>瀏覽時間序列模型的決策樹  
  
1.  在 [**樹狀結構**清單**模型**] 索引標籤的檢視器中，選取**T1000 Europe： 量**系列。  
  
     按一下 標示為節點**所有**。  
  
     針對**所有**節點，顯示的工具提示會在整個系列中，包含的案例數目等資訊，以及時間序列方程式衍生自分析的資料。  
  
2.  如果**採礦圖例**不是可見的以滑鼠右鍵按一下節點，然後選取**顯示圖例**。  
  
     **採礦圖例**提供的資訊相同的工具提示中。 如果有任何離散的獨立變數，您也會看到顯示變數分佈在節點中的長條圖。  
  
3.  現在選取另一個要檢視的時間序列。 使用**樹狀結構**清單**模型** 索引標籤的檢視器中，選取**M200 North America: Amount**系列。  
  
     樹狀圖形包含**所有**節點和兩個子節點。 您可以透過查看子節點上的標籤，了解趨勢線在哪個時間點變更。  
  
     對於每個子節點，在中描述**採礦圖例**也包含每個分支的樹狀結構中的 案例的計數。  
  
 下列清單說明樹狀檢視器的一些其他功能：  
  
-   您可以變更由圖表中使用變數**背景**控制項。 根據預設，較暗的節點包含更多的情況下，因為值**背景**設為**母體擴展**。 若要查看有多少案例只會在節點中，將滑鼠暫時放在某個節點上方，並檢視隨即出現，或按一下節點並檢視中的數字的工具提示**節點圖例**視窗。  
  
-   也可以在工具提示中或透過按一下節點來檢視節點的迴歸公式。 如果您建立了混合模型，則會看到兩個公式，一個用於 ARTXP (在分葉節點中)，另一個用於 ARIMA (在樹狀目錄的根節點中)。  
  
-   小菱形用於表示連續數字的節點。 菱形所在的橫線上會顯示屬性的範圍。 菱形會在節點的平均值置中，而菱形的寬度代表在該節點的屬性變異數。  
  
 [回到頁首](#bkmk_Charts)  
  
##  <a name="bkmk_Content"></a> （選擇性）一般內容樹狀檢視器  
 除了時間序列的自訂檢視器[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]提供**MicrosoftGeneric 內容樹狀檢視器**用於所有的資料採礦模型。 此檢視器具備一些優點：  
  
-   **Microsoft 時間序列檢視器**： 此檢視合併兩個演算法的結果。 雖然您可以分別檢視每個序列，但無法判斷各演算法結果如何結合。 此外，在此檢視中，工具提示和採礦圖例只顯示最重要的統計資料。  
  
-   **Generic Content Tree Viewer**： 可讓您瀏覽及檢視所使用的資料數列的所有模型中一次，如果您建立了混合模型，這兩個 ARIMA 和 ARTXP 樹狀結構會顯示在相同的圖形。  
  
     您可以使用此檢視器取得兩個演算法的所有統計資料，以及值分佈。  
  
     建議想要深入了解 ARIMA 和 ARTXP 分析的資料採礦專家使用者採用。  
  
#### <a name="to-view-details-for-a-particular-data-series-in-the-generic-content-viewer"></a>在一般內容樹狀檢視器中檢視特定資料序列的詳細資料  
  
1.  在 **採礦模型檢視器**索引標籤上，選取**Microsoft Generic Content Tree Viewer**從**檢視器**下拉式清單。  
  
2.  在 [ **Caption>** ] 窗格中，按一下最頂端的 (All) 節點。  
  
3.  在  ** 節點詳細資料** 窗格中，檢視 ATTRIBUTE_NAME 的值。  
  
     這個值顯示這個節點包含哪一個序列或產品與區域組合。 在 AdventureWorks 範例中，最頂端的節點屬於 M200 Europe 序列。  
  
4.  在 [ **Caption>** ] 窗格中，找出有子節點的第一個節點。  
  
     如果一個序列節點包含子系，樹狀檢視中，會出現在**模型**Microsoft 時間序列檢視器 索引標籤也會有一個分支結構。  
  
5.  展開該節點，並按一下其中一個子節點。  
  
     結構描述的 NODE_DESCRIPTION 資料行包含造成樹狀結構分岔的條件。  
  
6.  在 [ **Caption>** ] 窗格中，按一下最頂端的 ARIMA 節點，然後展開節點，直到所有的子節點會顯示。  
  
7.  在  ** 節點詳細資料** 窗格中，檢視 ATTRIBUTE_NAME 的值。  
  
     這個值會告訴您這個節點包含哪一個時間序列。 ARIMA 區段中最頂端的節點應該符合 (All) 區段中最頂端的節點。 在 AdventureWorks 範例中，這個節點包含 M200 Europe 序列的 ARIMA 分析。  
  
 如需詳細資訊，請參閱[時間序列模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-time-series-models-analysis-services-data-mining.md)。  
  
 [回到頁首](#bkmk_Charts)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立時間序列預測&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-time-series-predictions-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [時間序列模型查詢範例](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)   
 [Microsoft 時間序列演算法技術參考](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)  
  
  
