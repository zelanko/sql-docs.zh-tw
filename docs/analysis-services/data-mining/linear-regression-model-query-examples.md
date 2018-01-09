---
title: "線性迴歸模型查詢範例 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linear regression algorithms [Analysis Services]
- linear regression [Analysis Services]
- content queries [DMX]
ms.assetid: fd3cf312-57a1-44b6-b772-fce6fc1c26d7
caps.latest.revision: "21"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 150ef98bd2c949f7b4eb47170ec7855173608fbc
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="linear-regression-model-query-examples"></a>線性迴歸模型查詢範例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]當您建立針對資料採礦模型的查詢時，您可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，或您可以建立預測查詢，為新的資料進行預測模型中使用的模式。 例如，內容查詢可能會提供有關迴歸公式的其他詳細資料，而預測查詢則會告訴您新資料點是否符合模型。 您也可以使用查詢來擷取有關模型的中繼資料。  
  
 本節說明如何針對以 Microsoft 線性迴歸演算法為基礎的模型來建立查詢。  
  
> [!NOTE]  
>  線性迴歸是以 Microsoft 決策樹演算法的特殊案例為基礎，因此有許多相似處，而且使用連續可預測屬性的某些決策樹模型可以包含迴歸公式。 如需詳細資訊，請參閱 [Microsoft 決策樹演算法技術參考](../../analysis-services/data-mining/microsoft-decision-trees-algorithm-technical-reference.md)。  
  
 **內容查詢**  
  
 [使用資料採礦結構描述資料列集來判斷用於模型的參數](#bkmk_Query1)  
  
 [使用 DMX 傳回模型的迴歸公式](#bkmk_Query2)  
  
 [僅傳回模型的係數](#bkmk_Query3)  
  
 **預測查詢**  
  
 [使用單一查詢預測成果](#bkmk_Query4)  
  
 [搭配迴歸模型使用預測函數](#bkmk_Query5)  
  
##  <a name="bkmk_top"></a> 尋找有關線性迴歸模型的資訊  
 線性迴歸模型的結構相當簡單：採礦模型將資料表示為定義迴歸公式的單一節點。 如需詳細資訊，請參閱 [羅吉斯迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-logistic-regression-models.md)。  
  
 [回頁首](#bkmk_top)  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：使用資料採礦結構描述資料列集來判斷用於模型的參數  
 您可以查詢資料採礦結構描述資料列集來尋找有關模型的中繼資料。 這可能包括建立模型的時間、上次處理模型的時間、模型所依據之採礦結構的名稱，以及指定為可預測屬性之資料行的名稱。 您也可以傳回初次建立此模型時所使用的參數。  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_PredictIncome'  
```  
  
 範例結果：  
  
|MINING_PARAMETERS|  
|------------------------|  
|COMPLEXITY_PENALTY=0.9,<br /><br /> MAXIMUM_INPUT_ATTRIBUTES=255,<br /><br /> MAXIMUM_OUTPUT_ATTRIBUTES=255,<br /><br /> MINIMUM_SUPPORT=10,<br /><br /> SCORE_METHOD=4,<br /><br /> SPLIT_METHOD=3,<br /><br /> FORCE_REGRESSOR=|  
  
> [!NOTE]  
>  參數設定「`FORCE_REGRESSOR =` 」表示目前用於 FORCE_REGRESSOR 參數的值為 Null 值。  
  
 [回頁首](#bkmk_top)  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：擷取模型的迴歸公式  
 下列查詢會針對利用＜ [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)＞中所使用之相同目標郵寄資料來源所建立的線性迴歸模型，傳回採礦模型內容。 此模型會根據年齡預測客戶收入。  
  
 查詢會傳回包含迴歸公式之節點的內容。 每個變數和係數都儲存在 NODE_DISTRIBUTION 資料表的個別資料列中。 如果您要檢視完整的迴歸公式，使用 [Microsoft 樹狀檢視器](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-tree-viewer.md)，按一下 **(All)** 節點，然後開啟 **[採礦圖例]**。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION as t  
FROM LR_PredictIncome.CONTENT  
```  
  
> [!NOTE]  
>  如果您使用 `SELECT <column name> from NODE_DISTRIBUTION`之類的查詢參考巢狀資料表的個別資料行，某些資料行 (例如， **SUPPORT** 或 **PROBABILITY**) 必須括在刮號內，以便與同名的保留關鍵字區別。  
  
 預期的結果：  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|@shouldalert|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
|Age|471.687717702463|0|0|126.969442359327|7|  
|Age|234.680904692439|0|0|0|8|  
|Age|45.4269617936399|0|0|126.969442359327|9|  
||35793.5477381267|0|0|1012968919.28372|11|  
  
 相較之下，在 **[採礦圖例]**中，迴歸公式顯示如下：  
  
 `Yearly Income = 57,220.919 + 471.688 * (Age - 45.427)`  
  
 您可以發現，在 **[採礦圖例]**中，有些數字會被捨入，不過，NODE_DISTRIBUTION 資料表和 **[採礦圖例]** 基本上包含相同的值。  
  
 VALUETYPE 資料行中的值會告訴您每個資料列中包含哪種資訊；如果您要以程式設計方式處理結果，哪個比較實用。 下表顯示針對線性迴歸公式輸出的值類型。  
  
|VALUETYPE|  
|---------------|  
|1 (遺漏)|  
|3 (連續)|  
|7 (係數)|  
|8 (得分)|  
|9 (統計資料)|  
|7 (係數)|  
|8 (得分)|  
|9 (統計資料)|  
|11 (截距)|  
  
 如需迴歸模型每個值類型之意義的詳細資訊，請參閱 [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
 [回頁首](#bkmk_top)  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：僅傳回模型的係數  
 您可以使用 VALUETYPE 列舉，僅傳回迴歸方程式的係數，如以下查詢所示：  
  
```  
SELECT FLATTENED MODEL_NAME,  
    (SELECT ATTRIBUTE_VALUE, VALUETYPE  
     FROM NODE_DISTRIBUTION  
     WHERE VALUETYPE = 11)   
AS t  
FROM LR_PredictIncome.CONTENT  
```  
  
 此查詢會傳回兩個資料列，其中一個資料列來自採礦模型內容，而另一個資料列則來自包含係數的巢狀資料表。 ATTRIBUTE_NAME 資料行不包含在此處，因為該資料行對係數來說，永遠是空白的。  
  
|MODEL_NAME|t.ATTRIBUTE_VALUE|t.VALUETYPE|  
|-----------------|------------------------|-----------------|  
|LR_PredictIncome|||  
|LR_PredictIncome|35793.5477381267|11|  
  
 [回頁首](#bkmk_top)  
  
## <a name="making-predictions-from-a-linear-regression-model"></a>從線性迴歸模型進行預測  
 您可以使用資料採礦設計師中的 [採礦模型預測] 索引標籤，在線性迴歸模型上建立預測查詢。 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中都提供預測查詢產生器。  
  
> [!NOTE]  
>  您也可以使用適用於 Excel 的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料採礦增益集或適用於 Excel 的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 資料採礦增益集，在迴歸模型上建立查詢。 即使適用於 Excel 的資料採礦增益集沒有建立迴歸模型，您也可以瀏覽並查詢儲存在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]執行個體上的任何採礦模型。  
  
 [回頁首](#bkmk_top)  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4：使用單一查詢預測收入  
 在迴歸模型上建立單一查詢最簡單的方式是使用 **[單一查詢輸入]** 對話方塊。 例如，您可以適當的迴歸模型、選擇 **[單一查詢]**，然後輸入 **20** 做為 **Age**的值來建立下列 DMX 查詢。  
  
```  
SELECT [LR_PredictIncome].[Yearly Income]  
From   [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 範例結果：  
  
|Yearly Income|  
|-------------------|  
|45227.302092176|  
  
 [回頁首](#bkmk_top)  
  
###  <a name="bkmk_Query5"></a> 範例查詢 5：搭配迴歸模型使用預測函數  
 您可以搭配線性迴歸模型使用多個標準的預測函數。 下列範例說明如何將一些敘述性的統計資料加入到預測查詢結果中。 從這些結果中您可以發現，這與此模型的平均值有相當大的偏差。  
  
```  
SELECT  
  ([LR_PredictIncome].[Yearly Income]) as [PredIncome],  
  (PredictStdev([LR_PredictIncome].[Yearly Income])) as [StDev1]  
From  
  [LR_PredictIncome]  
NATURAL PREDICTION JOIN  
(SELECT 20 AS [Age]) AS t  
```  
  
 範例結果：  
  
|Yearly Income|StDev1|  
|-------------------|------------|  
|45227.302092176|31827.1726561396|  
  
 [回頁首](#bkmk_top)  
  
## <a name="list-of-prediction-functions"></a>預測函數的清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 線性迴歸演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|確定某個節點是否為模型中另一個節點的子系。|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|指示指定的節點是否包含目前案例。|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|傳回指定之資料行的一個或一組預測值。|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|傳回每個案例的 Node_ID。|  
|[PredictStdev &#40;DMX&#41;](../../dmx/predictstdev-dmx.md)|傳回預測值的標準差。|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|傳回指定狀態的支援值。|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|傳回指定之資料行的變異數。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法共用之函數的清單，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。 如需如何使用這些函數的詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](../../dmx/data-mining-extensions-dmx-function-reference.md)。  
  
## <a name="see-also"></a>請參閱  
 [Microsoft 線性迴歸演算法](../../analysis-services/data-mining/microsoft-linear-regression-algorithm.md)   
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)   
 [Microsoft 線性迴歸演算法技術參考](../../analysis-services/data-mining/microsoft-linear-regression-algorithm-technical-reference.md)   
 [線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)  
  
  
