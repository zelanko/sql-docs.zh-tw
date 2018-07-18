---
title: 貝氏機率分類模型查詢範例 |Microsoft Docs
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
- naive bayes model [Analysis Services]
- naive bayes algorithms [Analysis Services]
- content queries [DMX]
ms.assetid: e642bd7d-5afa-4dfb-8cca-4f84aadf61b0
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a2fb2a44ff12ef938abc09f7e307841a1b057be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224688"
---
# <a name="naive-bayes-model-query-examples"></a>貝式機率分類模型查詢範例
  當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，或是建立預測查詢來使用模型中的模式，為新的資料進行預測。 您也可以針對資料採礦結構描述資料列集使用查詢，藉以擷取有關模型的中繼資料。 本節說明如何針對以 Microsoft 貝氏機率分類演算法為基礎的模型來建立這些查詢。  
  
 **內容查詢**  
  
 [使用 DMX 取得模型中繼資料](#bkmk_Query1)  
  
 [擷取定型資料的摘要](#bkmk_Query2)  
  
 [尋找有關屬性的詳細資訊](#bkmk_Query3)  
  
 [使用系統預存程序](#bkmk_Query4)  
  
 **預測查詢**  
  
 [使用單一查詢預測結果](#bkmk_Query5)  
  
 [取得含有機率和支援值的預測](#bkmk_Query6)  
  
 [預測關聯](#bkmk_Query7)  
  
## <a name="finding-information-about-a-naive-bayes-model"></a>尋找有關貝式機率分類模型的資訊  
 貝氏機率分類模型的模型內容會提供定型資料中，有關值分佈的彙總資訊。 您也可以針對資料採礦結構描述資料列集建立查詢，藉以擷取有關模型之中繼資料的資訊。  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：使用 DMX 取得模型中繼資料  
 您可以查詢資料採礦結構描述資料列集來尋找模型的中繼資料。 這可能包括建立模型的時間、上次處理模型的時間、模型所依據之採礦結構的名稱，以及用來當做可預測屬性之資料行的名稱。 您也可以傳回建立此模型時所使用的參數。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, DATE_CREATED, LAST_PROCESSED,  
SERVICE_NAME, PREDICTION_ENTITY, FILTER  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_NaiveBayes_Filtered'  
```  
  
 範例結果：  
  
|||  
|-|-|  
|MODEL_CATALOG|AdventureWorks|  
|MODEL_NAME|TM_NaiveBayes_Filtered|  
|DATE_CREATED|3/1/2008 19:15|  
|LAST_PROCESSED|3/2/2008 20:00|  
|SERVICE_NAME|Microsoft_Naive_Bayes|  
|PREDICTION_ENTITY|Bike Buyer,Yearly Income|  
|FILTER|[Region] = 'Europe' OR [Region] = 'North America'|  
  
 用於此範例的模型是以您在 [Basic Data Mining Tutorial](../../tutorials/basic-data-mining-tutorial.md)中建立的貝氏機率分類模型為基礎，但是透過加入另一個可預測屬性，並將篩選套用到定型資料來修改。  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：擷取定型資料的摘要  
 在貝氏機率分類模型中，臨界統計資料節點會儲存定型資料中，有關值分佈的彙總資訊。 此摘要相當方便，而且您不必根據定型資料建立 SQL 查詢，就可以找到相同的資訊。  
  
 下列範例使用 DMX 內容查詢從節點 (NODE_TYPE = 24) 擷取資料。 由於統計資料儲存在巢狀資料表中，因此，FLATTENED 關鍵字的用途是讓結果更容易檢視。  
  
```  
SELECT FLATTENED MODEL_NAME,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE FROM NODE_DISTRIBUTION) AS t  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
> [!NOTE]  
>  您必須將 SUPPORT 和 PROBABILITY 資料行的名稱括在括號中，以便與相同名稱的「多維度運算式」(MDX) 保留關鍵字區別。  
  
 部分結果：  
  
|MODEL_NAME|t.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-----------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|8869|0.507263784|4|  
|TM_NaiveBayes|Bike Buyer|1|8615|0.492736216|4|  
|TM_NaiveBayes|Gender|Missing|0|0|1|  
|TM_NaiveBayes|Gender|F|8656|0.495081217|4|  
|TM_NaiveBayes|Gender|M|8828|0.504918783|4|  
  
 例如，這些結果告訴您每個離散值 (VALUETYPE = 4) 的定型案例數目，以及針對遺漏值 (VALUETYPE = 1) 調整的計算機率。  
  
 如需貝氏機率分類模型之 NODE_DISTRIBUTION 資料表中所提供值的定義，請參閱[貝式機率分類模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)。 如需支援與機率計算如何受到遺漏值影響的詳細資訊，請參閱[遺漏值 &#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：尋找有關屬性的詳細資訊  
 貝氏機率分類模型通常包含不同屬性之間關聯性的複雜資訊，檢視這些關聯性最簡單的方式就是使用 [Microsoft 貝氏機率分類檢視器](browse-a-model-using-the-microsoft-naive-bayes-viewer.md)。 不過，您可以建立 DMX 查詢來傳回資料。  
  
 下列範例顯示如何從模型傳回有關特定屬性 `Region`的資訊。  
  
```  
SELECT NODE_TYPE, NODE_CAPTION,   
NODE_PROBABILITY, NODE_SUPPORT, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE ATTRIBUTE_NAME = 'Region'  
```  
  
 此查詢會傳回兩種類型的節點：代表輸入屬性 (NODE_TYPE = 10) 的節點，以及屬性 (NODE_TYPE = 11) 每個值的節點。 節點標題 (而非節點名稱) 用於識別節點，因為標題會同時顯示屬性名稱和屬性值。  
  
|NODE_TYPE|NODE_CAPTION|NODE_PROBABILITY|NODE_SUPPORT|MSOLAP_NODE_SCORE|NODE_TYPE|  
|----------------|-------------------|-----------------------|-------------------|-------------------------|----------------|  
|10|Bike Buyer -> Region|1|17484|84.51555875|10|  
|11|Bike Buyer -> Region = Missing|0|0|0|11|  
|11|Bike Buyer -> Region = North America|0.508236102|8886|0|11|  
|11|Bike Buyer -> Region = Pacific|0.193891558|3390|0|11|  
|11|Bike Buyer -> Region = Europe|0.29787234|5208|0|11|  
  
 儲存在節點中的某些資料行與您可以從臨界統計資料節點中取得的資料行相同，例如，節點機率分數與節點支援值。 不過，MSOLAP_NODE_SCORE 是僅針對輸入屬性節點提供的特別值，表示此屬性在模型中的相對重要性。 您可以在檢視器的 [相依性網路] 窗格中看到很多相同的資訊，但是，此檢視器不提供分數。  
  
 下列查詢會傳回所有屬性在模型中的重要性分數：  
  
```  
SELECT NODE_CAPTION, MSOLAP_NODE_SCORE  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
ORDER BY MSOLAP_NODE_SCORE DESC  
```  
  
 範例結果：  
  
|NODE_CAPTION|MSOLAP_NODE_SCORE|  
|-------------------|-------------------------|  
|Bike Buyer -> Total Children|181.3654836|  
|Bike Buyer -> Commute Distance|179.8419482|  
|Bike Buyer -> English Education|156.9841928|  
|Bike Buyer -> Number Children At Home|111.8122599|  
|Bike Buyer -> Region|84.51555875|  
|Bike Buyer -> Marital Status|23.13297354|  
|Bike Buyer -> English Occupation|2.832069191|  
  
 透過在 [Microsoft 一般內容樹狀檢視器](browse-a-model-using-the-microsoft-generic-content-tree-viewer.md)中瀏覽模型內容，您將會更為了解哪些統計資料可能是有趣的。 此處會示範一些簡單的案例；您可能需要更常執行多個查詢，或在用戶端上儲存結果並進行處理。  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4：使用系統預存程序  
 除了撰寫您自己的內容查詢之外，您也可以使用某些 Analysis Services 系統預存程序瀏覽結果。 若要使用系統預存程序，在預存程序名稱開頭加上 CALL 關鍵字：  
  
```  
CALL GetPredictableAttributes ('TM_NaiveBayes')  
```  
  
 部分結果：  
  
|ATTRIBUTE_NAME|NODE_UNIQUE_NAME|  
|---------------------|------------------------|  
|Bike Buyer|100000001|  
  
> [!NOTE]  
>  這些系統預存程序供 Analysis Services 伺服器與用戶端之間的內部通訊使用，而只是為了方便而在開發和測試採礦模型時使用。 當您為實際系統建立查詢時，應該一律使用 DMX 撰寫您自己的查詢。  
  
 如需 Analysis Services 系統預存程序的詳細資訊，請參閱[資料採礦預存程序 &#40;Analysis Services - 資料採礦&#41;](/sql/analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining)。  
  
## <a name="using-a-naive-bayes-model-to-make-predictions"></a>使用貝式機率分類模型進行預測  
 Microsoft 貝氏機率分類演算法用於預測的頻率通常比用於瀏覽輸入屬性和可預測屬性之間關聯性的頻率低。 不過，此模型支援同時針對預測和關聯使用預測函數。  
  
###  <a name="bkmk_Query5"></a> 範例查詢 5：使用單一查詢預測結果  
 下列查詢使用單一查詢提供新的值，並根據模型預測具備這些特徵的客戶是否可能購買自行車。 在迴歸模型上建立單一查詢最簡單的方式是使用 **[單一查詢輸入]** 對話方塊。 例如，您可以選取 `TM_NaiveBayes` 模型、選擇 **[單一查詢]**，然後從 `[Commute Distance]` 和 `Gender`的下拉式清單選取值來建立下列 DMX 查詢。  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 範例結果：  
  
|運算式|  
|----------------|  
|0|  
  
 預測函數會傳回最可能的值，在此範例中為 0，也就是說，此類型的客戶不太可能購買自行車。  
  
###  <a name="bkmk_Query6"></a> 範例查詢 6：取得含有機率和支援值的預測  
 除了預測結果之外，您通常還想要知道預測的可能性。 下列查詢使用與先前範例相同的單一查詢，但是加入預測函數 ([PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)) 來傳回包含支援預測之統計資料的巢狀資料表。  
  
```  
SELECT  
  Predict([TM_NaiveBayes].[Bike Buyer]),  
  PredictHistogram([TM_NaiveBayes].[Bike Buyer])  
FROM  
  [TM_NaiveBayes]  
NATURAL PREDICTION JOIN  
(SELECT '5-10 Miles' AS [Commute Distance],  
  'F' AS [Gender]) AS t  
```  
  
 範例結果：  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|0|10161.5714|0.581192599|0.010530981|0|0|  
|1|7321.428768|0.418750215|0.008945684|0|0|  
||0.999828444|5.72E-05|5.72E-05|0|0|  
  
 資料表中的最後一個資料列會顯示支援與機率針對遺漏值所做的調整。 變異數和標準差永遠為 0，因為貝氏機率分類模型無法製作連續值的模型。  
  
###  <a name="bkmk_Query7"></a> 範例查詢 7：預測關聯  
 如果採礦結構包含巢狀資料表與當做索引鍵的可預測屬性，Microsoft 貝氏機率分類演算法可以用於關聯分析。 例如，您可以使用在資料採礦教學課程之[第 3 課：建立購物籃狀況 &#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md) 中所建立的採礦結構來建立貝氏機率分類模型。 此範例中所使用的模型會遭到修改，以便在案例資料表中加入有關收入和客戶地區的資訊。  
  
 下列查詢範例顯示的單一查詢會預測與購買產品 `'Road Tire Tube'`相關的產品。 您可以使用這項資訊提供產品建議給特定類型的客戶。  
  
```  
SELECT   PredictAssociation([Association].[v Assoc Seq Line Items])  
FROM [Association_NB]  
NATURAL PREDICTION JOIN  
(SELECT 'High' AS [Income Group],  
  'Europe' AS [Region],  
  (SELECT 'Road Tire Tube' AS [Model])   
AS [v Assoc Seq Line Items])   
AS t  
```  
  
 部分結果：  
  
|[模型]|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
|Touring-2000|  
|Touring-1000|  
  
## <a name="function-list"></a>函數清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝氏機率分類演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|確定某個節點是否為模型中另一個節點的子系。|  
|[預測&#40;DMX&#41;](/sql/dmx/predict-dmx)|傳回指定之資料行的一個或一組預測值。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|傳回加權機率。|  
|[[Predictassociation] &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|預測關聯資料集的成員資格。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|傳回每個案例的 Node_ID。|  
|[[Predictprobability] &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|傳回預測值的機率。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|傳回指定狀態的支援值。|  
  
 若要查看特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>另請參閱  
 [Microsoft 貝氏機率分類演算法技術參考](microsoft-naive-bayes-algorithm-technical-reference.md)   
 [Microsoft 貝氏機率分類演算法](microsoft-naive-bayes-algorithm.md)   
 [貝氏機率分類模型的採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-for-naive-bayes-models-analysis-services-data-mining.md)  
  
  
