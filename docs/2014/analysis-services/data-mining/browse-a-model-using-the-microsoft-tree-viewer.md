---
title: 瀏覽模型，使用 Microsoft 樹狀檢視器 |Microsoft Docs
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
- Tree Viewer [Analysis Services]
- predictions [Analysis Services], discrete attributes
- mining model content, viewing
- predictions [Analysis Services], continuous attributes
- mining legend [Analysis Services]
- discrete attributes [Analysis Services]
- Microsoft Decision Trees algorithm [Analysis Services]
- decision tree algorithms [Analysis Services]
- Microsoft Tree Viewer
- decision trees [Analysis Services]
- dependencies [Analysis Services]
- continuous attributes
ms.assetid: 0c96d518-ed20-40b7-8d62-b26ad6244287
caps.latest.revision: 45
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f66d8ed3ba6a545a3088f121c9564b6008ebfa9c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278444"
---
# <a name="browse-a-model-using-the-microsoft-tree-viewer"></a>使用 Microsoft 樹狀檢視器瀏覽模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 樹狀檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法建立的決策樹。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法是同時支援分類與迴歸的混合式決策樹演算法。 因此，您也可以使用這個檢視器來檢視以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法為基礎的模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法可用於離散和連續屬性的預測模型。 如需有關這個演算法的詳細資訊，請參閱＜ [Microsoft Decision Trees Algorithm](microsoft-decision-trees-algorithm.md)＞。  
  
> [!NOTE]  
>  若要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，請使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
##  <a name="BKMK_TabsPanes"></a> 檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 樹狀檢視器包含下列索引標籤和窗格：  
  
-   [決策樹](#BKMK_DecisionTree)  
  
-   [相依性網路](#BKMK_DependencyNetwork)  
  
-   [採礦圖例](#BKMK_MiningLegend)  
  
###  <a name="BKMK_DecisionTree"></a> 決策樹  
 當您建立決策樹模型時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會為每一個可預測屬性建立個別樹狀。 您可以從檢視器之 **[決策樹]** 索引標籤的 **[樹狀結構]** 清單中，選取個別樹狀結構來檢視它。  
  
 決策樹是由一系列的分割所組成，最重要的分割 (由演算法決定) 位於檢視器左邊的 **[全部]** 節點上。 其他分割出現在右邊。 [所有] 節點中的分割最重要，因為它包含資料集內最強的導致分割條件，因此它會導致第一個分割。  
  
 您可以展開或摺疊樹狀結構中的個別節點，以顯示或隱藏在每一個節點之後發生的分割。 您也可以使用 **[決策樹]** 索引標籤上的選項，影響樹狀結構的顯示方式。 使用 **[顯示層級]** 滑桿，來調整樹狀結構所顯示的層級數目。 使用 **[預設展開]** ，來設定模型中所有樹狀結構所顯示的預設層級數目。  
  
#### <a name="predicting-discrete-attributes"></a>預測離散屬性  
 以離散可預測屬性建立樹狀結構時，檢視器會在樹狀結構的每一個節點上顯示下列各項：  
  
-   造成分割的狀況。  
  
-   代表可預測屬性之狀態分佈的長條圖，依據常用性排序。  
  
 您可以使用 **[長條圖]** 選項，來變更出現在樹狀之長條圖中的狀態數目。 如果可預測屬性有許多狀態，則此選項很有用。 狀態會依常用性順序由左至右出現在長條圖中；如果您選擇要顯示的狀態數目少於屬性中的總狀態數目，則最不常用的狀態全部會以灰色顯示。 若要查看節點之每一個狀態的確切計數，請將指標暫停在該節點上以檢視工具提示，或選取該節點來檢視它在 **[採礦圖例]** 中的詳細資料。  
  
 每一個節點的背景色彩都會代表您使用 **[背景]** 選項選取之特定屬性狀態案例的集中情形。 您可以使用此選項來反白顯示包含您想要之特定目標的節點。  
  
#### <a name="predicting-continuous-attributes"></a>預測連續屬性  
 當樹狀是以連續可預測屬性建立時，檢視器會為樹狀中的每一個節點顯示鑽石形圖表，而非長條圖。 此鑽石形圖表有一條線代表屬性的範圍。 鑽石形位於節點的平均值之處，而鑽石形的寬度代表在該節點的屬性變異數。 鑽石形越窄，表示節點所建立的預測愈精確。 檢視器也會顯示迴歸方程式，它是用來決定節點中的分割。  
  
#### <a name="additional-decision-tree-display-options"></a>其他決策樹顯示選項  
 針對決策樹模型啟用鑽研之後，您可以在樹狀結構中以滑鼠右鍵按一下節點並選取 [鑽研]，來存取支援該節點的培訓案例。 您可以在資料採礦精靈內啟用鑽研，或在 **[採礦模型]** 索引標籤中調整採礦模型上的鑽研屬性。  
  
 您可以使用 **[決策樹]** 索引標籤上的縮放選項來放大或縮小樹狀，或使用 **[調成最適大小]** ，使整個模型調整成檢視器畫面大小。 如果樹狀過大而無法調整成螢幕大小，您可以使用 [導覽] 選項來導覽樹狀。 按一下 **[導覽]** 就會開啟個別導覽視窗，您可以使用它來選取要顯示的模型區段。  
  
 您也可以將樹狀檢視影像複製到剪貼簿，以便將其貼到文件中或貼到影像操作軟體中。 使用 **[複製圖表檢視]** 即可只複製檢視器中可見的樹狀區段，或使用 **[複製整個圖表]** 來複製樹狀中所有展開的節點。  
  
 [回到頁首](#BKMK_TabsPanes)  
  
###  <a name="BKMK_DependencyNetwork"></a> 相依性網路  
 **[相依性網路]** 會顯示模型中的輸入屬性和可預測屬性之間的相依性。 檢視器左邊的滑桿會有篩選的作用，與相依性程度相關。 如果您降低滑桿，則檢視器中只會顯示最強的連結。  
  
 當您選取節點時，檢視器會反白顯示該節點特定的相依性。 例如，若您選擇一個可預測的節點，檢視器也會反白顯示每一個可協助預測該可預測節點的節點。  
  
 如果檢視器包含多個節點，您可以使用 **[尋找節點]** 按鈕來搜尋特定節點。 按一下 **[尋找節點]** 就會開啟 **[尋找節點]** 對話方塊，您可以在此使用篩選來搜尋和選取特定節點。  
  
 檢視器底端的圖例會將色碼連結至圖表中的相依性類型。 例如，當您選取可預測的節點時，可預測節點會呈現淺粉藍色陰影，而預測所選取之節點的節點則會呈現橙色陰影。  
  
 [回到頁首](#BKMK_TabsPanes)  
  
###  <a name="BKMK_MiningLegend"></a> 採礦圖例  
 當您在決策樹模型中選取節點時， **[採礦圖例]** 會顯示下列資訊：  
  
-   節點中的案例數目，依可預測屬性的狀態細分。  
  
-   節點的可預測屬性之每一個案例的機率。  
  
-   包括可預測屬性的每一個狀態計數的長條圖。  
  
-   要連上特定節點所需的條件，亦稱為 *節點路徑*。  
  
-   若為線性迴歸模型，就會顯示迴歸公式。  
  
 您可以用類似方案總管的方式來停駐和使用 **[採礦圖例]** 。  
  
 [回到頁首](#BKMK_TabsPanes)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)   
 [採礦模型檢視器&#40;資料採礦模型設計工具&#41;](../mining-model-viewers-data-mining-model-designer.md)   
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦工具](data-mining-tools.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)  
  
  
