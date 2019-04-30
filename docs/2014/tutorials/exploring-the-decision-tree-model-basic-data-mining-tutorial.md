---
title: 瀏覽決策樹模型 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2e1472c2-3f3e-4dae-acb3-62fca374d397
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e7b77b445ff8cbef8be3acb72ef9cdb6fa3af159
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224601"
---
# <a name="exploring-the-decision-tree-model-basic-data-mining-tutorial"></a>瀏覽決策樹模型 (基本資料採礦教學課程)
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法會根據定型集中的其餘資料行，預測哪些資料行影響了自行車的購買決策。  
  

  
##  <a name="Decision_Tree_Tab"></a> 決策樹索引標籤  
 在 **決策樹**索引標籤上，您可以檢視每個可預測屬性的決策樹中的資料集。  
  
 在此情況下，此模型會預測只有一個資料行，Bike Buyer，因此只有一個樹狀結構檢視。 如果有多個樹狀結構，您可以使用**樹狀結構**方塊來選擇另一個樹狀結構。  
  
 當您檢視`TM_Decision_Tree`模型在決策樹檢視器中，您可以看到最重要的屬性，在圖表的左側。 「 最重要 」 表示這些屬性對於結果的最大影響。 沿著樹狀結構 (位於圖表右側) 愈往下的屬性其影響愈小。  
  
 在此範例中，年齡是預測自行車購買行為時最重要的一項因素。 模型會依年齡將客戶分組，然後顯示每個年齡群組的下一個最重要屬性。 例如，就客戶年齡層在 34 歲到 40 歲的群組來說，擁有車輛數是排在年齡後面的最強預測指標。  
  
#### <a name="to-explore-the-model-in-the-decision-tree-tab"></a>若要在決策樹索引標籤中瀏覽模型  
  
1.  選取 **採礦模型檢視器**索引標籤中**資料採礦設計師**。  
  
     根據預設，設計師會開啟第一個模型，在此情況下，已加入至結構- `TM_Decision_Tree`。  
  
2.  使用放大鏡按鈕調整樹狀結構顯示大小。  
  
     依預設，[!INCLUDE[msCoName](../includes/msconame-md.md)] 樹狀檢視器只顯示樹狀結構的前 3 個層級。 如果樹狀結構的層級不到 3 個，則檢視器只顯示現有的層級。 您可以使用，以檢視更多層級**顯示層級**滑桿或**預設展開**清單。  
  
3.  投影片**顯示層級**第四個列。  
  
4.  變更**背景**值`1`。  
  
     藉由變更**背景**設定，您可以迅速查看每個節點都有目標值的案例數目`1`之 [Bike Buyer]。 請記住，在這個特定案例中，每個案例都代表一個客戶。 該值`1`表示，客戶先前有購買自行車，值**0**表示客戶尚未購買自行車。 節點的陰影愈深，表示節點中擁有目標值的案例百分比愈高。  
  
5.  將游標放在標示為節點**所有**。 隨即出現工具提示，顯示下列資訊：  
  
    -   案例總數  
  
    -   非自行車購買者的案例數目  
  
    -   自行車購買者的案例數目  
  
    -   遺漏 [Bike Buyer] 值的案例數目  
  
     或者，將滑鼠游標放在樹狀結構其中任何一個節點上方，查看從前一個節點到達該節點所需的條件。 您也可以檢視在此相同資訊**採礦圖例**。  
  
6.  個節點上按一下**Age > = 34 和 < 41**。 其長條圖會顯示為一個橫跨節點的細長水平橫條，並表示在此年齡範圍中，已購買 (粉紅色) 或未購買 (藍色) 自行車的客戶分佈狀況。 檢視器顯示出年齡介於 34 到 40，只有一台車子或沒有車子的客戶有可能購買自行車。 再進一步研究，我們可以發現如果客戶年齡落在 38 到 40 歲，購買自行車的可能性又更高。  
  
 由於您在建立結構和模型時已啟用鑽研，因此您可以從模型案例和採礦結構中擷取詳細資訊，包括未包含在採礦模型中的資料行 (例如 emailAddress 和 FirstName)。  
  
 如需詳細資訊，請參閱 [鑽研查詢 &#40;資料採礦&#41;](../../2014/analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
#### <a name="to-drill-through-to-case-data"></a>若要鑽研案例資料  
  
1.  以滑鼠右鍵按一下節點，然後選取**鑽研**再**僅模型資料行**。  
  
     各定型案例的詳細資訊會以試算表格式顯示。 這些詳細資料來自您在建立採礦結構時，選取為案例資料表的 vTargetMail 檢視。  
  
2.  以滑鼠右鍵按一下節點，然後選取**鑽研**再**模型和結構資料行**。  
  
     隨即顯示相同的資料表，且結尾附加結構資料行。  
  
  
###  <a name="Dependency_Network_Tab"></a> 相依性網路 索引標籤  
 **相依性網路**索引標籤會顯示採礦模型的預測能力來幫助的變數之間的關聯性。 相依性網路檢視器更加印證我們的發現，也就是在預測自行車購買行為時，年齡和地區是重要的因素。  
  
##### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>若要在相依性網路索引標籤中瀏覽模型  
  
1.  按一下 `Bike Buyer`節點以找出其相依性。  
  
     相依性網路中，[中心] 節點`Bike Buyer`，表示採礦模型中的可預測屬性。 圖形會反白顯示對可預測屬性有影響的任何相連節點。  
  
2.  調整**所有連結**滑動軸來識別最具影響力的屬性。  
  
     當您拖曳滑桿下，具有弱式效果 [Bike Buyer] 資料行上的屬性會從圖形移除。 藉由調整滑動軸，您可以發現年齡和地區是預測自行車購買者的最大因素。  
  
## <a name="related-tasks"></a>相關工作  
 請參閱下列主題，使用其他種類的模型來瀏覽資料。  
  
-   [瀏覽群集模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
-   [瀏覽貝氏機率分類模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [瀏覽群集模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和使用說明](../../2014/analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [決策樹索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/decision-tree-tab-mining-model-viewer.md)   
 [相依性網路 索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)   
 [使用 Microsoft 樹狀檢視器瀏覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)  
  
  
