---
title: 瀏覽模型，使用 Microsoft 時序叢集檢視器 |Microsoft 文件
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cce1203b73f5a1685634c4b50f6e5941bed3eb98
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016785"
---
# <a name="browse-a-model-using-the-microsoft-sequence-cluster-viewer"></a>使用 Microsoft 時序叢集檢視器瀏覽模型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序叢集檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法建立的採礦模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法是時序分析演算法，用來瀏覽包含事件的資料，這些事件可透過遵循路徑或 *時序*加以連結。 如需這個演算法的詳細資訊，請參閱 [Microsoft 時序群集演算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)。  
  
> [!NOTE]  
>  若要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c)。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集檢視器會提供類似 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集檢視器的功能和選項。 如需詳細資訊，請參閱 [使用 Microsoft 叢集檢視器瀏覽模型](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)。  
  
##  <a name="BKMK_ViewerTabs"></a> 檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集檢視器會提供下列索引標籤，用來瀏覽時序群集採礦模型：  
  
-   [群集圖表](#BKMK_Diagram)  
  
-   [叢集設定檔](#BKMK_Profile)  
  
-   [群集特性](#BKMK_Characteristics)  
  
-   [群集辨識](#BKMK_Discrimination)  
  
-   [群集轉換](#BKMK_Transitions)  
  
###  <a name="BKMK_Diagram"></a> 群集圖表  
 **時序群集檢視器的** [群集圖表] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 索引標籤，會顯示採礦模型中的所有群集。 連接一個群集與另一個群集的線條陰影代表群集的相似程度。 如果陰影很淡或不存在，則表示群集不太相似。 當線條色彩加深時，連結的相似度就更高。 您可以調整群集右邊的滑桿，來調整檢視器要顯示的線條數目。 降低滑桿只顯示最強的連結。  
  
 依預設，陰影代表群集的母體。 使用 [陰影變數] 和 [狀態] 選項，您可以選取陰影所代表的屬性和狀態組合。 陰影愈深，表示特定狀態的屬性散發就愈大。 當陰影變淡時，散發跟著減少。  
  
 若要重新命名叢集，請以滑鼠右鍵按一下其節點，然後選取 [重新命名叢集]。 新名稱會保存在伺服器上。  
  
 若要將圖表的可見區段複製到剪貼簿，請按一下 **[複製圖表檢視]**。 若要複製完整圖表，請按一下 **[複製整個圖表]**。 您也可以使用 **[放大]** 和 **[縮小]** 來放大和縮小，或使用 **[將圖表縮放至視窗大小]**，使圖表符合視窗大小。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> 叢集設定檔  
 **[群集設定檔]** 索引標籤，會提供模型中的演算法所建立之群集的整體檢視。 在方格中的 **[母體]** 資料行後面的每一個資料行代表模型所發現的群集。 \<屬性 > t 資料列都代表不同的資料存在於叢集中，時序和\<屬性 > 資料列描述群集包含的所有項目和及其整體散發。  
  
 [長條圖列]  選項會控制長條圖中可見的橫條數。 如果總列數超出您選擇要顯示的列數，就會保留最重要的列，而其餘的列將會分組放入灰色值區中。  
  
 您可以變更群集的預設名稱，使名稱更具描述性。 請以滑鼠右鍵按一下叢集的資料行標題並選取 [重新命名叢集]，來重新命名叢集。 您可以選取 **[隱藏資料行]** 來隱藏群集，也可以拖曳資料行，在檢視器中將它們重新排序。  
  
 若要開啟一個能提供更大、更詳細之叢集檢視的視窗，請按兩下 [狀態] 資料行的資料格或檢視器中的長條圖。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 群集特性  
 若要使用 **[群集特性]** 索引標籤，請從 **[群集]** 清單中選取群集。 選取群集之後，您可以檢查構成該特定群集的特性。 群集包含的屬性將列於 **[變數]** 資料行中，而所列屬性的狀態則列於 **[值]** 資料行中。 屬性狀態是依重要性列出，以它們出現在群集裡的機率來描述。 機率會在 **[機率]** 資料行中顯示。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> 群集辨識  
 您可以使用 **[群集辨識]** 索引標籤來比較兩個群集之間的屬性，以決定時序中的項目對一個群集的喜好程度勝過另一個群集多少。 請使用 **[群集 1]** 和 **[群集 2]** 清單來選取要比較的群集。 檢視器會判斷群集間最重要的差異，並依重要性的順序顯示與差異相關聯的屬性狀態。 屬性右邊的列會顯示狀態喜好的群集，而列的大小會顯示狀態喜好群集的程度。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Transitions"></a> 群集轉換  
 藉由選取 **[群集轉換]** 索引標籤上的群集，您可以瀏覽所選取群集裡的時序狀態之間的轉換。 檢視器中的每一個節點都代表時序資料行的狀態。 箭頭代表兩個狀態之間的轉換以及與轉換相關聯的機率。 如果轉換回到原始節點，箭頭可指回到原始節點。  
  
 源自一個點的箭頭，代表節點是時序開頭的機率。 造成 Null 的結束邊緣，則代表節點是時序結尾的機率。  
  
 您可以使用索引標籤左邊的滑桿來篩選節點的邊緣。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Microsoft 時序群集演算法](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm.md)   
 [資料採礦工具](../../analysis-services/data-mining/data-mining-tools.md)   
 [資料採礦模型檢視器](../../analysis-services/data-mining/data-mining-model-viewers.md)   
 [瀏覽模型，使用 Microsoft 叢集檢視器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-cluster-viewer.md)  
  
  
