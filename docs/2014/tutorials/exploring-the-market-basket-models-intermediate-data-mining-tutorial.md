---
title: 探索購物籃模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: da1c9cb7-6c32-4b9b-96ec-ecea772aeb77
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8a7b2f97cbda0594698c6cbaa68019a6493f1e74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224612"
---
# <a name="exploring-the-market-basket-models-intermediate-data-mining-tutorial"></a>探索購物籃模型 (中繼資料採礦教學課程)
  既然您已建立`Association`模型中，您可以使用瀏覽它[!INCLUDE[msCoName](../includes/msconame-md.md)]中的關聯檢視器**採礦模型檢視器**資料採礦設計師 索引標籤。 此教學課程會逐步引導您使用檢視器來探索項目之間的關聯性。 此檢視器可幫助您快速地查看哪些產品經常一起出現，並大概了解新興的模式。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]關聯檢視器包含三個索引標籤：**規則**，**項目集**，以及**相依性網路**。 因為每一個索引標籤都會呈現稍微不同的資料檢視，所以當您探索模型時，您通常會在不同的窗格之間來回切換幾次，以獲得有用的資訊。  
  
-   [相依性網路 索引標籤](#bkmk_DepNet)  
  
-   [項目集 索引標籤](#bkmk_Itemsets)  
  
-   [規則索引標籤](#bkmk_Rules)  
  
-   [一般內容檢視](#bkmk_ContentViewer)  
  
 本教學課程中，您將會開始在**相依性網路**索引標籤，然後再使用**規則**索引標籤並**項目集**索引標籤，加深您了解關聯性顯示檢視器中。 您也會使用**Microsoft 一般內容樹狀檢視器**來擷取個別規則或項目集的詳細統計資料。  
  
##  <a name="bkmk_DepNet"></a> 相依性網路 索引標籤  
 具有**相依性網路**索引標籤上，您可以調查的模型中的不同項目互動。 檢視器中的每一個節點都代表某個項目，而節點之間的線條則代表規則。 您可以透過選取某個節點，查看其他哪些節點會預測選取的項目，或目前的項目預測出哪些項目。 在某些情況下，項目之間會存在雙向關聯，表示它們通常會出現在同一項交易中。 您可以參考此索引標籤底部的色彩圖例來判斷關聯的方向。  
  
 連接兩個項目的線條表示，這兩個項目很可能同時出現在單一交易中。 換句話說，客戶很可能一起購買這兩個項目。 滑動軸與規則的機率相關。 將滑動軸往上移或往下移來篩選掉微弱的關聯，也就是機率很低的規則。  
  
 相依性網路圖表會顯示成對的規則，為 a->b，這表示如果購買產品 A，則產品 B 可能可以以邏輯方式表示。 此圖表無法顯示類型 AB->C 的規則]-> [c。 如果您移動滑動軸來顯示所有規則，但是在圖表中仍然未看到任何線條，這表示沒有任何成對規則符合演算法參數的準則。  
  
 您也可以依據名稱來尋找節點，其方式是輸入屬性名稱的第一個字母。 如需詳細資訊，請參閱[尋找節點對話方塊 &#40;採礦模型檢視器&#41;](../../2014/analysis-services/find-node-dialog-box-mining-model-viewer.md)。  
  
#### <a name="to-open-the-association-mode-in-the-microsoft-assocaition-rules-viewer"></a>若要在 Microsoft 關聯規則檢視器中開啟關聯模式  
  
1.  在 [**方案總管] 中**，按兩下關聯結構。  
  
2.  在資料採礦設計師中，按一下 **[採礦模型檢視器]** 索引標籤。  
  
3.  從採礦模型中的清單中選取 關聯**採礦模型**下拉式清單中。  
  
#### <a name="to-navigate-the-dependency-graph-and-locate-specific-nodes"></a>若要導覽相依性圖表及尋找特定的節點  
  
1.  在 [**採礦模型檢視器**索引標籤上，按一下**相依性網路**] 索引標籤。  
  
2.  按一下 **拉近**好幾次，直到您可以輕鬆檢視每個節點的標籤。  
  
     根據預設，顯示此圖表時，將可看見所有的節點。 複雜模型中可能有許多節點，使得每一個節點看起來很小。  
  
3.  按一下  **+** 登入的檢視器右下角，然後按住滑鼠按鈕，即可放大圖表。  
  
4.  在檢視器的左側，將拖曳滑動軸往下將它從**所有連結**（預設值） 滑桿控制項的底部。  
  
5.  檢視器會更新此圖表，現在它只會顯示 Touring Tire 與 Touring Tire Tube 項目之間最強的關聯。  
  
6.  按一下 標示為節點**Touring Tire Tube = Existing**。  
  
     此圖表會更新，僅反白顯示與此項目之間有強烈相關性的項目。 請注意兩個項目之間的箭頭方向。  
  
7.  在檢視器的左邊，將滑動軸再次往上拖曳，將它從底部移到中間附近。  
  
     請注意連接兩個項目之箭頭的變更。  
  
8.  選取 **只顯示屬性名稱**從下拉式清單中頂端的 相依性網路 窗格。  
  
     圖表中的文字標籤會更新，只顯示模型名稱。  
  
 [回到頁首](#bkmk_DepNet)  
  
##  <a name="bkmk_Itemsets"></a> 項目集 索引標籤  
 接下來，您將會深入了解此模型針對 Touring Tire 和 Touring Tire Tube 產品所產生的規則與項目集。 **項目集**索引標籤會顯示三個重要部分的資訊與相關項目集，[!INCLUDE[msCoName](../includes/msconame-md.md)]關聯分析演算法會探索：  
  
-   **支援：** 發生在哪個項目集的交易數目。  
  
-   **大小：** 項目集內的項目數目。  
  
-   **項目：** 每個項目集內包含之項目的清單。  
  
 演算法可能會產生許多項目集，這會因演算法參數的設定方式而不同。 檢視器中傳回的每個項目集都代表已賣出此項目的交易。 使用控制項的頂端**項目集**索引標籤上，您可以篩選檢視器顯示只有項目集包含指定的最小支援和項目集大小。  
  
 如果您正在使用不同的採礦模型，而且未列出任何項目集，這是因為沒有任何項目集符合演算法參數的準則。 在這類情況下，您可以變更演算法參數，允許具有較低支援的項目集。  
  
#### <a name="to-filter-the-itemsets-that-are-shown-in-the-viewer-by-name"></a>若要依名稱篩選檢視器中顯示的項目集  
  
1.  按一下 [**項目集**檢視器] 索引標籤。  
  
2.  在 **篩選項目集**方塊中，輸入`Touring Tire`，然後按一下 外部 方塊中。  
  
     此篩選會傳回包含這個字串的所有項目。  
  
3.  在 **顯示**清單中，選取**只顯示屬性名稱**。  
  
4.  選取 **顯示完整名稱**核取方塊。  
  
     項目集的清單會更新，僅顯示包含 Touring Tire 字串的項目集。 項目集的完整名稱包括了內含每一個項目之屬性和值的資料表名稱。  
  
5.  清除**顯示完整名稱**核取方塊。  
  
     項目集的清單會更新，僅顯示簡短名稱。  
  
 中的值**支援**資料行指出每個項目集的交易數目。 項目集的交易表示包含此項目集內所有項目的購買。  
  
 根據預設，檢視器會依照支援的遞減順序列出項目集。 您可以按一下資料行標頭，依照不同的資料行排序，例如項目集大小或名稱。 如果您有興趣進一步了解項目集內包含的個別交易，您可以從項目集鑽研到個別案例。 鑽研結果中的結構資料行是模型中未使用的客戶收入等級和客戶識別碼。  
  
#### <a name="to-view-details-for-an-itemset"></a>若要檢視項目集的詳細資料  
  
1.  在項目集清單中，按一下**項目集**，依名稱排序的資料行標題。  
  
2.  找到的項目， `Touring Tire` （與沒有第二個項目）。  
  
3.  項目，以滑鼠右鍵按一下`Touring Tire`，選取**鑽研**，然後選取**模型和結構資料行**。  
  
     **鑽研**對話方塊會顯示使用做為支援此項目集的個別交易。  
  
4.  展開巢狀資料表 vAssocSeqLineItems，檢視交易中的實際購買清單。  
  
#### <a name="to-filter-itemsets-by-support-or-size"></a>若要依照支援或大小篩選項目集  
  
1.  清除可能在任何文字**篩選項目集** 方塊中。 您無法將文字篩選與數值篩選一起使用。  
  
2.  在 **的最小支援**方塊中輸入 100，然後再按一下 檢視器的背景。  
  
     項目集的清單會更新，僅顯示支援至少為 100 的項目集。  
  
 [回到頁首](#bkmk_DepNet)  
  
##  <a name="bkmk_Rules"></a> 規則索引標籤  
 **規則**索引標籤會顯示此演算法會尋找的規則相關的下列資訊。  
  
-   **機率：***可能性*的規則，定義為給定左邊項目右邊項目的機率。  
  
-   **重要性：** 規則的實用性的量值。 較大的值表示較好的規則。  
  
     提供重要性可幫助您測量規則的實用性，因為單獨使用機率可能會產生誤導。 例如，如果每筆交易都包含一個水壺 (或許將水壺當做促銷活動的贈品自動加入到每一個客戶的購物車內)，此模型會建立一個規則來預測水壺的機率為 1。 如果這個規則只根據機率將會非常精確，但是無法提供實用的資訊。  
  
-   **規則：** 規則定義。 若為購物籃模型，規則會描述特定的項目組合。  
  
 每項規則都可用來根據其他項目的出現情況，預測這個項目在交易中的出現狀況。 就像**項目集**索引標籤上，您可以篩選規則，以顯示最有趣的規則。 如果您正在使用沒有任何規則的採礦模型，您可能會想要變更演算法參數，以降低規則的機率臨界值。  
  
#### <a name="to-see-only-rules-that-include-the-mountain-200-bicycle"></a>若要查看只包含 Mountain-200 自行車的規則  
  
1.  在 [**採礦模型檢視器**索引標籤上，按一下**規則**] 索引標籤。  
  
2.  在 **篩選器規則**方塊中，輸入`Mountain-200`。  
  
     清除**顯示完整名稱**核取方塊。  
  
3.  從**顯示**清單中，選取**只顯示屬性名稱**。  
  
     檢視器會顯示包含文字的規則"`Mountain-200`」。 規則的機率會告訴您如何可能它是，當有使用者購買`Mountain-200`腳踏車，該人員同時購買其他列出之產品。  
  
 這些規則會依照機率的遞減順序排序，但是您可以按一下資料行標題來變更排序次序。 如果您很有興趣了解特定規則的詳細資料，您可以使用鑽研來檢視支援的案例。  
  
#### <a name="to-view-cases-that-support-a-particular-rule"></a>若要檢視可支援特定規則的案例  
  
1.  在 **規則**索引標籤上，以滑鼠右鍵按一下您想要檢視的規則。  
  
2.  選取 **鑽研**，然後選取**僅模型資料行**，或**模型和結構資料行**。  
  
     **鑽研** 對話方塊中提供的規則，在頂端的窗格中和一份所有情況下，做為規則支援資料摘要。  
  
 [回到頁首](#bkmk_DepNet)  
  
##  <a name="bkmk_ContentViewer"></a> 一般內容樹狀檢視器  
 此檢視器可用於所有模型，不論演算法或模型類型為何。 **Microsoft Generic Content Tree Viewer**可從**檢視器**下拉式清單。  
  
 內容樹狀結構會將採礦模型表示為節點的序列，其中的每一個節點都表示所學習到有關某些資料集的知識。 節點可以包含模式、一組規則、叢集，或是共用某些特性之日期範圍的定義。 節點的確切內容會因為演算法和可預測之屬性的類型而有所不同，但是內容的一般表示都是相同的。 您可以展開每一個節點，以查看詳細資料的遞增層級，並將任何節點的內容複製到剪貼簿。  
  
#### <a name="to-view-details-about-the-rule-by-using-the-content-viewer"></a>若要使用內容檢視器來檢視有關此規則的詳細資料  
  
1.  在 **採礦模型檢視器**索引標籤上，選取**Microsoft Generic Content Tree Viewer**從**檢視器**清單。  
  
2.  在 [節點標題] 窗格中，捲動到清單的底部，然後按一下最後一個節點。  
  
     檢視器會先顯示項目集，接著再顯示規則，但是不會加以分組。 有一個最簡單的方法可尋找特定節點，那就是建立內容查詢。 如需詳細資訊，請參閱 [關聯模型查詢範例](../../2014/analysis-services/data-mining/association-model-query-examples.md)。  
  
3.  在 [節點詳細資料] 窗格中，檢閱 NODE_TYPE 和 NODE_DESCRIPTION 的值。  
  
     節點類型 8 是一個規則，而節點類型 7 則是一個項目集。 對於規則而言，NODE_DESCRIPTION 的值會告訴您組成此規則的條件。 對於項目集而言，NODE_DESCRIPTION 的值會告訴您包含在此項目集中的項目。  
  
 您也可以建立內容查詢，以取得有關規則的詳細統計資料。 如需有關採礦模型內容以及如何解譯它的詳細資訊，請參閱 <<c0> [ 關聯模型的採礦模型內容&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。</c0>  
  
 [回到頁首](#bkmk_DepNet)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [篩選採礦模型中的巢狀的資料表&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [第 3 課：建立購物籃狀況&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)   
 [第 4 課：建立時序群集案例&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)   
 [Microsoft 關聯分析演算法](../../2014/analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Microsoft 關聯分析演算法技術參考](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)  
  
  
