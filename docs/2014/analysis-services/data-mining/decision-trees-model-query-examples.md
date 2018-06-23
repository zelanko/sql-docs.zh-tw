---
title: 決策樹模型查詢範例 |Microsoft 文件
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
- decision tree algorithms [Analysis Services]
- content queries [DMX]
- decision trees [Analysis Services]
ms.assetid: ceaf1370-9dd1-4d1a-a143-7f89a723ef80
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 56763f6e1b207e0f676c08e5bbca7066b680dcda
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134744"
---
# <a name="decision-trees-model-query-examples"></a>決策樹模型查詢範例
  當您針對資料採礦模型建立查詢時，可以建立內容查詢來提供有關分析期間所發現之模式的詳細資料，或是建立預測查詢來使用模型中的模式，為新的資料進行預測。 例如，決策樹模型的內容查詢可能會提供有關每一樹狀結構層上之案例數的統計資料，或是區分案例的規則。 或者，預測查詢會將此模型對應到新的資料，以便產生建議、分類等等。 您也可以使用查詢來擷取有關模型的中繼資料。  
  
 本節說明如何針對以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法為基礎的模型來建立查詢。  
  
 **內容查詢**  
  
 [從資料採礦結構描述資料列集擷取模型參數](#bkmk_Query1)  
  
 [使用 DMX 取得有關模型中樹狀結構的詳細資料](#bkmk_Query2)  
  
 [從模型擷取子樹](#bkmk_Query3)  
  
 **預測查詢**  
  
 [傳回包含機率的預測](#bkmk_Query4)  
  
 [從決策樹模型預測關聯](#bkmk_Query5)  
  
 [從決策樹模型擷取迴歸公式](#bkmk_Query6)  
  
##  <a name="bkmk_top2"></a> 尋找有關決策樹模型的資訊  
 若要在決策樹模型的內容上建立有意義的查詢，您應該了解模型內容的結構，以及哪一種節點類型會儲存那一種資訊。 如需詳細資訊，請參閱[決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：從資料採礦結構描述資料列集擷取模型參數  
 您可以藉由查詢資料採礦結構描述資料列集來尋找有關此模型的中繼資料，例如此模型建立的時間、上次處理此模型的時間、此模型所根據的採礦結構名稱，以及用來當做可預測屬性的資料行名稱。 您也可以傳回初次建立此模型時所使用的參數。  
  
```  
select MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM_Decision Tree'  
```  
  
 範例結果：  
  
 MINING_PARAMETERS  
  
 COMPLEXITY_PENALTY=0.5, MAXIMUM_INPUT_ATTRIBUTES=255,MAXIMUM_OUTPUT_ATTRIBUTES=255,MINIMUM_SUPPORT=10,SCORE_METHOD=4,SPLIT_METHOD=3,FORCE_REGRESSOR=  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：使用 DMX 傳回有關模型內容的詳細資料  
 下列查詢會傳回您在 [資料採礦基本教學課程](../../tutorials/basic-data-mining-tutorial.md)中建立模型時所建立之決策樹模型的一些基本資訊。 每個樹狀結構都會儲存在它自己的節點中。 由於此模型只包含單一可預測屬性，因此只有一個樹狀節點。 但是，如果您使用決策樹演算法來建立關聯模型，可能會有好幾百個樹狀結構，每一個產品都有一個。  
  
 此查詢會傳回類型 2 的所有節點，這些節點是代表特定可預測屬性之樹狀結構的最上層節點。  
  
> [!NOTE]  
>  資料行， `CHILDREN_CARDINALITY`，必須括在括號內具有相同名稱的 MDX 保留關鍵字區別。  
  
```  
SELECT MODEL_NAME, NODE_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY]  
FROM TM_DecisionTrees.CONTENT  
WHERE NODE_TYPE = 2  
```  
  
 範例結果：  
  
|MODEL_NAME|NODE_NAME|NODE_CAPTION|NODE_SUPPORT|CHILDREN_CARDINALITY|  
|-----------------|----------------|-------------------|-------------------|---------------------------|  
|TM_DecisionTree|000000001|All|12939|5|  
  
 這些結果代表什麼意思？ 在決策樹模型中，特定節點的基數會告訴您該節點擁有多少下層子節點。 這個節點的基數是 5，表示此模型已將潛在自行車買主的目標母體分成 5 個子群組。  
  
 下列相關查詢會傳回這五個子群組的子節點，連同這些子節點中屬性和值的分佈。 例如支援、 機率和變異數的統計資料會儲存在巢狀資料表中，因為`NODE_DISTRIBUTION`，這個範例會使用`FLATTENED`關鍵字來輸出巢狀的資料表資料行。  
  
> [!NOTE]  
>  巢狀的資料表資料行`SUPPORT`，必須括在方括號，以便與同名的保留關鍵字區分。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT]  
FROM NODE_DISTRIBUTION) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE [PARENT_UNIQUE_NAME] = '000000001'  
```  
  
 範例結果：  
  
|NODE_NAME|NODE_CAPTION|T.ATTRIBUTE_NAME|T.ATTRIBUTE_VALUE|SUPPORT|  
|----------------|-------------------|-----------------------|------------------------|-------------|  
|00000000100|Number Cars Owned = 0|Bike Buyer|Missing|0|  
|00000000100|Number Cars Owned = 0|Bike Buyer|0|1067|  
|00000000100|Number Cars Owned = 0|Bike Buyer|@shouldalert|1875|  
|00000000101|Number Cars Owned = 3|Bike Buyer|Missing|0|  
|00000000101|Number Cars Owned = 3|Bike Buyer|0|678|  
|00000000101|Number Cars Owned = 3|Bike Buyer|@shouldalert|473|  
  
 從這些結果中，您所見的客戶購買自行車 (`[Bike Buyer]` = 1)，有 1067 位客戶擁有 0 輛汽車 473 客戶擁有 3 輛汽車。  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：從模型擷取子樹  
 假設您想要進一步探索哪些客戶購買自行車的詳細資料。 您可以在查詢中使用 [IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx) 函數 (如下列範例所示)，檢視任何子樹的其他詳細資料。 此查詢會傳回自行車買主的人數，其方式是從包含 42 歲以上之客戶的樹狀結構中擷取分葉節點 (NODE_TYPE = 4)。 此查詢會將巢狀資料表的資料列限制為 Bike Buyer = 1 的資料列。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,NODE_TYPE,  
(  
SELECT [SUPPORT] FROM NODE_DISTRIBUTION WHERE ATTRIBUTE_NAME = 'Bike Buyer' AND ATTRIBUTE_VALUE = '1'  
) AS t  
FROM TM_DecisionTree.CONTENT  
WHERE ISDESCENDANT('0000000010001')  
AND NODE_TYPE = 4  
```  
  
 範例結果：  
  
|NODE_NAME|NODE_CAPTION|t.SUPPORT|  
|----------------|-------------------|---------------|  
|000000001000100|Yearly Income >= 26000 and < 42000|266|  
|00000000100010100|Total Children = 3|75|  
|0000000010001010100|Number Children At Home = 1|75|  
  
## <a name="making-predictions-using-a-decision-trees-model"></a>使用決策樹模型進行預測  
 由於決策樹可用於各種工作，包括分類、迴歸，甚至是關聯，所以當您在決策樹模型上建立預測查詢時，您有許多可用的選項。 您必須了解此模型的建立目的，才能了解預測的結果。 下列查詢範例說明三種不同的案例：  
  
-   傳回分類模型的預測，連同正確預測的機率，然後根據機率篩選結果。  
  
-   建立單一查詢來預測關聯。  
  
-   當輸入和輸出之間的關係為線性時，針對決策樹的一部分擷取迴歸公式。  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4：傳回包含機率的預測  
 下列範例查詢會使用您在 [資料採礦基本教學課程](../../tutorials/basic-data-mining-tutorial.md)中建立的決策樹模型。 此查詢會從 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW 的 dbo.ProspectiveBuyers 資料表傳入一組新的取樣資料，以便預測新資料集中的哪些客戶將購買自行車。  
  
 此查詢使用預測函數 [PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)，它會傳回一個巢狀資料表，其中包含此模型所探索之機率的有用資訊。 此查詢的最終 WHERE 子句會篩選結果，以便只傳回預測為可能購買自行車之機率大於 0% 的客戶。  
  
```  
SELECT  
  [TM_DecisionTree].[Bike Buyer],  
  PredictHistogram([Bike Buyer]) as Results  
From  
  [TM_DecisionTree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [FirstName],  
      [LastName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM_DecisionTree].[First Name] = t.[FirstName] AND  
  [TM_DecisionTree].[Last Name] = t.[LastName] AND  
  [TM_DecisionTree].[Marital Status] = t.[MaritalStatus] AND  
  [TM_DecisionTree].[Gender] = t.[Gender] AND  
  [TM_DecisionTree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM_DecisionTree].[Total Children] = t.[TotalChildren] AND  
  [TM_DecisionTree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM_DecisionTree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM_DecisionTree].[Number Cars Owned] = t.[NumberCarsOwned]  
WHERE [Bike Buyer] = 1  
AND PredictProbability([Bike Buyer]) >'.05'  
```  
  
 依預設， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回具有資料行標籤 **Expression**的巢狀資料表。 您可以為傳回的資料行設定別名來變更這個標籤。 如果您這樣做，此別名 (此案例中為 **Results**) 會用來當作資料行標題及巢狀資料表中的值。 您必須展開此巢狀資料表，才能看到結果。  
  
 範例結果其中 Bike Buyer = 1:  
  
|Bike Buyer|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|$VARIANCE|$STDEV|  
|----------------|--------------|------------------|--------------------------|---------------|------------|  
|@shouldalert|2540|0.634849242045644|0.013562168281562|0|0|  
|0|1460|0.364984174579377|0.00661336932550915|0|0|  
||0|0.000166583374979177|0.000166583374979177|0|0|  
  
 如果提供者不支援階層式資料列集 (例如這裡顯示的內容)，您可以在查詢中使用 FLATTENED 關鍵字，以資料表的形式傳回結果，此資料表包含了用來取代重複資料行值的 Null。 如需詳細資訊，請參閱[巢狀資料表 &#40;Analysis Services - 資料採礦&#41;](nested-tables-analysis-services-data-mining.md) 或[了解 DMX Select 陳述式](/sql/dmx/understanding-the-dmx-select-statement)。  
  
###  <a name="bkmk_Query5"></a> 範例查詢 5：從決策樹模型預測關聯  
 下列範例查詢是以關聯採礦結構為基礎。 若要依照此範例進行，您可以將新的模型加入至此採礦結構，然後選取 Microsoft 決策樹做為演算法。 如需如何建立關聯採礦模型的詳細資訊，請參閱[第 3 課︰建立購物籃狀況 &#40;中繼資料採礦教學課程&#41;](../../tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)。  
  
 下列範例查詢為單一查詢，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中輕鬆地建立此查詢，其方式是選擇欄位，然後從下拉式清單中選取這些欄位的值。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
FROM  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Patch kit' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 預期的結果：  
  
|[模型]|  
|-----------|  
|Mountain-200|  
|Mountain Tire Tube|  
|Touring Tire Tube|  
  
 結果告訴您建議已經購買 Patch Kit 產品的客戶來購買的三件最佳產品。 當您做出建議時，也可以提供多個產品當作輸入，其方式是輸入值，或是使用 [單一查詢輸入] 對話方塊以及加入或移除值。 下列範例查詢會示範如何提供多個值，根據這些值進行預測。 定義輸入值之 SELECT 陳述式中的 UNION 子句會用來連接值。  
  
```  
SELECT PredictAssociation([DT_Association].[v Assoc Seq Line Items],3)  
From  
  [DT_Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Racing Socks' AS [Model]  
  UNION SELECT 'Women''s Mountain Shorts' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
```  
  
 預期的結果：  
  
|[模型]|  
|-----------|  
|Long-Sleeve Logo Jersey|  
|Mountain-400-W|  
|Classic Vest|  
  
###  <a name="bkmk_Query6"></a> 範例查詢 6：從決策樹模型擷取迴歸公式  
 當您建立的決策樹模型在連續屬性上包含迴歸時，您可以使用迴歸公式來進行預測，或是可以擷取有關此迴歸公式的資訊。 如需迴歸模型上之查詢的詳細資訊，請參閱 [線性迴歸模型查詢範例](linear-regression-model-query-examples.md)。  
  
 如果決策樹模型包含迴歸節點及分散於離散屬性或範圍上之節點的混合，您只能建立傳回迴歸節點的查詢。 NODE_DISTRIBUTION 資料表包含迴歸公式的詳細資料。 在此範例中，資料行會扁平化，而且會設定 NODE_DISTRIBUTION 資料表的別名來方便檢視。 但是在此模型中，未找到任何迴歸輸入變數可以將 Income 與其他連續屬性產生關聯。 在這類情況下， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會傳回此屬性的平均值以及模型中該屬性的總變異數。  
  
```  
SELECT FLATTENED NODE_DISTRIBUTION AS t  
FROM DT_Predict. CONTENT  
WHERE NODE_TYPE = 25  
```  
  
 範例結果：  
  
|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VARIANCE|t.VALUETYPE|  
|-----------------------|------------------------|---------------|-------------------|----------------|-----------------|  
|Yearly Income|Missing|0|0.000457142857142857|0|@shouldalert|  
|Yearly Income|57220.8876687257|17484|0.999542857142857|1041275619.52776|3|  
||57220.8876687257|0|0|1041216662.54387|11|  
  
 如需迴歸模型中所用的值類型和統計資料的詳細資訊，請參閱[線性迴歸模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-for-linear-regression-models-analysis-services-data-mining.md)。  
  
## <a name="list-of-prediction-functions"></a>預測函數的清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 決策樹演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[IsDescendant &#40;DMX&#41;](/sql/dmx/isdescendant-dmx)|確定某個節點是否為模型中另一個節點的子系。|  
|[IsInNode &#40;DMX&#41;](/sql/dmx/isinnode-dmx)|指示指定的節點是否包含目前案例。|  
|[PredictAdjustedProbability &#40;DMX&#41;](/sql/dmx/predictadjustedprobability-dmx)|傳回加權機率。|  
|[PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)|預測關聯資料集的成員資格。|  
|[PredictHistogram &#40;DMX&#41;](/sql/dmx/predicthistogram-dmx)|傳回與目前預測值相關之值的資料表。|  
|[PredictNodeId &#40;DMX&#41;](/sql/dmx/predictnodeid-dmx)|傳回每個案例的 Node_ID。|  
|[PredictProbability &#40;DMX&#41;](/sql/dmx/predictprobability-dmx)|傳回預測值的機率。|  
|[PredictStdev &#40;DMX&#41;](/sql/dmx/predictstdev-dmx)|傳回指定之資料行的預測標準差。|  
|[PredictSupport &#40;DMX&#41;](/sql/dmx/predictsupport-dmx)|傳回指定狀態的支援值。|  
|[PredictVariance &#40;DMX&#41;](/sql/dmx/predictvariance-dmx)|傳回指定之資料行的變異數。|  
  
 如需所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法通用函數的清單，請參閱[一般預測函數 &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx)。 如需特定函數的語法，請參閱[資料採礦延伸模組 &#40;DMX&#41; 函數參考](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft 決策樹演算法](microsoft-decision-trees-algorithm.md)   
 [Microsoft 決策樹演算法技術參考](microsoft-decision-trees-algorithm-technical-reference.md)   
 [決策樹模型的採礦模型內容&#40;Analysis Services-資料採礦&#41;](mining-model-content-for-decision-tree-models-analysis-services-data-mining.md)  
  
  
