---
title: Microsoft 決策樹演算法技術參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MAXIMUM_INPUT_ATTRIBUTES parameter
- SPLIT_METHOD parameter
- MINIMUM_SUPPORT parameter
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- FORCED_REGRESSOR parameter
- decision tree algorithms [Analysis Services]
- decision trees [Analysis Services]
- COMPLEXITY_PENALTY parameter
- SCORE_METHOD parameter
ms.assetid: 1e9f7969-0aa6-465a-b3ea-57b8d1c7a1fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e58f43c7004f94aeff81d9ac43a9c9c2804b184
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722000"
---
# <a name="microsoft-decision-trees-algorithm-technical-reference"></a>Microsoft 決策樹演算法技術參考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法是一種混合式演算法，其中併入建立樹狀結構的不同方法，並支援多種分析工作，包括迴歸、分類以及關聯。 Microsoft 決策樹演算法支援製作離散和連續屬性的模型。  
  
 本主題說明演算法的實作、描述如何針對不同的工作自訂演算法的行為，以及提供查詢決策樹模型其他資訊的連結。  
  
## <a name="implementation-of-the-decision-trees-algorithm"></a>實作決策樹演算法  
 Microsoft 決策樹演算法將貝氏方法套用至學習因果互動模型，取得模型的近似事後分佈。 如需這種方法的詳細說明，請參閱 Microsoft Research 網站上由 [結構和參數學習](https://go.microsoft.com/fwlink/?LinkId=237640&clcid=0x409)提供的文件。  
  
 評估學習所需之 *「優先」* (Priors) 資訊值的方法，是根據 *「可能性相等」*(Likelihood Equivalence) 的假設。 此假設認為，資料無法協助您區分代表條件式獨立之相同判斷提示的網路結構。 每個案例都假設擁有一個單一的貝氏優先網路以及對於該網路之信心的單一量值。  
  
 使用這些優先網路，演算法就可以根據目前的定型資料，計算網路結構的相對 *「事後機率」* (Posterior Probabilities)，並識別事後機率最高的網路結構。  
  
 Microsoft 決策樹演算法使用不同的方法計算最佳的樹狀結構。 所使用的方法取決於工作，這可以是線性迴歸、分類或關聯分析。 單一模型可以包含不同可預測屬性的多個樹狀結構。 此外，根據資料中的屬性和值數目，每個樹狀結構都可以包含多個分支。 在特定模型中建立的樹狀結構形狀和深度取決於所使用的計分方法與其他參數。 參數中的變更也可能影響節點分岔的位置。  
  
### <a name="building-the-tree"></a>建立樹狀結構  
 當 Microsoft 決策樹演算法建立一組可能的輸入值時，該演算法會執行 *feature selection* 來識別提供多數資訊的屬性和值，並移除值非常稀少的考量。 此演算法也會將這些值分組到 *bin*中，以建立可以當做一個單位處理之值的群組，讓效能最佳化。  
  
 樹狀結構可以透過決定輸入和目標結果間的關聯來建立。 讓所有屬性產生關聯之後，此演算法會找出最清楚分隔結果的單一屬性。 最佳分隔的這個點會使用計算資訊改善的方程式測量。 擁有資訊改善最佳分數的屬性用於將案例分割為子集，然後透過相同的程序進行遞迴性分析，直到無法再分割樹狀結構為止。  
  
 用於評估資訊改善的完整方程式取決於建立演算法時所設定的參數、可預測資料行的資料類型，以及輸入的資料類型。  
  
### <a name="discrete-and-continuous-inputs"></a>離散和連續輸入  
 當可預測的屬性和輸入都是離散的時，每個輸入的計算結果就是建立矩陣，並在矩陣中建立每個資料格之分數的結果。  
  
 不過，當可預測的屬性是離散的，而輸入是連續的時，就會將連續資料行的輸入自動離散化。 您可以接受預設值，並讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 尋找最佳的 bin 數目，或者您可以設定 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 屬性來控制將連續輸入分隔的方式。 如需詳細資訊，請參閱 [變更採礦模型中的資料行分隔](change-the-discretization-of-a-column-in-a-mining-model.md)。  
  
 針對連續屬性，此演算法使用線性迴歸來決定決策樹分岔之處。  
  
 當可預測的屬性是連續數值資料類型時，也會將特徵選取套用到輸出中，以降低可能的結果數目並讓模型的建立更為快速。 您可以變更特徵選取的臨界值，並藉此設定 MAXIMUM_OUTPUT_ATTRIBUTES 參數來增加或減少可能值的數目。  
  
 如需有關如何搭配使用的詳細說明[!INCLUDE[msCoName](../../includes/msconame-md.md)]決策樹演算法如何與分隔可預測資料行，請參閱[學習 Bayesian 網路：知識與統計資料的組合](https://go.microsoft.com/fwlink/?LinkId=45963)。 如需 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法如何與連續可預測資料行一起運作的詳細資訊，請參閱 [Autoregressive Tree Models for Time-Series Analysis](https://go.microsoft.com/fwlink/?LinkId=45966)(時間序列分析的自動迴歸樹狀模型) 的附錄。  
  
### <a name="scoring-methods-and-feature-selection"></a>計分方法與特徵選取  
 Microsoft 決策樹演算法提供三個資訊改善的公式：Shannon 的 entropy、 Bayesian 網路 K2 prior 和統一狄氏分配 Bayesian 網路。 三種方法全都堅實的建立在資料採礦欄位中。 建議您試驗不同的參數與計分方法來判斷哪個公式會提供最佳的結果。 如需有關這些計分方法的詳細資訊，請參閱＜ [Feature Selection](../../sql-server/install/feature-selection.md)＞。  
  
 所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦演算法都會自動使用特徵選取來改善分析並減少處理的負載。 特徵選取所使用的方法取決於建立模型所使用的演算法。 針對決策樹模型控制特徵選取的演算法參數為 MAXIMUM_INPUT_ATTRIBUTES 和 MAXIMUM_OUTPUT。  
  
|演算法|分析的方法|註解|  
|---------------|------------------------|--------------|  
|決策樹|有趣性分數<br /><br /> Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|如果任何資料行包含非二進位連續數值，則所有資料行都會使用有趣性分數以確保一致性。 否則，會使用預設值或指定的方法。|  
|線性迴歸|有趣性分數|線性迴歸只會使用有趣性，因為它只支援連續的資料行。|  
  
### <a name="scalability-and-performance"></a>延展性和效能  
 分類是一個重要的資料採擷策略。 一般而言，為案例分類所需之資訊的數量會以輸入記錄數目的直接比例成本。 這會限制可以分類之資料的大小。 Microsoft 決策樹演算法使用下列方法解決這些問題、改善效能，並排除記憶體限制。  
  
-   特徵選取，用於最佳化屬性選取。  
  
-   貝氏計分，用於控制樹狀結構的成長。  
  
-   bin 最佳化，用於連續屬性。  
  
-   輸入值的動態群組，用於判斷最重要的值。  
  
 Microsoft 決策樹演算法快速、可擴充，而且針對輕鬆平行處理而設計，也就是說，所有處理器會一同運作以建立單一而且一致的模型。 這些特徵的結合可讓決策樹分類成為資料採礦的理想工具。  
  
 如果效能限制嚴苛，您可以在定期決策樹模型期間，使用下列方法改善處理時間。 不過，如果您這麼做，請注意，刪除屬性來改善處理效能將會變更模型的結果，而且可能比較不能代表總母體。  
  
-   增加 COMPLEXITY_PENALTY 參數的值來限制樹狀結構的成長。  
  
-   限制關聯模型中的項目數目以限制所建立的樹狀結構數目。  
  
-   增加 MINIMUM_SUPPORT 參數的值以防止過度膨脹。  
  
-   將任何屬性之離散值的數目限制為 10 以下。 您可以嘗試在不同的模型中，嘗試以不同的方式為這些值分組。  
  
    > [!NOTE]  
    >  您可以使用  [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 中所提供的資料瀏覽工具，將資料中的值分佈視覺化，並在開始資料採礦前，將您的值正確分組。 如需詳細資訊，請參閱 [資料分析工作和檢視器](../../integration-services/control-flow/data-profiling-task-and-viewer.md)。 您也可以使用 [適用於 Excel 2007 的資料採礦增益集](https://www.microsoft.com/downloads/details.aspx?FamilyID=7C76E8DF-8674-4C3B-A99B-55B17F3C4C51)瀏覽、分組，以及重新標示 Microsoft Excel 中的資料。  
  
## <a name="customizing-the-decision-trees-algorithm"></a>自訂決策樹演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法支援會影響所產生之採礦模型效能和精確度的參數。 您也可以設定採礦模型資料行或採礦結構資料行上的模型旗標來控制處理資料的方式。  
  
> [!NOTE]  
>  Microsoft 決策樹演算法可用於所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中，但是 Microsoft 決策樹演算法自訂行為的某些進階參數只能在特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中使用。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本支援的功能清單，請參閱 [SQL Server 2012 版本支援的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 下表描述可以搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法使用的參數。  
  
 *COMPLEXITY_PENALTY*  
 控制決策樹的成長。 低值會增加分岔數目，而高值會減少分岔數目。 預設值是依據特定模型的屬性數目，如下列清單所述：  
  
-   1 到 9 個屬性，預設值為 0.5。  
  
-   10 到 99 個屬性，預設值為 0.9。  
  
-   100 個以上的屬性，預設值為 0.99。  
  
 *FORCE_REGRESSOR*  
 強制演算法使用指定的資料行做為迴歸輸入變數，不考慮演算法計算出來之資料行的重要性。 此參數只用於預測連續屬性的決策樹。  
  
> [!NOTE]  
>  您可以設定這個屬性來強制演算法嘗試使用屬性當做迴歸輸入變數。 不過，屬性實際上在最終模型中是否當做迴歸輸入變數使用，則視分析的結果而定。 您可以查詢模型內容，找出當做迴歸輸入變數使用的資料行。  
  
 [只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中才可使用]  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 定義演算法在叫用特徵選取之前，可以處理的輸入屬性數目。  
  
 預設值是 255。  
  
 將此值設定為 0 可關閉特徵選取。  
  
 [只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用]  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 定義演算法在叫用特徵選取之前，可以處理的輸出屬性數目。  
  
 預設值是 255。  
  
 將此值設定為 0 可關閉特徵選取。  
  
 [只有在某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中才可使用]  
  
 *MINIMUM_SUPPORT*  
 決定要在決策樹中產生分岔所需的最小分葉案例數目。  
  
 預設值是 10。  
  
 如果資料集非常大，您可能需要增加這個值以防止過度膨脹。  
  
 *SCORE_METHOD*  
 決定用來計算分岔準則的方法。 下列是可以使用的選項：  
  
|ID|名稱|  
|--------|----------|  
|1|熵|  
|3|使用 K2 優先的貝氏|  
|4|使用統一優先的貝氏狄氏等價 (Bayesian Dirichlet Equivalent，BDE)<br /><br /> (預設值)|  
  
 預設值是 4 或 BDE。  
  
 如需這些計分方法的說明，請參閱＜ [Feature Selection](../../sql-server/install/feature-selection.md)＞。  
  
 *SPLIT_METHOD*  
 決定用來分岔節點的方法。 下列是可以使用的選項：  
  
|ID|名稱|  
|--------|----------|  
|1|**二進位：** 表示，無論屬性值的實際數目，樹狀結構都會分岔為兩個分支。|  
|2|**完成：** 表示樹狀結構可以建立有屬性值的分岔。|  
|3|**兩者：** 指定 Analysis Services 可以決定是否應該使用二進位還是完整分岔來產生最佳的結果。|  
  
 預設值是 3。  
  
### <a name="modeling-flags"></a>模型旗標  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法支援下列模型旗標。 當您建立採礦結構或採礦模型時，您會定義模型旗標來指定分析期間要如何處理每個資料行中的值。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](modeling-flags-data-mining.md)。  
  
|模型旗標|描述|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|表示資料行將被視為擁有兩個可能狀態：`Missing` 和 `Existing`。 Null 為遺漏值。<br /><br /> 適用於採礦模型資料行。|  
|NOT NULL|表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。<br /><br /> 適用於採礦結構資料行。|  
  
### <a name="regressors-in-decision-tree-models"></a>決策樹模型中的迴歸輸入變數  
 即使您不使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法，包含連續數值輸入和輸出的任何決策樹模型潛在可能包含代表連續屬性迴歸的節點。  
  
 您不需要指定連續數值資料的資料行代表迴歸輸入變數。 即使未在資料行上設定 REGRESSOR 旗標， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法也會自動使用資料行當做潛在迴歸輸入變數，並將資料集分割成具備有意義之模式的區域。  
  
 不過，您可以使用 FORCE_REGRESSOR 參數來確保演算法會使用特定的迴歸輸入變數。 這個參數僅能搭配 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法使用。 當您設定模型旗標時，此演算法會嘗試尋找形式的迴歸方程式 * C1 + b\*C2 +...以樹狀結構的節點中符合模式。 之後會計算剩餘數的總和，如果差異過大，就會在樹狀結構中強制進行分割。  
  
 例如，如果您要使用 **Income** 做為屬性來預測客戶購買行為，且在資料行上設定 REGRESSOR 模型旗標，則演算法首先會使用標準迴歸公式來比對 **Income** 值。 如果差異過大，就會放棄迴歸公式，且根據其他的屬性分割樹狀結構。 在分割之後，決策樹演算法就會接著嘗試在每個分支中比對迴歸輸入變數與收入。  
  
## <a name="requirements"></a>需求  
 決策樹模型必須包含索引鍵資料行、輸入資料行和至少一個可預測資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法支援下表所列的特定輸入資料行和可預測資料行。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
|「資料行」|內容類型|  
|------------|-------------------|  
|輸入屬性|Continuous、Cyclical、Discrete、Discretized、Key、Ordered、Table|  
|可預測屬性|Continuous、Cyclical、Discrete、Discretized、Ordered、Table|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)   
 [決策樹模型查詢範例](decision-trees-model-query-examples.md)   
 [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
