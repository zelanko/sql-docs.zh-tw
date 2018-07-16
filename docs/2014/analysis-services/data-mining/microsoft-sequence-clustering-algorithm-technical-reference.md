---
title: Microsoft 時序群集演算法技術參考 |Microsoft Docs
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
- MAXIMUM_SEQUENCE_STATES parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_STATES parameter
- sequence clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: 251c369d-6b02-4687-964e-39bf55c9b009
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 29cb245c65976e517aad12ecae636df264dda9d7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37242008"
---
# <a name="microsoft-sequence-clustering-algorithm-technical-reference"></a>Microsoft 時序群集演算法技術參考
  Microsoft 時序叢集演算法是一種混合式演算法，它使用 Markov 鏈結分析來識別已排序的時序，並結合此分析的結果與叢集技術，根據模型中的時序和其他屬性產生叢集。 本主題描述演算法的實作、如何自訂演算法，以及時序叢集模型的特殊需求。  
  
 如需有關演算法的一般詳細資訊，包括如何瀏覽和查詢時序叢集模型，請參閱＜ [Microsoft Sequence Clustering Algorithm](microsoft-sequence-clustering-algorithm.md)＞。  
  
## <a name="implementation-of-the-microsoft-sequence-clustering-algorithm"></a>Microsoft 時序群集演算法的實作  
 Microsoft 時序叢集模型使用 Markov 模型來識別時序，並判斷時序的機率。 Markov 模型是一種導向圖形，可儲存不同狀態間的轉換。 Microsoft 時序叢集演算法使用 n 順序的 Markov 鏈結，而非隱藏的 Markov 模型。  
  
 Markov 鏈結中的順序數目會告訴您使用多少個狀態判斷目前狀態的機率。 在第一優先順序的 Markov 模型中，目前狀態的機率僅取決於先前的狀態。 在第二優先順序的 Markov 鏈結中，狀態的機率取決於先前的兩個狀態，以此類推。 轉換矩陣會針對每個 Markov 鏈結儲存每個狀態組合的轉換。 當 Markov 鏈結的長度增加時，矩陣的大小也會以指數方式增加，而且該矩陣會變得相當疏鬆。 處理時間也會等比例地增加。  
  
 這可能有助於使用點選流分析的範例視覺化鏈結，以分析網頁的查閱次數。 每個使用者都會針對每個工作階段建立一長串的點選。 當您建立模型來分析網站上的使用者行為時，用於定型的資料集就是轉換為圖形的一連串 URL，其中包含相同點選路徑之所有執行個體的計數。 例如，此圖形包含使用者從第 1 頁移到第 2 頁的機率 (10%)、使用者從第 1 頁移到第 3 頁的機率 (20%) 等等。 當您將所有可能的路徑與路徑片段放在一起時，您會取得可能比任何單一已觀察路徑更長、更複雜的圖形。  
  
 根據預設，Microsoft 時序群集演算法使用 Expectation Maximization (EM) 群集方法。 如需詳細資訊，請參閱 [Microsoft 群集演算法技術參考](microsoft-clustering-algorithm-technical-reference.md)。  
  
 群集的目標為循序與非循序屬性。 每個群集都會使用機率分配隨機選取。 每個群集都有一個代表一組完整路徑的 Markov 鏈結，以及包含時序狀態轉換和機率的矩陣。 根據初始分配，貝氏機率分類規則用於計算特定群集中任何屬性的機率，包括時序。  
  
 Microsoft 時序叢集演算法支援模型額外的非循序屬性。 也就是說，這些額外的屬性會結合時序屬性，就像在一般叢集模型般建立具有類似屬性之案例的群集。  
  
 時序群集模型傾向於建立比一般叢集模型還要更多的叢集。 因此，Microsoft 時序群集演算法會根據時序及其他屬性執行 *「群集分解」*(Cluster Decomposition) 來分割群集。  
  
### <a name="feature-selection-in-a-sequence-clustering-model"></a>時序叢集模型中的特徵選取  
 特徵選取不會在建立時序時叫用，但是特徵選取會在群集階段套用。  
  
|模型類型|特徵選取方法|註解|  
|----------------|------------------------------|--------------|  
|時序群集|未使用|尚未叫用特徵選取。不過，您可以藉由設定 MINIMUM_SUPPORT 和 MINIMUM_PROBABILIITY 參數的值，控制演算法的行為。|  
|群集|有趣性分數|雖然群集演算法可以使用離散或離散化的演算法，但每個屬性的分數都會計算為距離，而且是連續的；因此會使用有趣性分數。|  
  
 如需詳細資訊，請參閱 [Feature Selection](../../sql-server/install/feature-selection.md)。  
  
### <a name="optimizing-performance"></a>最佳化效能  
 Microsoft 時序群集演算法支援各種最佳化處理的方式：  
  
-   設定 CLUSTER_COUNT 參數的值來控制所產生之群集的數目。  
  
-   增加 MINIMUM_SUPPORT 參數的值來減少當做屬性加入之時序的數目。 因此，系統會刪除極少數的序列。  
  
-   處理模型前，將相關的屬性分組來降低複雜度。  
  
 一般而言，您可以利用數種方式，使 n 順序 Markov 鏈結模式的效能最佳化：  
  
-   控制可能時序的長度。  
  
-   以程式設計方式減少 n 的值。  
  
-   只儲存超過指定之臨界值的機率。  
  
 這些方法的完整討論超出本主題的範圍。  
  
## <a name="customizing-the-sequence-clustering-algorithm"></a>自訂時序群集演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。 您也可以設定控制演算法處理定型資料之方式的模型旗標，修改已完成之模型的行為。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可搭配 Microsoft 時序群集演算法使用的參數。  
  
 CLUSTER_COUNT  
 指定演算法要建立的大約群集數目。 如果無法從資料建立大約群集數目，則演算法會盡可能建立最多的群集。 將 CLUSTER_COUNT 參數設定為 0，會導致演算法使用啟發式來判斷可建立的最佳群集數目。  
  
 預設值是 10。  
  
> [!NOTE]  
>  指定非零的數字做為演算法的提示，這樣會繼續尋找指定之數字的目標，但最後可能會找到更多或更少的結果。  
  
 MINIMUM_SUPPORT  
 指定支援屬性建立群集所需之案例的最小數目。  
  
 預設值是 10。  
  
 MAXIMUM_SEQUENCE_STATES  
 指定一個順序可以具有的最大狀態數目。  
  
 將此值設定為大於 100 的數字，可能會導致演算法建立一個無法提供有用資訊的模型。  
  
 預設值為 64。  
  
 MAXIMUM_STATES  
 針對演算法支援的非順序屬性指定最大狀態數目。 如果非循序屬性的狀態數目大於狀態的最大數目，演算法會使用屬性最常用的狀態，並將其餘狀態視為`Missing`。  
  
 預設值為 100。  
  
### <a name="modeling-flags"></a>模型旗標  
 下列模型旗標受到支援，可搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序叢集演算法使用。  
  
 NOT NULL  
 表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。  
  
 適用於採礦結構資料行。  
  
 MODEL_EXISTENCE_ONLY  
 表示資料行將被視為擁有兩個可能狀態：`Missing`和`Existing`。 Null 值會被視為`Missing`值。  
  
 適用於採礦模型資料行。  
  
 如需如何在採礦模型中使用 Missing 值，以及遺漏值如何影響機率分數的詳細資訊，請參閱[遺漏值&#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)。  
  
## <a name="requirements"></a>需求  
 案例資料表必須有一個案例識別碼資料行。 案例資料表可以選擇性地包含儲存案例之相關屬性的其他資料行。  
  
 Microsoft 時序群集演算法需要儲存為巢狀資料表的時序資訊。 巢狀資料表必須有一個單一的 Key Sequence 資料行。 A`Key Sequence`資料行可以包含任何類型的資料，可以進行排序，包括字串資料類型，但資料行必須包含每個案例的唯一值。 此外，處理模型前，您必須確認案例資料表與巢狀資料表都根據與資料表相關的索引鍵，以遞增方式排序。  
  
> [!NOTE]  
>  如果您建立使用 Microsoft 時序演算法但不使用時序資料行的模型，所產生的模型將不包含任何時序，但是將只根據模型中包含的其他屬性群集案例。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法支援下表所列的特定輸入資料行和可預測資料行。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
|「資料行」|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Cyclical、Discrete、Discretized、Key、Key Sequence、Table 和 Ordered|  
|可預測屬性|Continuous、Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
## <a name="remarks"></a>備註  
  
-   請使用 [PredictSequence &#40;DMX&#41;](/sql/dmx/predictsequence-dmx) 函數以預測時序。 如需版本的詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，支援時序預測，請參閱 <<c2> [ 支援的 SQL Server 2012 的版本功能](http://go.microsoft.com/fwlink/?linkid=232473)(http://go.microsoft.com/fwlink/?linkid=232473)。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序叢集演算法不支援使用預測模型標記語言 (PMML) 來建立採礦模型。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 時序群集演算法支援鑽研、OLAP 採礦模型的使用，以及資料採礦維度的使用。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 時序群集演算法](microsoft-sequence-clustering-algorithm.md)   
 [時序叢集模型查詢範例](clustering-model-query-examples.md)   
 [時序群集模型的採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-for-sequence-clustering-models.md)  
  
  
