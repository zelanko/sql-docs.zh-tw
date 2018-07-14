---
title: 探索時序群集模型 （中繼資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f8a485d5-47ed-4dd5-bb66-ef4d6d463845
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a17523ea68b8f04de5240011ad426dbe19779e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37226618"
---
# <a name="exploring-the-sequence-clustering-model-intermediate-data-mining-tutorial"></a>探索時序群集模型 (中繼資料採礦教學課程)
  既然您已建立**Sequence Clustering with Region**模型，您可以使用瀏覽它[!INCLUDE[msCoName](../includes/msconame-md.md)]中的時序叢集檢視器**採礦模型檢視器**資料採礦設計師 索引標籤。 [!INCLUDE[msCoName](../includes/msconame-md.md)]時序叢集檢視器包含五個索引標籤：**群集圖表**，**群集設定檔**，**群集特性**， **ClusterDiscrimination**，並**的狀態轉換**。 如需如何使用這個檢視器的詳細資訊，請參閱[瀏覽模型，使用 Microsoft 時序叢集檢視器](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)。  
  
-   [群集圖表索引標籤](#bkmk_CDiagram)  
  
-   [叢集圖表索引標籤](#bkmk_CProfiles)  
  
-   [叢集特性索引標籤](#bkmk_CChars)  
  
-   [群集辨識索引標籤](#bkmk_CDiscrim2)  
  
-   [狀態轉換索引標籤](#bkmk_StateTran)  
  
-   [一般內容檢視](#bkmk_Generic)  
  
##  <a name="bkmk_CDiagram"></a> 群集圖表索引標籤  
 **群集圖表** 索引標籤以圖形方式顯示演算法所發現之群集的資料庫中。 圖表的配置代表群集的關聯性，而且類似的群集會緊密地聚集在一起。 依預設，每一個節點的陰影都代表群集中所有案例的密度：節點的陰影越暗，表示它所包含的案例越多。 您可以變更節點陰影的意義，使它在每一個群集中代表屬性和狀態的支援。  
  
 您也可以重新命名群集，讓您可以更輕鬆地識別及處理目標群集。 在此教學課程中，我們將會重新命名太平洋地區具有最高客戶百分比的群集，以及整體上具有最多案例的群集。  
  
> [!NOTE]  
>  當您重新處理此模型時，指派給特定群集的案例可能會變更 (視資料和模型參數而定)。 此外，如果您重新命名群集，在您重新處理採礦模型時將會遺失名稱。  
  
#### <a name="to-change-the-attribute-used-for-highlighting-clusters"></a>若要變更用於反白顯示群集的屬性  
  
1.  在 **陰影變數**清單中，選取**模型**。  
  
2.  選取  **Cycling Cap**中**狀態**清單。  
  
     此圖表會更新，以顯示每一個群集中選定產品的聚集程度。 具有最暗陰影的群集所包含的 Cycling Cap 密度最高。 您可以變更陰影變數來使用任何輸入資料行的任何狀態。  
  
3.  在 **陰影變數**清單中，選取**母體擴展**。  
  
     當您將陰影變數變更成母體時，此圖表就會更新，根據大小來比較群集。 具有最暗陰影的群集所包含的案例要比其他群集多。  
  
#### <a name="to-rename-nodes-in-the-model"></a>若要重新命名模型內的節點  
  
1.  變更**陰影變數**要`Region`，並將**狀態**來**太平洋**。  
  
2.  反白顯示圖表中最暗的節點。  
  
3.  以滑鼠右鍵按一下此叢集，然後選取**重新命名群集。**  
  
4.  輸入名稱**Pacific Cluster。**  
  
5.  值變更**陰影變數**要**母體擴展**。  
  
6.  在更新的圖表中，尋找最暗的群集，這應該是最大的群集。 如果您不能從陰影來判斷哪一個群集最大，請將滑鼠暫時放在每一個群集的上方，並檢視工具提示，然後選擇包含最多案例的群集。  
  
7.  以滑鼠右鍵按一下此叢集，然後選取**重新命名群集**。 輸入新的名稱， `Largest Cluster`。  
  
 您可以從代表此群集的節點鑽研，以檢視位於每一個群集內之案例的詳細資料。 如果您想要針對分析的結果採取動作，例如傳送電子郵件給客戶，這樣的作法會很實用。 您也可以瀏覽您已併入結構內，但是未在模型內使用之案例的其他屬性，例如 Region 和 IncomeGroup。 如需有關如何透過從採礦模型鑽研到基礎案例的詳細資訊，請參閱[鑽研查詢&#40;資料採礦&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-drill-through-to-details-from-the-cluster-diagram"></a>若要從群集圖表鑽研到詳細資料  
  
1.  以滑鼠右鍵按一下`Pacific Cluster`，選取**鑽研**，然後選取**模型和結構資料行**。  
  
     **鑽研**對話方塊隨即開啟。 資料行，不會在模型中，但可用於查詢前面會加上**結構**。  
  
     您可以看到這個群集包含的客戶大多是來自太平洋地區，只有少數客戶來自其他地區。  
  
2.  按一下巢狀資料行 v Assoc Seq Line Items 中的加號，以檢視特定客戶訂單中項目的序列。  
  
3.  關閉**鑽研** 對話方塊。  
  
    > [!NOTE]  
    >  **播放**按鈕可讓您重新查詢資料; 不過，重新查詢不會變更資料顯示，除非模型已動態更新在背景中有其他處理序。  
  
 [回到頁首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CProfiles"></a> 叢集圖表索引標籤  
 **群集設定檔**索引標籤會顯示每個叢集中的時序。 叢集會列於右側的個別資料行**狀態**資料行。  
  
 在檢視器中，**模型**資料列描述項目在叢集中，整體分佈並**Model.samples**資料列都包含項目的序列。 每個彩色序列的每個資料格中的一行**Model.samples**資料列都代表在叢集中隨機選取使用者的行為。  
  
 個別序列長條圖中的每個顏色都代表一個產品型號。 採礦圖例會同時使用色彩編碼和產品型號名稱來顯示產品的序列。 如果您已經將其他資料行加入到模型內進行群集，例如 Region 或 Income Group，檢視器將會針對每一個資料行各包含另一個資料列，該資料列會顯示這些值在每一個群集內的分佈。  
  
#### <a name="to-view-the-sequences-that-are-most-common-in-a-cluster"></a>若要檢視群集中最常見的序列  
  
1.  以滑鼠右鍵按一下**模型**叢集資料行中的資料列`Largest Cluster`，然後選取**顯示圖例**。  
  
     **色彩**資料行包含陰影長的條，表示序列中找到的項目的頻率。 每一個項目都由不同的色彩表示。 **意義**欄會列出每一種色彩的產品型號名稱。 **發佈**資料行告訴您包含這個項目序列中的案例百分比。  
  
2.  關閉**採礦圖例**。  
  
3.  以滑鼠右鍵按一下**Model.samples**標題下，資料行中的資料列**母體擴展**，然後選取**顯示圖例**。  
  
4.  掃描整體模型中的時序清單`.`  
  
     [採礦圖例] 會先列出最常見的序列，好讓您可以看到 Mountain Tire Tube 在許多序列中都是第一個項目。 這表示客戶非常可能會先將 Mountain Tire Tube 放在購物籃中。  
  
#### <a name="to-drill-through-to-cases-from-the-cluster-viewer"></a>若要從群集檢視器鑽研到案例  
  
1.  向下捲動 [屬性] 窗格中，直到您找到的資料列`Region`屬性。  
  
     資料列包含在模型中，每個群集的長條圖，加上一個額外的長條圖**母體擴展**，這表示整個模型中使用的案例集合。 長條圖是一個具有不同色彩的長條，每一個色彩都代表一個屬性，而該屬性之色彩區段的大小則代表具有該屬性之案例的百分比。  
  
2.  比較您命名為群集的長條圖`Pacific Cluster`和`Largest Cluster`。 每一個群集都會出現在不同的資料行內。  
  
     兩者看起來都是純色，但是色彩不同。  
  
3.  在 `Region`資料列中上, 暫停滑鼠游標的色彩長條圖`Largest Cluster`。  
  
     工具提示會顯示值，這些值代表每一個地區之案例的實際百分比。  
  
4.  以滑鼠右鍵按一下中的色彩的長條圖`Region`的資料列`Pacific Cluster`，選取**鑽研**，然後選取**僅模型資料行**。  
  
5.  移動捲軸來檢閱這個群集中的所有客戶。  
  
     同樣地，鑽研到詳細資料可讓您看到此群集大多包含來自太平洋地區的訂單，但也有少數來自北美和歐洲地區。  
  
6.  關閉**鑽研** 對話方塊。  
  
 [回到頁首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CChars"></a> 叢集特性索引標籤  
 **群集特性**索引標籤會摘要顯示以視覺方式表示所選叢集的屬性值的重要性的長條叢集中的狀態之間轉換。 **變數**資料行告訴您被模型湊對於選取的群集或母體很重要： 特定值或值，稱為之間的關聯性*轉換*。 **值**資料行提供有關該值或轉換的進一步詳細資訊並**機率**資料行以視覺方式表示這個屬性或轉換的加權。  
  
#### <a name="to-view-the-important-attributes-for-a-cluster"></a>若要檢視群集的重要屬性  
  
1.  在 **叢集**下拉式清單中選取`Pacific Cluster`。  
  
     此清單會更新以顯示您已重新命名群集的特性`Pacific Cluster`。 在此叢集中，最重要特性是`Region`。  
  
2.  將滑鼠暫時放在資料列中的陰影長條上方`Region`。  
  
     這個值為 Pacific 的機率很高。 如需如何解譯這些值的詳細資訊，請參閱[Microsoft 時序群集演算法技術參考](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)。  
  
3.  查看群集的特性清單，直到您找到第一個轉換資料列為止。  
  
4.  轉換資料列包含的文字轉換中**變數**直條圖和循序屬性值中的一些組合**值**資料行。 此序列也可包含起點和遺漏的值。  
  
     例如，假設轉換的值為 [Start] -> Road Tire Tube。 這表示此群集中的客戶經常會將 Road Tire Tube 先放在他們的購物籃中。 這可能表示，此產品是客戶會先尋找的熱賣商品，或者可能只表示，此產品很容易在購買網站上找到。  
  
5.  捲動清單，直到您找到第一個轉換，並沒有 **[開始]** 或是**遺漏**裡面。  
  
     例如，假設您發現轉換**Touring Tire，Touring Tire Tube**。 這表示此群集中的客戶經常一起購買這些項目 (與這個順序完全相同)。  
  
6.  將滑鼠暫時放在這個轉換的陰影長條上方。  
  
     這個轉換的機率會顯示成百分比。  
  
7.  在 **叢集**下拉式清單中選取**母體擴展 （全部）**。  
  
     屬性的清單會更新，以顯示用來建立模型之所有訂單的特性。 在此採礦模型中，是最重要的區分群集的特性`Region`，其值為**North America**。  
  
 檢閱這些工作以後，您得知兩件事。 第一件就是您需要很多的資料，才能取得有意義的組合數目。 例如，具有最高機率的順序可能會包括 **[開始]** 或是**遺漏**狀態。  
  
 第二個是會有很大的叢集影響屬性上`Region`，因此更難看到序列的群組。 因此，您決定建立另一個只使用序列的模型，而且不包括地區或收入資料行。  
  
 [回到頁首](#bkmk_CDiagram)  
  
##  <a name="bkmk_CDiscrim2"></a> 群集辨識索引標籤  
 **群集辨識** 索引標籤可協助您比較兩個群集，來判斷哪一個屬性可區分特定群集從另一個叢集。 這個索引標籤包含四個資料行：**變數**，**值**，**叢集 1**，以及**Cluster 2**。  您可以選擇任何群集當做**群集 1**並**Cluster 2**。  
  
 **變數**資料行告訴您該屬性，這可以是資料行名稱或資料行名稱和這個字的組合名稱**轉換**。 **值**資料行會顯示之確切值的屬性或轉換。 中的資料行的陰影長的條**群集 1**並**Cluster 2**指出您要比較之群集的屬性強度。 長條越長，就表示此群集包含具有該屬性之案例的可能性越高。  
  
#### <a name="to-compare-two-clusters-by-using-the-cluster-discrimination-tab"></a>若要使用群集辨識索引標籤來比較兩個群集  
  
1.  在**群集辨識**索引標籤上，如**群集 1**，選取`Pacific Cluster`。  
  
     根據預設，選取**Cluster 2**變更為**補數的太平洋 * * * 叢集**。  
  
     最上層屬性，可區別`Pacific Cluster`從所有其他情況下是區域。 地區是一個很強的群集屬性，它會讓其他屬性相形失色。 為了避免這樣的影響，請嘗試互相比較幾個較小的群集。 當您這樣做時，屬性的清單會變更，而且可能包括模型之間的更多轉換。  
  
2.  找出轉換資料列，然後將滑鼠暫時放在陰影長條上方。  
  
     中的項目**值**資料行可以包含狀態和轉換。 每個項目的陰影代表辨識率。 若要深入了解不同的分數的意義，請參閱[時序叢集模型的採礦模型內容&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [回到頁首](#bkmk_CDiagram)  
  
##  <a name="bkmk_StateTran"></a> 狀態轉換索引標籤  
 在 **狀態轉換**索引標籤上，您可以選取一個群集來瀏覽它的狀態轉換。 如果您選取**母體擴展 （全部）** 從叢集下拉式清單中，圖表會顯示整個採礦模型的狀態的分佈。  
  
 圖表中的每個節點都代表一種狀態，或是您嘗試分析之序列的可能值。 節點的背景色彩代表該狀態的頻率。 線條會連接某些狀態，這表示狀態之間的轉換。 您可以將滑動軸上移或下移來變更轉換的機率臨界值。 數字與某些節點有關，這表示該狀態的機率。  
  
#### <a name="to-explore-the-relationships-in-the-state-transition-tab"></a>若要在狀態轉換索引標籤中探索關聯性  
  
1.  在 **狀態轉換** 索引標籤的 採礦模型檢視器中，選取`Pacific Cluster`從叢集清單。 請確認**顯示邊緣標籤**選項。  
  
     此圖表會更新，以顯示該群集中最常用的轉換。  
  
2.  按一下透過一條線與另一個節點連接的任何節點。  
  
     此圖表會更新，並反白顯示相關的節點。 此線條旁邊的數值表示轉換的機率。  
  
3.  最多將滑動軸**所有連結**，以增加圖表中包含的轉換次數。  
  
4.  選取 **母體擴展 （全部）** 從**叢集**。  
  
     請注意，當您載入不同群集時，此圖表會重設為預設顯示設定，好讓滑動軸控制項重設為中間位置。  
  
5.  按一下 在圖形中，這應該是最暗的節點**Sport-100**。  
  
     請注意，沒有任何線條可將這個產品連接其他產品。  
  
6.  將滑動軸上移一個步驟，以增加圖表中包含的轉換數。 不會一直**所有連結**尚未。  
  
     此圖表會更新，其方式是在圖表中加入其他幾個轉換，但是不能有包含 Sport-100 模型的轉換。  
  
7.  移動滑桿控制項一路**所有連結**。 按一下 [Sport-100] 節點 (若尚未選取)。  
  
     此圖表會更新，以顯示許多包含 Sport-100 產品的轉換。 連接線上箭頭的方向告訴您，Sport-100 項目選為此配對中的第一個項目還是第二個項目。  
  
8.  按一下 Touring Tire 的節點，並將滑動軸控制項往下移回中間位置。  
  
     在一開始，有許多轉換線連接 Touring Tire 和其他產品，但是當您提高機率臨界值時，從圖表中移除轉換的可能性就越低，只留下 Touring Tire > Touring Tire Tube 轉換。 這個轉換表示，如果某位客戶將 Touring Tire 放入購物籃，則該客戶接著將 Touring Tire Tube 也放入購物籃的機率很高。  
  
 [回到頁首](#bkmk_CDiagram)  
  
##  <a name="bkmk_Generic"></a> 一般內容樹狀檢視器  
 此檢視器可用於所有模型，不論演算法或模型類型為何。 **MicrosoftGeneric 內容樹狀檢視器**可從**檢視器**下拉式清單。  
  
 內容樹狀結構會將任何採礦模型表示為一系列的節點，其中的每一個節點都表示所學習到有關定型資料的知識。 節點可以包含模式、一組規則、群集，或是共用某些屬性之日期範圍的定義。 節點的確切內容會因為演算法和可預測屬性而有所不同，但是內容的一般表示都是相同的。  
  
 您可以展開每一個節點，以查看詳細資料的遞增層級，並將任何節點的內容複製到剪貼簿。 如需詳細資訊，請參閱 [使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)。  
  
#### <a name="to-view-details-for-a-sequence-clustering-model-by-using-the-generic-content-tree-viewer"></a>若要使用一般內容樹狀檢視器檢視時序群集模型的詳細資料  
  
1.  在 **採礦模型檢視器**索引標籤上，按一下**檢視器**清單，然後選取**Microsoft 一般內容樹狀檢視器**。  
  
2.  在  **Caption>** 窗格中，按一下  `Pacific Cluster (1)`。  
  
     這個節點的名稱同時包含您指派給群集的易記名稱和基礎節點識別碼。 您可以使用節點識別碼，向下鑽研到模型內的其他詳細資料。  
  
3.  展開第一個子節點，名為**群集 1 的時序層級**。  
  
     群集的時序層級節點包含有關該群集內包含之狀態和轉換的詳細資料。 您可以使用 NODE_DISTRIBUTION 資料行中提供的這些詳細資料，以整體方式探索每一個群集或模型的時序和狀態。  
  
4.  繼續展開節點，並在 HTML 檢視器窗格中檢視詳細資料。  
  
 如需有關採礦模型內容，以及如何使用詳細資料檢視器中的詳細資訊，請參閱[時序叢集模型的採礦模型內容&#40;Analysis Services-Data Mining&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)。  
  
 [回到頁首](#bkmk_CDiagram)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [建立相關的時序群集模型&#40;中繼資料採礦教學課程&#41;](../../2014/tutorials/creating-a-related-sequence-clustering-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時序群集演算法](../../2014/analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [時序群集模型查詢範例](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)  
  
  
