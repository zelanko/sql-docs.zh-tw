---
title: "Microsoft 關聯分析演算法技術參考 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MINIMUM_ITEMSET_SIZE parameter
- MAXIMUM_SUPPORT parameter
- association algorithms [Analysis Services]
- MINIMUM_SUPPORT parameter
- OPTIMIZED_PREDICTION_COUNT parameter
- associations [Analysis Services]
- MAXIMUM_ITEMSET_COUNT parameter
- MAXIMUM_ITEMSET_SIZE parameter
- MINIMUM_PROBABILITY parameter
ms.assetid: 50a22202-e936-4995-ae1d-4ff974002e88
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a029a6efad9ebdbc15e42d593db28f9530b1b8e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="microsoft-association-algorithm-technical-reference"></a>Microsoft 關聯分析演算法技術參考
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法是有名的 Apriori 演算法的簡單實作。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法都可用來分析關聯，但每個演算法所找到的規則都可能不同。 在決策樹模型中，導致特定規則的分岔是根據資訊改善而定，在關聯模型中，規則則是完全根據信心而定。 因此，在關聯模型中，強大的規則或具有高信心指數的規則可能因為沒有提供新資訊而不具有高「有趣性」。  
  
## <a name="implementation-of-the-microsoft-association-algorithm"></a>Microsoft 關聯分析演算法的實作  
 Apriori 演算法並不會分析模式，而是產生「候選項目集」並接著加以計算。 項目可能代表事件、產品或屬性的值，根據分析的資料類型而定。  
  
 在常見類型的關聯模型中，代表「是/否」或「遺漏/現有」值的布林值變數會指派給每個屬性，例如產品或事件名稱。 購物籃分析是關聯規則模型的其中一個範例，該模型使用布林值變數代表客戶購物籃中的特定產品是否存在。  
  
 接著，演算法會針對每個項目集建立代表支援及信心的分數。 這些分數可用來從項目集衍生有趣性規則並排列其次序。  
  
 您也可以針對數值屬性建立關聯模型。 如果是連續屬性，可以將數字「分隔」或群組到值區中。 接著就可以將離散化的值當做布林值或屬性值配對處理。  
  
### <a name="support-probability-and-importance"></a>支援、機率和重要性  
 「支援」(有時也稱為「頻率」) 代表包含目標項目或項目組合的案例數。 只有至少具有指定支援量的項目才能包含在模型中。  
  
 「常見項目集」代表項目的集合，其中的項目組合也具有 MINIMUM_SUPPORT 參數所定義臨界值以上的支援。 例如，如果項目集為 {A,B,C} 而 MINIMUM_SUPPORT 值為 10，則每個個別的 A、B 及 C 項目都必須至少存在於模型所含的 10 個案例中，且項目組合 {A,B,C} 也必須存在於至少 10 個案例中。  
  
 **注意** ：您也可以指定項目集的最大長度 (長度代表項目數) 來控制採礦模型中的項目集數目。  
  
 根據預設，任何特定項目或項目集的支援都代表包含該項目或項目集的案例計數。 不過，您也可以將數字輸入為小於 1 的小數值，將 MINIMUM_SUPPORT 表示為資料集總案例數的百分比。 例如，如果將 MINIMUM_SUPPORT 值指定為 0.03，該值代表資料集中至少有 3% 的總案例數必須包含此項目或項目集，才能加入模型。 您應該試用模型，以判斷是計數或是百分比比較適用。  
  
 相反地，規則的臨界值不會表示為計數或百分比，而是以機率表示，這有時也稱為「信心」。 例如，如果項目集 {A,B,C} 出現在 50 個案例中，但項目 {A,B,D} 也出現在 50 個案例中，而項目集 {A,B} 則出現在另外 50 個案例中，則很明顯地 {A,B} 並不能準確地預測 {C}。 因此，為了針對所有已知結果來計算特定結果的加權， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會使用項目集 {A,B,C} 的支援除以所有相關項目集的支援來計算個別規則的機率 (例如 If {A,B} Then {C})。  
  
 您也可以藉由設定 MINIMUM_PROBABILITY 的值來限制模型所產生的規則數。  
  
 對於每個建立的規則，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 都會輸出分數指出其「重要性」，也稱為「增益」。 項目集和規則的增益重要性計算方式不同。  
  
 項目集的重要性計算方式是用項目集的機率除以項目集中個別項目的複合機率。 例如，如果項目集包含 {A,B}，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會先計算所有包含此 A 和 B 組合的案例數，並將該值除以總案例數，然後再正規化為機率。  
  
 規則的重要性則是在已知規則左側的情況下，用規則右側的對數可能性來計算。 例如，在規則 `If {A} Then {B}`中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會計算具有 A 和 B 的案例對於具有 B 但沒有 A 的案例的比率，然後再使用對數刻度將該比率正規化。  
  
### <a name="feature-selection"></a>特徵選取  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法不會執行任何類型的自動特徵選取， 而是提供參數來控制演算法所使用的資料。 這可能包含每個項目集大小的限制，或者將項目集加入至模型時所需最大及最小支援的設定。  
  
-   若要篩選出太平常以致於不有趣的項目集事件，請減少 MAXIMUM_SUPPORT 的值，以從模型中移除太常出現的項目集。  
  
-   若要篩選出很少見的項目和項目集，請增加 MINIMUM_SUPPORT 的值。  
  
-   若要篩選出規則，請增加 MINIMUM_PROBABILITY 的值。  
  
## <a name="customizing-the-microsoft-association-rules-algorithm"></a>自訂 Microsoft 關聯規則演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 您可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的資料採礦設計師，隨時變更採礦模型的參數。 您也可以變更參數以程式設計方式使用<xref:Microsoft.AnalysisServices.MiningModel.AlgorithmParameters%2A>集合在 AMO 中，或使用[MiningModels 元素 &#40;ASSL &#41;](../../analysis-services/scripting/collections/miningmodels-element-assl.md) XMLA 中。 下表描述每一個參數。  
  
> [!NOTE]  
>  您不能使用 DMX 陳述式變更現有模型中的參數；而必須在建立模型時，在 DMX CREATE MODEL 或 ALTER STRUCTURE… ADD MODEL 中指定參數。  
  
 *MAXIMUM_ITEMSET_COUNT*  
 指定要產生的最大項目集數目。 如果沒有指定任何數目，則會使用預設值。  
  
 預設值是 200000。  
  
> [!NOTE]  
>  項目集是由支援排序。 在擁有相同支援的項目集中具有任意的排序。  
  
 *MAXIMUM_ITEMSET_SIZE*  
 指定項目集內所允許的最大項目數。 將此值設定為 0，即代表項目集沒有大小限制。  
  
 預設值是 3。  
  
> [!NOTE]  
>  減少這個值可能會縮短建立模型所需的時間，因為在達到限制時，模型的處理就會停止。  
  
 *MAXIMUM_SUPPORT*  
 指定項目集可支援的最大案例數目。 這個參數可用來排除經常出現的項目，因此可能沒有什麼意義。  
  
 如果此值小於 1，則此值代表總案例數的百分比。 大於 1 的值代表可包含項目集的絕對案例數目。  
  
 預設值是 1。  
  
 *MINIMUM_ITEMSET_SIZE*  
 指定項目集內所允許的最小項目數目。 如果增加此數目，模型可能會包含較少的項目集。 如果您要忽略單一項目的項目集，舉例來說，則這會很有用。  
  
 預設值是 1。  
  
> [!NOTE]  
>  您不能藉由增加最小值來縮短模型處理時間，因為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在處理中仍需計算單一項目的機率。 不過，將此值設定為較高的值可讓您篩選出較小的項目集。  
  
 *MINIMUM_PROBABILITY*  
 指定規則成立的最小機率。  
  
 例如，如果將此值設定為 0.5，則代表不能產生任何機率小於 50% 的規則。  
  
 預設值是 0.4。  
  
 *MINIMUM_SUPPORT*  
 指定演算法產生規則之前必須包含項目集的最小案例數目。  
  
 如果將此值設定為小於 1，則會以總案例數的百分比來計算最小案例數目。  
  
 如果將此值設定為大於 1 的整數，則會以必須包含項目集的案例計數來計算最小案例數目。 如果記憶體有限，演算法可自動增加此參數的值。  
  
 預設值是 0.03。 也就是說只有至少具有 3% 案例的項目集才能包含在模型中。  
  
 *OPTIMIZED_PREDICTION_COUNT*  
 定義要達成最佳化預測所進行快取的項目數目。  
  
 預設值是 0。 使用預設值時，演算法將會在查詢中產生所要求的預測數目。  
  
 如果您為 *OPTIMIZED_PREDICTION_COUNT,* 指定非零值，即使您要求更多的預測，預測查詢最多也只能傳回指定的項目數。 不過，設定一個值可以增強預測效能。  
  
 例如，如果值設定為 3，則演算法只會快取 3 個項目進行預測。 您將不會看到其他可能等同所傳回之 3 個項目的預測。  
  
### <a name="modeling-flags"></a>模型旗標  
 下列模型旗標受到支援，可用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法。  
  
 NOT NULL  
 表示資料行不能包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在模型定型期間遇到 Null 值，將會產生錯誤。  
  
 適用於採礦結構資料行。  
  
 MODEL_EXISTENCE_ONLY  
 表示資料行將被視為擁有兩個可能狀態： **Missing** 和 **Existing**。 Null 為遺漏值。  
  
 適用於採礦模型資料行。  
  
## <a name="requirements"></a>需求  
 關聯模型必須包含索引鍵資料行、輸入資料行和單一的可預測資料行。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法支援下表所列的特定輸入資料行和可預測資料行。 如需採礦模型中內容類型意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-types-data-mining.md)。  
  
|資料行|內容類型|  
|------------|-------------------|  
|輸入屬性|Cyclical、Discrete、Discretized、Key、Table 和 Ordered|  
|可預測屬性|Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>請參閱＜  
 [Microsoft 關聯分析演算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [關聯模型查詢範例](../../analysis-services/data-mining/association-model-query-examples.md)   
 [關聯模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  

