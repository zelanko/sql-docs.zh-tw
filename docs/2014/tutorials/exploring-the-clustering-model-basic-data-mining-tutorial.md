---
title: 瀏覽群集模型 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26869ca780bc74e3c9c56b38b39195b893dbf523
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147768"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>瀏覽群集模型 (基本資料採礦教學課程)
  [!INCLUDE[msCoName](../includes/msconame-md.md)]群集演算法會將案例分成包含類似特性的群集。 這些群集對於瀏覽資料、識別資料的異常及建立預測很有幫助。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 叢集檢視器會提供下列索引標籤，用來瀏覽叢集採礦模型：  
  

  
##  <a name="ClusterDiagramTab"></a> 群集圖表索引標籤  
 [群集圖表] 索引標籤會顯示採礦模型中的所有群集。 群集之間的線代表「相似程度」，並根據群集的相似程度加上陰影。 每一個群集的實際色彩各代表變數的頻率和群集中的狀態。  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>若要在群集圖表索引標籤中瀏覽模型  
  
1.  使用**採礦模型**清單頂端**採礦模型檢視器**索引標籤切換至`TM_Clustering`模型。  
  
2.  在 **檢視器**清單中，選取**Microsoft 叢集檢視器**。  
  
3.  在 **陰影變數**方塊中，選取**Bike Buyer**。  
  
     預設變數是**母體擴展**，但您可以在模型中，若要探索哪些群集包含具有所需的屬性成員的任何屬性變更。  
  
4.  選取  **1**中**狀態**方塊來瀏覽這種情況下，已購買自行車。  
  
     **密度**圖例說明陰影變數] 和 [狀態中所選取之屬性狀態配對的密度。 在此範例告訴我們 clusterwith 最暗陰影的有最高百分比的自行車買主。  
  
5.  將滑鼠暫停在最深陰影的群集上方。  
  
     工具提示會顯示具有 `Bike Buyer = 1` 屬性的案例百分比。  
  
6.  選取具有最高的密度，以滑鼠右鍵按一下叢集，請選取群集**重新命名群集**並輸入**Bike Buyers High**以便日後識別。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  尋找具有最淺陰影 (和最低密度) 的群集。 以滑鼠右鍵按一下叢集，請選取**重新命名群集**並輸入**Bike Buyers Low**。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  按一下  **Bike Buyers High**叢集，並將它拖曳到窗格可讓您清楚檢視它與其他群集的連接的區域。  
  
     當您選取群集時，將此群集連接至其他群集的線條會反白顯示，如此您就可以輕鬆看見這個群集的所有關聯性。 當未選取此群集時，您可以透過線條的明暗度來區分圖表中所有群集之間關聯性的強烈程度。 如果陰影很淡或不存在，則表示群集不太相似。  
  
9. 利用網路左側的滑動軸，可以篩選掉較弱的連結，並找出關聯性最近的群集。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 行銷部門在判斷傳遞目標郵件的最佳方法時，可能會想要將類似的群集結合在一起。  
  

  
##  <a name="ClusterProfilesTab"></a> 叢集圖表索引標籤  
 **群集設定檔**索引標籤所提供的整體檢視`TM_Clustering`模型。 **群集設定檔** 索引標籤包含每個叢集模型中的資料行。 第一個資料行列出至少與一個群集相關聯的變數。 檢視器的其餘部份含有每一個群集的變數，其狀態的分佈情形。 離散變數的分佈會顯示為橫條圖中顯示的最大數目的彩色列**長條圖列**清單。 連續變數是以鑽石圖顯示，代表在每一個群集中的平均與標準差。  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>若要在群集設定檔索引標籤中瀏覽模型  
  
1.  設定**長條圖**軸**5**。  
  
     在我們的模型中，5 是任何一個變數的最大狀態數。  
  
2.  如果**採礦圖例**封鎖的顯示方式**屬性設定檔**，將它移開。  
  
3.  選取  **Bike Buyers High**資料行並將它拖曳至右邊**母體擴展**資料行。  
  
4.  選取  **Bike Buyers Low**資料行並將它拖曳至右邊**Bike Buyers High**資料行。  
  
5.  按一下  **Bike Buyers High**資料行。  
  
     **變數**資料行以該群集的重要性順序排序。 捲動資料行，並檢閱 Bike Buyer High 群集的特性。 例如，它們可能會有比較短的通勤距離。  
  
6.  按兩下**年齡**格中**Bike Buyers High**資料行。  
  
     **採礦圖例**顯示更詳細檢視，而且您可以看到的年齡範圍的這些客戶，以及平均年齡。  
  
7.  以滑鼠右鍵按一下**Bike Buyers Low**資料行，然後選取**隱藏資料行**。  
  

  
##  <a name="ClusterCharacteristicsTab"></a> 叢集特性索引標籤  
 具有**群集特性**索引標籤上，您可以更詳細地檢查組成群集的特性。 您可以一次瀏覽一個群集，而不是比較所有群集的特性 (如同 [群集設定檔] 索引標籤上的處理方式)。 例如，如果您選取**Bike Buyers High**從**叢集** 清單中，您可以看到這個群集中客戶的特性。 雖然這個顯示與 [群集設定檔] 檢視器不同，但是找到的結果是相同的。  
  
> [!NOTE]  
>  除非您設定的初始值**holdoutseed**，結果將會每次當您處理模型而有所不同。 如需詳細資訊，請參閱[HoldoutSeed 元素](../analysis-services/scripting/properties/holdoutseed-element.md)  
  

  
##  <a name="ClusterDiscriminationTab"></a> 群集辨識索引標籤  
 具有**群集辨識**索引標籤上，您可以瀏覽區分不同群集的特性。 您選取兩個叢集，其中來自後**群集 1**  清單中，而另一個來自**Cluster 2**  清單中，檢視器會計算群集之間的差異，並顯示的屬性清單，最能區分群集。  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>若要在群集辨識索引標籤中瀏覽模型  
  
1.  在 **群集 1**方塊中，選取**Bike Buyers High**。  
  
2.  在  **Cluster 2**方塊中，選取**Bike Buyers Low**。  
  
3.  按一下 **變數**的字母順序排序。  
  
     某些更重大的差異，在客戶間**Bike Buyers Low**並**Bike Buyers High**叢集包含年齡、 是否擁有汽車、 子系和區域數目。  
  
## <a name="related-tasks"></a>相關工作  
 請參閱下列主題，瀏覽其他採礦模型。  
  
-   [瀏覽決策樹模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [瀏覽貝氏機率分類模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [瀏覽貝氏機率分類模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [瀏覽決策樹模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽模型，使用 Microsoft 叢集檢視器](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [叢集辨識索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [叢集設定檔 索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [叢集特性索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [叢集圖表索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
