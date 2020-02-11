---
title: 探索貝氏貝氏機率分類模型（基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb35c829b798335a27a37629711acf299ac2c7c9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62472882"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>瀏覽貝氏機率分類模型 (基本資料採礦教學課程)
  [!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏貝氏機率分類演算法提供數種方法來顯示自行車購買與輸入屬性之間的互動。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏貝氏機率分類 Viewer 提供下列索引標籤，供您用來探索貝氏貝氏機率分類的採礦模型：  
  
 
  
##  <a name="DependencyNetwork"></a>相依性網路  
 [相依性**網路**] 索引標籤的運作方式**** 與[!INCLUDE[msCoName](../includes/msconame-md.md)]樹狀檢視器的 [相依性網路] 索引標籤相同。 檢視器中的每一個節點各代表變數，節點之間的線條則代表關聯性。 在此檢視器中，您可以查看對於可預測屬性 Bike Buyer 的狀態具有影響力的所有屬性。  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>若要在相依性網路索引標籤中瀏覽模型  
  
1.  使用 [**採礦模型檢視器**] 索引標籤頂端的 [**採礦模型**] 清單， `TM_NaiveBayes`切換到模型。  
  
2.  使用 [**檢視器]** 清單切換至 [ **Microsoft 貝氏貝氏機率分類檢視器]**。  
  
3.  按一下`Bike Buyer`節點以識別其相依性。  
  
     粉紅色的陰影表示所有屬性都會影響自行車的購買。  
  
4.  調整滑動軸來識別最具影響力的屬性。  
  
     隨著您將滑動軸往下移，便只留下對 [Bike Buyer] 資料行影響最大的屬性。 當您調整滑動軸時，您可以發現幾個最具影響力的屬性如下：擁有的汽車數量、通勤距離及小孩總數。  
 
  
##  <a name="AttributeProfiles"></a>屬性設定檔  
 [**屬性設定檔**] 索引標籤會描述輸入屬性的不同狀態如何影響可預測屬性的結果。  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>若要在屬性設定檔索引標籤中瀏覽模型  
  
1.  在 [**可預測**] 方塊中`Bike Buyer` ，確認已選取 []。  
  
2.  如果「**挖掘圖例**」封鎖了**屬性設定檔**的顯示，請將它移出。  
  
3.  在 [**長條圖**列] 方塊中，選取 [ **5**]。  
  
     在我們的模型中，5 是任何一個變數的最大狀態數。  
  
     能夠影響這個可預測屬性所處狀態的屬性，會與輸入屬性之每一個狀態的值及其在可預測屬性之每一個狀態中的分佈情況一同列出。  
  
4.  在 [**屬性**] 資料行中，尋找 [**擁有的汽車數目**]。  請注意自行車買主 (標記為 1 的資料行) 與非買主 (標記為 0 的資料行) 的長條圖差異。 沒有任何汽車或是擁有一輛汽車的人比較可能購買自行車。  
  
5.  按兩下 [自行車購買者] （標示為1的資料行）資料行中的 [**汽車擁有的數位**] 資料格。  
  
     [**挖掘圖例**] 會顯示更詳細的觀點。  
  
  
##  <a name="AttributeCharacteristics"></a>屬性特性  
 使用 [**屬性特性**] 索引標籤，您可以選取屬性和值，以查看其他屬性的值在選取的值案例中出現的頻率。  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>若要在屬性特性索引標籤中瀏覽模型  
  
1.  在 [**屬性**] 清單中， `Bike Buyer`確認已選取 []。  
  
2.  將**值**設定為**1**。  
  
     在此檢視器中，您將會看到家裡沒有小孩、通勤距離很短而且住在北美地區的客戶比較可能購買自行車。  
  
  
##  <a name="AttributeDiscrimination"></a>屬性辨識  
 使用 [**屬性**辨識] 索引標籤，您可以調查自行車購買和其他屬性值的兩個離散值之間的關聯性。 因為`TM_NaiveBayes`模型只有兩個狀態，1和0，所以您不需要對檢視器進行任何變更。  
  
 在此檢視器中，您可以看出沒有汽車的人傾向於購買自行車，而擁有兩輛汽車的人則傾向於不購買自行車。  
  
## <a name="related-tasks"></a>相關工作  
 請參閱下列主題，瀏覽其他採礦模型。  
  
-   [流覽決策樹模型 &#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [&#40;基本資料採礦教學課程中探索群集模型&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第5課： &#40;基本資料採礦教學課程來測試模型&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [&#40;基本資料採礦教學課程中探索群集模型&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用 Microsoft 貝氏貝氏機率分類檢視器流覽模型](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [[屬性辨識] 索引標籤 &#40;[採礦模型檢視器]&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [[屬性設定檔] 索引標籤 &#40;[採礦模型檢視器&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [[屬性特性] 索引標籤 &#40;[採礦模型檢視器]&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [[相依性網路] 索引標籤 &#40;&#41;的採礦模型檢視器](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
