---
title: 瀏覽貝氏機率分類模型 （基本資料採礦教學課程） |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b06708d5-4477-4a51-bf8d-0b1e3c1f9ebb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4cc0e052b49cbfbf2324850aced8bd4753ca7ee3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48058168"
---
# <a name="exploring-the-naive-bayes-model-basic-data-mining-tutorial"></a>瀏覽貝氏機率分類模型 (基本資料採礦教學課程)
  [!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏機率分類演算法提供數種方法來顯示自行車購買與輸入的屬性之間的互動。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]貝氏機率分類檢視器會提供下列索引標籤，用來瀏覽貝氏機率分類採礦模型：  
  
 
  
##  <a name="DependencyNetwork"></a> 相依性網路  
 **相依性網路** 索引標籤的運作方式與**相依性網路**索引標籤[!INCLUDE[msCoName](../includes/msconame-md.md)]樹狀檢視器。 檢視器中的每一個節點各代表變數，節點之間的線條則代表關聯性。 在此檢視器中，您可以查看對於可預測屬性 Bike Buyer 的狀態具有影響力的所有屬性。  
  
#### <a name="to-explore-the-model-in-the-dependency-network-tab"></a>若要在相依性網路索引標籤中瀏覽模型  
  
1.  使用**採礦模型**清單頂端**採礦模型檢視器**索引標籤切換至`TM_NaiveBayes`模型。  
  
2.  使用**檢視器**切換至清單**Microsoft 貝氏機率分類檢視器**。  
  
3.  按一下 `Bike Buyer`節點以找出其相依性。  
  
     粉紅色的陰影表示所有屬性都會影響自行車的購買。  
  
4.  調整滑動軸來識別最具影響力的屬性。  
  
     隨著您將滑動軸往下移，便只留下對 [Bike Buyer] 資料行影響最大的屬性。 當您調整滑動軸時，您可以發現幾個最具影響力的屬性如下：擁有的汽車數量、通勤距離及小孩總數。  
 
  
##  <a name="AttributeProfiles"></a> 屬性設定檔  
 **屬性設定檔**索引標籤描述不同狀態的輸入的屬性會影響結果的可預測的屬性。  
  
#### <a name="to-explore-the-model-in-the-attribute-profiles-tab"></a>若要在屬性設定檔索引標籤中瀏覽模型  
  
1.  在  **Predictable**方塊中，確認`Bike Buyer`已選取。  
  
2.  如果**採礦圖例**封鎖顯示**屬性設定檔**，將它移開。  
  
3.  在 **長條圖**軸方塊中，選取**5**。  
  
     在我們的模型中，5 是任何一個變數的最大狀態數。  
  
     能夠影響這個可預測屬性所處狀態的屬性，會與輸入屬性之每一個狀態的值及其在可預測屬性之每一個狀態中的分佈情況一同列出。  
  
4.  在 **屬性**資料行中，尋找**Number Cars Owned**。  請注意自行車買主 (標記為 1 的資料行) 與非買主 (標記為 0 的資料行) 的長條圖差異。 沒有任何汽車或是擁有一輛汽車的人比較可能購買自行車。  
  
5.  按兩下**Number Cars Owned**格中自行車買主 （標記為 1 的資料行） 的資料行。  
  
     **採礦圖例**顯示更詳細的檢視。  
  
  
##  <a name="AttributeCharacteristics"></a> 屬性特性  
 具有**屬性特性**索引標籤上，您可以選取的屬性和值來查看其他屬性的值會出現在選定的值案例的頻率。  
  
#### <a name="to-explore-the-model-in-the-attribute-characteristics-tab"></a>若要在屬性特性索引標籤中瀏覽模型  
  
1.  在 **屬性**清單中，確認`Bike Buyer`已選取。  
  
2.  設定**值**要**1**。  
  
     在此檢視器中，您將會看到家裡沒有小孩、通勤距離很短而且住在北美地區的客戶比較可能購買自行車。  
  
  
##  <a name="AttributeDiscrimination"></a> 屬性辨識  
 具有**屬性辨識**索引標籤上，您可以調查的自行車購買行為的兩個離散值與其他屬性值之間的關聯性。 因為`TM_NaiveBayes`模型有兩個狀態，1 和 0，您就不必對此檢視器中的任何變更。  
  
 在此檢視器中，您可以看出沒有汽車的人傾向於購買自行車，而擁有兩輛汽車的人則傾向於不購買自行車。  
  
## <a name="related-tasks"></a>相關工作  
 請參閱下列主題，瀏覽其他採礦模型。  
  
-   [瀏覽決策樹模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-decision-tree-model-basic-data-mining-tutorial.md)  
  
-   [瀏覽群集模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="next-lesson"></a>下一課  
 [第 5 課： 測試模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/lesson-5-testing-models-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>本課程的前一項工作  
 [瀏覽群集模型&#40;基本資料採礦教學課程&#41;](../../2014/tutorials/exploring-the-clustering-model-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽模型，使用 Microsoft 貝氏機率分類檢視器](../../2014/analysis-services/data-mining/browse-a-model-using-the-microsoft-naive-bayes-viewer.md)   
 [屬性辨識索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/attribute-discrimination-tab-mining-model-viewer.md)   
 [屬性設定檔 索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/attribute-profiles-tab-mining-model-viewer.md)   
 [屬性特性索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/attribute-characteristics-tab-mining-model-viewer.md)   
 [相依性網路 索引標籤&#40;採礦模型檢視器&#41;](../../2014/analysis-services/dependency-network-tab-mining-model-viewer.md)  
  
  
