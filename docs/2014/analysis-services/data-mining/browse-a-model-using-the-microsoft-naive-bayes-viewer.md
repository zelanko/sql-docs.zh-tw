---
title: 瀏覽模型，使用 Microsoft 貝氏機率分類檢視器 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- discrimination [Analysis Services]
- naive bayes model [Analysis Services]
- Bayesian classifiers
- mining model content, viewing
- predictive modeling [Analysis Services]
- Naive Bayes Viewer [Analysis Services]
- data mining [Analysis Services], predictive modeling
- Microsoft Naive Bayes Viewer
- histograms [Analysis Services]
- mining models [Analysis Services], predictive modeling
- dependencies [Analysis Services]
ms.assetid: 19743095-63c1-4486-8c1d-2efc143243be
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da5682ca2b998a9a73071aad9038c119e58152f0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145268"
---
# <a name="browse-a-model-using-the-microsoft-naive-bayes-viewer"></a>使用 Microsoft 貝氏機率分類檢視器瀏覽模型
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 貝氏機率分類檢視器會顯示以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法建立的採礦模型。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法是可高度適應預測模型工作的分類演算法。 如需有關這個演算法的詳細資訊，請參閱＜ [Microsoft Naive Bayes Algorithm](microsoft-naive-bayes-algorithm.md)＞。  
  
 由於貝氏機率分類模型的主要用途之一是要提供一個方式來快速瀏覽資料集內的資料，因此 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類檢視器會提供數個方法，來顯示可預測屬性和輸入屬性之間的互動。  
  
> [!NOTE]  
>  如果您要檢視有關此模型中所用的方程式及所探索之模式的詳細資訊，可以切換至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 一般內容樹狀檢視器。 如需詳細資訊，請參閱[使用 Microsoft 一般內容樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)或 [Microsoft 一般內容樹狀檢視器 &#40;資料採礦&#41;](../microsoft-generic-content-tree-viewer-data-mining.md)。  
  
##  <a name="BKMK_ViewerTabs"></a> 檢視器索引標籤  
 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中瀏覽採礦模型時，該模型會在適合它的檢視器中，顯示於資料採礦設計師的 **[採礦模型檢視器]** 索引標籤上。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類檢視器會提供用來瀏覽資料的下列索引標籤：  
  
-   [相依性網路](#BKMK_Dependency)  
  
-   [屬性設定檔](#BKMK_Profiles)  
  
-   [屬性特性](#BKMK_Characteristics)  
  
-   [屬性辨識](#BKMK_Discrimination)  
  
##  <a name="BKMK_Dependency"></a> 相依性網路  
 **[相依性網路]** 索引標籤會顯示模型中的輸入屬性和可預測屬性之間的相依性。 檢視器左邊的滑桿會有篩選的作用，與相依性程度相關。 降低滑桿只顯示最強的連結。  
  
 當您選取節點時，檢視器會反白顯示該節點特定的相依性。 例如，若您選擇一個可預測的節點，檢視器也會反白顯示每一個可協助預測該可預測節點的節點。  
  
 檢視器底端的圖例會將色碼連結至圖表中的相依性類型。 例如，當您選取可預測的節點時，可預測節點會呈現淺粉藍色陰影，而預測所選取之節點的節點則會呈現橙色陰影。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Profiles"></a> 屬性設定檔  
 **[屬性設定檔]** 索引標籤會在方格中顯示長條圖。 您可以使用這個方格，來比較您在 **[可預測]** 方塊中選取的可預測屬性與模型中的所有其他屬性。 索引標籤中的每一個資料行代表可預測屬性的狀態。 如果可預測屬性有許多狀態，您可以調整 **[長條圖列]** 來變更會出現在長條圖中的狀態數目。 如果您選擇的數目小於屬性中的狀態總數，狀態就會依支援的順序列出，剩餘狀態則收集到單一灰色值區內。  
  
 若要顯示使長條圖色彩與屬性狀態相關的採礦圖例，請按一下 **[顯示圖例]** 核取方塊。 採礦圖例也會針對您所選取的每個屬性值組顯示案例的分佈情況。  
  
 若要將方格的內容複製到 [剪貼簿] 作為一個 HTML 資料表，請以滑鼠右鍵按一下 [屬性設定檔] 索引標籤，然後選取 [複製]。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Characteristics"></a> 屬性特性  
 若要使用 **[屬性特性]** 索引標籤，請從 **[屬性]** 清單中選取一個可預測屬性，並從 **[值]** 清單中選取所選屬性的狀態。 當您設定這些變數時， **[屬性特性]** 索引標籤會顯示與所選屬性的所選案例相關聯之屬性的狀態。 屬性是依重要性排序。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
##  <a name="BKMK_Discrimination"></a> 屬性辨識  
 若要使用 **[屬性辨識]** 索引標籤，請從 **[屬性]**、 **[值 1]** 和 **[值 2]** 清單中選取可預測屬性和它的兩個狀態。 接著， **[屬性辨識]** 索引標籤上的方格會在資料行中顯示下列資訊：  
  
 **[屬性]**  
 列出資料集內的其他屬性，這些屬性包含一個非常喜好可預測屬性之其中一個狀態的狀態。  
  
 **值**  
 在 [屬性] 資料行中顯示屬性的值。  
  
 **喜好\<1 值 >**  
 顯示一個彩色列，它會指出屬性值喜好 [值 1] 中顯示之可預測屬性值的強烈程度。  
  
 **喜好\<值 2 >**  
 顯示一個彩色列，它會指出屬性值喜好 [值 2] 中顯示之可預測屬性值的強烈程度。  
  
 [回到頁首](#BKMK_ViewerTabs)  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 貝氏機率分類演算法](microsoft-naive-bayes-algorithm.md)   
 [採礦模型檢視器工作和使用說明](mining-model-viewer-tasks-and-how-tos.md)   
 [資料採礦工具](data-mining-tools.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)  
  
  