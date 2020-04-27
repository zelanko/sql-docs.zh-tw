---
title: 探索群集模型（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce8aa034-161b-473f-baec-9c29e0a8e5f5
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9bb2c6457122a5ea49824ca178b6950d88f75563
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63280425"
---
# <a name="exploring-the-clustering-model-basic-data-mining-tutorial"></a>瀏覽群集模型 (基本資料採礦教學課程)
  群集[!INCLUDE[msCoName](../includes/msconame-md.md)]演算法會將案例分組至包含類似特性的群集。 這些群集對於瀏覽資料、識別資料的異常及建立預測很有幫助。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 叢集檢視器會提供下列索引標籤，用來瀏覽叢集採礦模型：  
  

  
##  <a name="cluster-diagram-tab"></a><a name="ClusterDiagramTab"></a>[群集圖表] 索引標籤  
 [群集圖表] 索引標籤會顯示採礦模型中的所有群集。 群集之間的線代表「相似程度」，並根據群集的相似程度加上陰影。 每一個群集的實際色彩各代表變數的頻率和群集中的狀態。  
  
#### <a name="to-explore-the-model-in-the-cluster-diagram-tab"></a>若要在群集圖表索引標籤中瀏覽模型  
  
1.  使用 [**採礦模型檢視器**] 索引標籤頂端的 [**採礦模型**] 清單， `TM_Clustering`切換到模型。  
  
2.  在 [**檢視器]** 清單中，選取 [ **Microsoft 叢集檢視器]**。  
  
3.  在 [**陰影變數**] 方塊中，選取 [**自行車買方**]。  
  
     預設變數是 [擴展]，但您可以將其變更為模型中的任何**屬性，以**探索哪些叢集包含擁有您想要之屬性的成員。  
  
4.  在 [**狀態**] 方塊中選取**1** ，以探索已購買自行車的案例。  
  
     **密度**圖例會描述在陰影變數和狀態中所選取之屬性狀態配對的密度。 在此範例中，它會告訴我們，clusterwith 最深的陰影具有自行車購買者的最高百分比。  
  
5.  將滑鼠暫停在最深陰影的群集上方。  
  
     工具提示會顯示具有 `Bike Buyer = 1` 屬性的案例百分比。  
  
6.  選取最高密度的叢集，在叢集上按一下滑鼠右鍵，選取 [**重新命名**叢集]，然後輸入**自行車購買**者，以供日後辨識。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  尋找具有最淺陰影 (和最低密度) 的群集。 在叢集上按一下滑鼠右鍵，選取 [**重新命名**叢集]，然後輸入**自行車買家 Low**。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  按一下 [**自行車購買**者] 高叢集，並將它拖曳到窗格的某個區域，讓您清楚瞭解其與其他叢集的連接。  
  
     當您選取群集時，將此群集連接至其他群集的線條會反白顯示，如此您就可以輕鬆看見這個群集的所有關聯性。 當未選取此群集時，您可以透過線條的明暗度來區分圖表中所有群集之間關聯性的強烈程度。 如果陰影很淡或不存在，則表示群集不太相似。  
  
9. 利用網路左側的滑動軸，可以篩選掉較弱的連結，並找出關聯性最近的群集。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 行銷部門在判斷傳遞目標郵件的最佳方法時，可能會想要將類似的群集結合在一起。  
  

  
##  <a name="cluster-profiles-tab"></a><a name="ClusterProfilesTab"></a>群集設定檔索引標籤  
 [**群集設定檔**] 索引標籤會提供`TM_Clustering`模型的整體觀點。 [**群集設定檔**] 索引標籤包含模型中每個叢集的資料行。 第一個資料行列出至少與一個群集相關聯的變數。 檢視器的其餘部份含有每一個群集的變數，其狀態的分佈情形。 離散變數的分佈會顯示為彩色列，其中包含**長條圖**列清單中所顯示的最大橫條數。 連續變數是以鑽石圖顯示，代表在每一個群集中的平均與標準差。  
  
#### <a name="to-explore-the-model-in-the-cluster-profiles-tab"></a>若要在群集設定檔索引標籤中瀏覽模型  
  
1.  將**長條圖**列設定為**5**。  
  
     在我們的模型中，5 是任何一個變數的最大狀態數。  
  
2.  如果「**挖掘圖例**」封鎖**屬性設定檔**的顯示，請將它移出。  
  
3.  選取 [**自行車買家 High** ] 資料行，並將它拖曳至 **[擴展**] 資料行的右邊。  
  
4.  選取 [**自行車購買者下限**] 資料行，並將它拖曳至 [**自行車買家 High** ] 資料行的右邊。  
  
5.  按一下 [**自行車買家 High** ] 資料行。  
  
     [**變數**] 資料行會依該叢集的重要性順序排序。 捲動資料行，並檢閱 Bike Buyer High 群集的特性。 例如，它們可能會有比較短的通勤距離。  
  
6.  按兩下 [**自行車購買**者] [High] 資料行中的 [**年齡**] 資料格。  
  
     [**挖掘圖例**] 會顯示更詳細的觀點，您可以看到這些客戶的年齡範圍以及平均年齡。  
  
7.  以滑鼠右鍵按一下 [**自行車購買者下限**] 資料行，然後選取 [**隱藏資料行**]。  
  

  
##  <a name="cluster-characteristics-tab"></a><a name="ClusterCharacteristicsTab"></a>群集特性索引標籤  
 使用 [叢集**特性**] 索引標籤，您可以更詳細地檢查組成叢集的特性。 您可以一次瀏覽一個群集，而不是比較所有群集的特性 (如同 [群集設定檔] 索引標籤上的處理方式)。 例如，如果您**從 [叢集**] 清單中選取 [**自行車購買者高**]，就可以看到此叢集中客戶的特性。 雖然這個顯示與 [群集設定檔] 檢視器不同，但是找到的結果是相同的。  
  
> [!NOTE]  
>  除非您設定**holdoutseed**的初始值，否則每次處理模型時，結果會有所不同。 如需詳細資訊，請參閱[HoldoutSeed 元素](https://docs.microsoft.com/bi-reference/assl/properties/holdoutseed-element)  
  

  
##  <a name="cluster-discrimination-tab"></a><a name="ClusterDiscriminationTab"></a>群集辨識索引標籤  
 使用 [**叢集**辨識] 索引標籤，您可以探索區別另一個叢集的特性。 在您選取兩個叢集（一個來自 [叢集**1** ] 清單，另一個來自 [**群集 2** ] 清單）之後，檢視器會計算叢集之間的差異，並顯示最能區分叢集的屬性清單。  
  
#### <a name="to-explore-the-model-in-the-cluster-discrimination-tab"></a>若要在群集辨識索引標籤中瀏覽模型  
  
1.  在 [**群集 1** ] 方塊中，選取 [**自行車買家 High**]。  
  
2.  在 [**群集 2** ] 方塊中，選取 [**自行車買家 Low**]。  
  
3.  按一下 [**變數**] 以字母順序排序。  
  
     **自行車購買**者的低與**自行車購買者高階**叢集的客戶之間，有一些較大的差異，包括年齡、汽車擁有權、子女數目和地區。  
  
## <a name="related-tasks"></a>相關工作  
 請參閱下列主題，瀏覽其他採礦模型。  
  
-   [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [探索貝氏貝氏機率分類模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="next-task-in-lesson"></a>本課程的下一項工作  
 [探索貝氏貝氏機率分類模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-naive-bayes-model-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 Microsoft 叢集檢視器流覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)   
 [&#40;採礦模型檢視器&#41;的 [叢集辨識] 索引標籤](../../2014/analysis-services/cluster-discrimination-tab-mining-model-viewer.md)   
 [[叢集設定檔] 索引標籤 &#40;&#41;的採礦模型檢視器](../../2014/analysis-services/cluster-profiles-tab-mining-model-viewer.md)   
 [[叢集特性] 索引標籤 &#40;[採礦模型檢視器]&#41;](../../2014/analysis-services/cluster-characteristics-tab-mining-model-viewer.md)   
 [[叢集圖表] 索引標籤 &#40;[採礦模型檢視器]&#41;](../../2014/analysis-services/cluster-diagram-tab-mining-model-viewer.md)  
  
  
