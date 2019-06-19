---
title: Microsoft 決策樹演算法 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- predictions [Analysis Services], discrete attributes
- predictions [Analysis Services], continuous attributes
- algorithms [data mining]
- discrete attributes [Analysis Services]
- classification algorithms [Analysis Services]
- discrete columns [Analysis Services]
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- continuous columns
- regression algorithms [Analysis Services]
ms.assetid: 95ffe66f-c261-4dc5-ad57-14d2d73205ff
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7a9adfe74aef16e475d06eddfbe08852f7618518
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084107"
---
# <a name="microsoft-decision-trees-algorithm"></a>Microsoft 決策樹演算法
  [!INCLUDE[msCoName](../../includes/msconame-md.md)]決策樹演算法是所提供的分類和迴歸演算法[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]用於離散和連續屬性的預測模型。  
  
 針對分隔屬性，此演算法依據資料集內的輸入資料行之間的關聯性來產生預測。 它會使用這些資料行的值 (稱為狀態) 來預測您指定為可預測之資料行的狀態。 尤其，此演算法會識別與可預測資料行相互關聯的輸入資料行。 例如，在預測哪些客戶可能購買腳踏車的狀況中，如果 10 個年輕客戶當中有 9 個購買腳踏車，但 10 個年紀較大的客戶當中只有 2 個人這麼做，則演算法會推斷年齡是腳踏車購買的理想預測器。 決策樹就是依據傾向於特定結果的趨勢來產生預測。  
  
 針對連續屬性，此演算法使用線性迴歸來決定決策樹分岔之處。  
  
 如果不止一個資料行設定為可預測，或輸入資料包含的巢狀資料表設定為可預測，則演算法會建立每一個可預測資料行的個別決策樹。  
  
## <a name="example"></a>範例  
 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 公司的行銷部門想要識別舊客戶的特性，這些特性會指出那些客戶是否可能購買未來的產品。 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫會儲存描述舊客戶的人口統計資訊。 藉由使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法來分析此資訊，行銷部門可以建立模型，依據關於特定客戶之已知資料行的狀態 (例如人口統計或過去購買模式) 來預測該客戶是否會購買產品。  
  
## <a name="how-the-algorithm-works"></a>演算法的運作方式  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法會在樹狀結構中建立一系列分割，藉以建立資料採礦模型。 然後，這些分割會表示成「節點」  。 每次發現輸入資料行與可預測資料行有明顯地相互關聯時，此演算法就會在模型中加入一個節點。 演算法決定分岔的方式不同，視它預測連續資料行或分隔資料行而定。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法會使用「特徵選取」  來引導選取最有用的屬性。 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦演算法都會使用特徵選取來改善效能和分析的品質。 若要防止不重要的屬性佔用處理器時間，特徵選取就很重要。 如果您在設計資料採礦模型時使用過多輸入或可預測的屬性，此模型可能會需要很長的時間才能處理完成，甚至用完記憶體。 用來判斷是否要分割樹狀結構的方法包括 *entropy* 和 Bayesian 網路的業界標準。  如需用來選取有意義屬性，然後針對這些屬性計分並排名之方法的詳細資訊，請參閱[特徵選取 &#40;資料採礦&#41;](feature-selection-data-mining.md)。  
  
 資料採礦模型中常見的問題是模型變得過度敏感定型資料中的小差異，而這種情況就稱為*過度納入*或是*過度定型*。 過度調整的模型無法一般化成為其他資料集。 為了避免過度調整任何特定資料集， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法會使用控制樹狀目錄成長的技術。 如需 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法如何運作的更深入說明，請參閱 [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)。  
  
### <a name="predicting-discrete-columns"></a>預測分隔資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法為分隔可預測資料行建立樹狀結構的方式，可使用長條圖來示範。 下列圖表顯示一個長條圖，它繪製出可預測資料行 Bike Buyers 對照輸入資料行 Age。 長條圖顯示某人的年齡可協助區分此人是否會購買腳踏車。  
  
 ![從 Microsoft 決策樹演算法的長條圖](../media/dt-histogram.gif "自 Microsoft 決策樹演算法的長條圖")  
  
 圖表中所顯示的相互關聯會導致 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法在模型中建立新節點。  
  
 ![決策樹節點](../media/dt-tree.gif "決策樹節點")  
  
 當演算法在模型中加入新節點時，就會形成樹狀結構。 樹狀的最上層節點描述客戶整體母體擴展之可預測資料行的細分。 當模型繼續成長時，演算法會考量所有資料行。  
  
### <a name="predicting-continuous-columns"></a>預測連續資料行  
 當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法依據連續可預測資料行建立樹狀結構時，每一個節點會包含一個迴歸公式。 分岔會出現在迴歸公式中的非線性點上。 例如，請看下列圖表。  
  
 ![多個迴歸程式行顯示非線性](../media/regression-tree1.gif "多個迴歸程式行顯示非線性")  
  
 圖表包含可使用單線或使用兩條連接線建立模型的資料。 不過，用單線來表示資料，效果較差。 相對地，如果您使用雙線，則模型更能做好模擬資料的作業。 兩條線交叉的點就是非線性點，也是在決策樹模型中之節點會分岔的那個點。 例如，對應至上面圖表中之非線性點的節點可由下列圖表來表示。 兩個方程式代表兩條線的迴歸方程式。  
  
 ![表示非線性點的方程式](../media/regression-tree2.gif "表示非線性點的方程式")  
  
## <a name="data-required-for-decision-tree-models"></a>決策樹模型所需的資料  
 當您準備資料以供決策樹模型使用時，應該要了解特定演算法的需求，包括所需的資料量及資料的使用方式等。  
  
 決策樹模型的需求如下：  
  
-   **單一索引鍵資料行** ：每個模型都必須包含一個能唯一識別每一筆記錄的數值或文字資料行。 不允許複合的索引鍵。  
  
-   **可預測資料行** ：至少需要一個可預測資料行。 您可以在模型中加入多個可預測的屬性，而且這些可預測的屬性可以屬於不同的類型：數值或離散。 不過，增加可預測屬性的數目可能會增加處理時間。  
  
-   **輸入資料行** ：需要可以是離散或連續的輸入資料行。 增加輸入屬性的數目會影響處理時間。  
  
 如需決策樹模型所支援之內容類型和資料類型的詳細資訊，請參閱 [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)的＜需求＞一節。  
  
## <a name="viewing-a-decision-trees-model"></a>檢視決策樹模型  
 若要瀏覽此模型，您可以使用 [Microsoft 樹狀檢視器]  。 如果模型產生了多個樹狀目錄，您就可以選取一個樹狀目錄，然後此檢視器會顯示這些案例如何針對每個可預測屬性分類的細目。 您也可以使用相依性網路檢視器來檢視樹狀目錄的互動。 如需詳細資訊，請參閱 [使用 Microsoft 樹狀檢視器瀏覽模型](browse-a-model-using-the-microsoft-tree-viewer.md)。  
  
 如果您想要了解樹狀結構中任何分支或節點的詳細資料，也可以使用 [Microsoft 一般內容樹狀檢視器](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)來瀏覽此模型。 針對此模型所儲存的內容包括每個節點中所有值的分佈、樹狀目錄之每個層級的機率，以及其連續屬性的迴歸公式。 如需詳細資訊，請參閱 [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
## <a name="creating-predictions"></a>建立預測  
 在此模型已處理之後，結果會儲存成一組模式和統計資料，供您瀏覽關聯性或進行預測。  
  
 如需要搭配決策樹模型使用之查詢的範例，請參閱 [決策樹模型查詢範例](decision-trees-model-query-examples.md)。  
  
 如需如何針對採礦模型建立查詢的一般資訊，請參閱 [資料採礦查詢](data-mining-queries.md)。  
  
## <a name="remarks"></a>備註  
  
-   支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
-   支援鑽研。  
  
-   支援 OLAP 採礦模型的使用和資料採礦維度的建立。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)   
 [決策樹模型查詢範例](decision-trees-model-query-examples.md)   
 [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
