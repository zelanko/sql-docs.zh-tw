---
title: Microsoft 貝氏機率分類演算法技術參考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MINIMUM_DEPENDENCY_PROBABILITY parameter
- MAXIMUM_INPUT_ATTRIBUTES parameter
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- MAXIMUM_OUTPUT_ATTRIBUTES parameter
- MAXIMUM_STATES parameter
ms.assetid: a4cd47fe-2127-4930-b18f-3edd17ee9a65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5d69af9ad01e001394836449f97c48b4dae8dab7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62734821"
---
# <a name="microsoft-naive-bayes-algorithm-technical-reference"></a>Microsoft 貝氏機率分類演算法技術參考
   [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所提供用於預測模型的分類演算法。 此演算法會計算輸入資料行和可預測資料行之間的條件式機率，並假設資料行是獨立的。 這種獨立性假設產生了貝氏機率分類這個名稱。  
  
## <a name="implementation-of-the-microsoft-naive-bayes-algorithm"></a>Microsoft 貝氏機率分類演算法的實作  
 此演算法比其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法更少計算，因此對於快速產生採礦模型來探索輸入資料行和可預測資料行之間的關聯性很有用。 此演算法會考量輸入屬性值與輸出屬性值的每個配對。  
  
 貝氏理論的數學屬性描述超出本文件中; 的範圍如需詳細資訊，請參閱 Microsoft Research 報告中的[學習 Bayesian 網路：知識與統計資料的組合](https://go.microsoft.com/fwlink/?LinkId=207029)。  
  
 如需調整所有模型中的機率來表示可能遺漏值的描述，請參閱[遺漏值 &#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)。  
  
### <a name="feature-selection"></a>特徵選取  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法會執行自動特徵選取，藉以限制建立模型時所考量的值數目。 如需詳細資訊，請參閱[特徵選取 &#40;資料採礦&#41;](feature-selection-data-mining.md)。  
  
|演算法|分析的方法|註解|  
|---------------|------------------------|--------------|  
|貝氏機率分類|Shannon 熵<br /><br /> 使用 K2 優先的貝氏<br /><br /> 使用優先統一狄氏分配的貝氏 (預設值)|貝氏機率分類只接受離散或離散化的屬性，因此無法使用有趣性分數。|  
  
 此演算法的設計會將處理時間降至最低，並可有效地選取重要性最高的屬性，不過，您可以設定參數來控制此演算法所使用的資料，如下所示：  
  
-   若要限制當做輸入使用的值，減少 MAXIMUM_INPUT_ATTRIBUTES 的值。  
  
-   若要限制模型分析的屬性數目，減少 MAXIMUM_OUTPUT_ATTRIBUTES 的值。  
  
-   若要限制可以針對任何一個屬性考量的值數目，減少 MINIMUM_STATES 的值。  
  
## <a name="customizing-the-naive-bayes-algorithm"></a>自訂貝氏機率分類演算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法支援數個會影響所產生之採礦模型的行為、效能和精確度的參數。 您也可以設定模型資料行上的模型旗標來控制處理資料的方式，或設定採礦結構上的旗標來指定處理遺漏值或 Null 值的方式。  
  
### <a name="setting-algorithm-parameters"></a>設定演算法參數  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法支援數個會影響所產生之採礦模型的效能和精確度的參數。 下表描述每一個參數。  
  
 *MAXIMUM_INPUT_ATTRIBUTES*  
 指定在叫用特徵選取之前，演算法可以處理輸入屬性的最大數目。 將此值設定為 0，會停用輸入屬性的特徵選取。  
  
 預設值是 255。  
  
 *MAXIMUM_OUTPUT_ATTRIBUTES*  
 指定在叫用特徵選取之前，演算法可以處理輸出屬性的最大數目。 將此值設定為 0，會停用輸出屬性的特徵選取。  
  
 預設值是 255。  
  
 *MINIMUM_DEPENDENCY_PROBABILITY*  
 指定介於輸入和輸出屬性之間的最小相依機率。 這個值會用來限制演算法所產生之內容的大小。 此屬性可設定為 0 到 1。 越大的值會減少模型內容中的屬性數目。  
  
 預設值是 0.5。  
  
 *MAXIMUM_STATES*  
 指定演算法所支援之屬性狀態的最大數目。 如果屬性擁有的狀態數目大於狀態的最大數目，演算法會使用屬性最常用的狀態，並將其餘狀態視為遺漏。  
  
 預設值為 100。  
  
### <a name="modeling-flags"></a>模型旗標  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法支援下列模型旗標。 當您建立採礦結構或採礦模型時，您會定義模型旗標來指定分析期間要如何處理每個資料行中的值。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](modeling-flags-data-mining.md)。  
  
|模型旗標|描述|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|表示資料行都會被視為擁有兩個可能狀態：遺失，且現有的。 Null 為遺漏值。<br /><br /> 適用於採礦模型資料行。|  
|NOT NULL|表示資料行不能包含 Null 值。 如果 Analysis Services 在模型定型期間遇到 Null 值，將會產生錯誤。<br /><br /> 適用於採礦結構資料行。|  
  
## <a name="requirements"></a>需求  
 貝氏機率分類樹狀模型必須包含索引鍵資料行、至少一個可預測屬性，以及至少一個輸入屬性。 任何屬性都不得為連續的；如果您的資料包含連續數值資料，將會忽略或離散化該資料。  
  
### <a name="input-and-predictable-columns"></a>輸入和可預測資料行  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法支援下表所列的特定輸入資料行和可預測資料行。 如需內容類型用於採礦模型時所代表意義的詳細資訊，請參閱[內容類型 &#40;資料採礦&#41;](content-types-data-mining.md)。  
  
|「資料行」|內容類型|  
|------------|-------------------|  
|輸入屬性|Cyclical、Discrete、Discretized、Key、Table 和 Ordered|  
|可預測屬性|Cyclical、Discrete、Discretized、Table 和 Ordered|  
  
> [!NOTE]  
>  系統支援 Cyclical 和 Ordered 內容類型，但是演算法將它們視為離散值，因此不會執行特殊處理。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 貝氏機率分類演算法](microsoft-naive-bayes-algorithm.md)   
 [Naive Bayes Model Query Examples](naive-bayes-model-query-examples.md)   
 [貝氏機率分類模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
