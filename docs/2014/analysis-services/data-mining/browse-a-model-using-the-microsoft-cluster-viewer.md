---
title: 瀏覽模型，使用 Microsoft 叢集檢視器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- clusters [Analysis Services]
- discrimination [Analysis Services]
- names [Analysis Services], clusters
- Microsoft Cluster Viewer
- mining model content, viewing
- comparing clusters
- viewing clusters
- displaying clusters
- data mining [Analysis Services], clusters
- Cluster Viewer [Analysis Services]
- mining models [Analysis Services], clusters
ms.assetid: 591fe30b-d88f-4a71-94d4-4a3907fc275d
caps.latest.revision: 41
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ebba3499c092ab89bacb4011671b0f90df67eb5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183562"
---
# <a name="browse-a-model-using-the-microsoft-cluster-viewer"></a>使用 Microsoft 叢集檢視器瀏覽模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 叢集檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法建立的採礦模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 群集演算法是用來瀏覽資料以識別資料中的異常及建立預測的一種分割演算法。 如需這個演算法的詳細資訊，請參閱 [Microsoft 群集演算法](microsoft-clustering-algorithm.md)。  
  
> [!NOTE]  
>  若要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
##  <a name="BKMK_ViewerTabs"></a> 檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集檢視器會提供下列索引標籤，用來瀏覽叢集採礦模型：  
  
-   [群集圖表](#BKMK_Diagram)  
  
-   [叢集設定檔](#BKMK_Profile)  
  
-   [群集特性](#BKMK_Characteristics)  
  
-   [群集辨識](#BKMK_Discrimination)  
  
###  <a name="BKMK_Diagram"></a> 群集圖表  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 叢集檢視器的 [叢集圖表] 索引標籤會顯示採礦模型中的所有叢集。 連接一個群集與另一個群集的線條陰影代表群集的相似程度。 如果陰影很淡或不存在，則表示群集不太相似。 當線條色彩加深時，連結的相似度就更高。 您可以調整群集右邊的滑桿，來調整檢視器要顯示的線條數目。 降低滑桿只顯示最強的連結。  
  
 依預設，陰影代表群集的母體。 使用 [陰影變數] 和 [狀態] 選項，您可以選取陰影所代表的屬性和狀態組合。 陰影愈深，表示特定狀態的屬性散發就愈大。 當陰影變淡時，散發跟著減少。  
  
 若要重新命名叢集，請以滑鼠右鍵按一下其節點，然後選取 [重新命名叢集]。 新名稱會保存在伺服器上。  
  
 若要將圖表的可見區段複製到剪貼簿，請按一下 **[複製圖表檢視]**。 若要複製完整圖表，請按一下 **[複製整個圖表]**。 您也可以使用 **[放大]** 和 **[縮小]** 來放大和縮小，或使用 **[將圖表縮放至視窗大小]**，使圖表符合視窗大小。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Profile"></a> 叢集設定檔  
 [叢集設定檔] 索引標籤會提供模型中的演算法所建立之叢集的整體檢視。 這個檢視會顯示每一個屬性以及該屬性在每一個群集中的分佈。 每一個資料格的資訊提示會顯示散發統計資料，而每一個資料行標題的資訊提示會顯示群集母體擴展。 分隔屬性是以彩色列顯示，而連續屬性是以鑽石圖顯示，鑽石圖代表每一個群集的平均差和標準差。 [長條圖列]  選項會控制長條圖中可見的橫條數。 如果總列數超出您選擇要顯示的列數，就會保留最重要的列，而其餘的列將會分組放入灰色值區中。  
  
 您可以變更群集的預設名稱，使名稱更具描述性。 請以滑鼠右鍵按一下叢集的資料行標題並選取 [重新命名叢集]，來重新命名叢集。 您也可以選取 [隱藏資料行] 來隱藏叢集。  
  
 若要開啟一個能提供更大、更詳細之叢集檢視的視窗，請按兩下 [狀態] 資料行的資料格或檢視器中的長條圖。  
  
 按一下資料行標題，即可依該群集的重要性順序來排序屬性。 您也可以拖曳資料行，在檢視器中重新排列它們。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Characteristics"></a> 群集特性  
 若要使用 **[群集特性]** 索引標籤，請從 **[群集]** 清單中選取群集。 選取群集之後，您可以檢查構成該特定群集的特性。 群集包含的屬性將列於 **[變數]** 資料行中，而所列屬性的狀態則列於 **[值]** 資料行中。 屬性狀態是依重要性列出，以它們出現在群集裡的機率來描述。 機率會在 **[機率]** 資料行中顯示。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
###  <a name="BKMK_Discrimination"></a> 群集辨識  
 您可以使用 [叢集辨識] 索引標籤來比較兩個叢集之間的屬性。 請使用 **[群集 1]** 和 **[群集 2]** 清單來選取要比較的群集。 檢視器會判斷群集間最重要的差異，並依重要性的順序顯示與差異相關聯的屬性狀態。 屬性右邊的列會顯示狀態喜好的群集，而列的大小會顯示狀態喜好群集的程度。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 群集演算法](microsoft-clustering-algorithm.md)   
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦工具](data-mining-tools.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)  
  
  
