---
title: "關聯模型查詢範例 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- itemsets [Analysis Services]
- association algorithms [Analysis Services]
- rules [Data Mining]
- association rules
- content queries [DMX]
ms.assetid: 68b39f5c-c439-44ac-8046-6f2d36649059
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b176b73816fb01ff7659e00f58dd4441bc689866
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="association-model-query-examples"></a>關聯模型查詢範例
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]當您建立針對資料採礦模型的查詢時，您可以建立內容查詢，來提供有關分析期間發現的項目集和規則的詳細資料，或您可以建立預測查詢來使用資料中發現的關聯進行預測。 對關聯模型而言，預測通常會以規則為基礎，而且可以用來進行推薦，而對內容所做的查詢則通常會探索項目集之間的關聯性。 您也可以擷取有關模型的中繼資料。  
  
 本節說明如何針對以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯規則演算法為基礎的模型來建立此類查詢。  
  
 **Content Queries**  
  
 [使用 DMX 取得模型中繼資料](#bkmk_Query1)  
  
 [從結構描述資料列集取得中繼資料](#bkmk_Query2)  
  
 [擷取模型的原始參數](#bkmk_Query3)  
  
 [擷取項目集和產品的清單](#bkmk_Query4)  
  
 [傳回前 10 個項目集](#bkmk_Query5)  
  
 **預測查詢**  
  
 [預測關聯的項目](#bkmk_Query6)  
  
 [判斷相關項目集的信心](#bkmk_Query7)  
  
##  <a name="bkmk_top2"></a> 尋找有關模型的資訊  
 所有的採礦模型都會公開演算法根據標準化結構描述所學習的內容，也稱為採礦模型結構描述資料列集。 您可以使用資料採礦延伸模組 (DMX) 陳述式或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 預存程序，針對採礦模型結構描述資料列集建立查詢。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，您也可以使用類似 SQL 的語法，將結構描述資料列集當做系統資料表直接進行查詢。  
  
###  <a name="bkmk_Query1"></a> 範例查詢 1：使用 DMX 取得模型中繼資料  
 下列查詢會傳回有關關聯模型 `Association`的基本中繼資料，例如模型的名稱、模型儲存位置所在的資料庫，以及模型中子節點的數目。 此查詢會使用 DMX 內容查詢從模型的父節點擷取中繼資料：  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, NODE_CAPTION,   
NODE_SUPPORT, [CHILDREN_CARDINALITY], NODE_DESCRIPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 1  
```  
  
> [!NOTE]  
>  您必須將資料行 CHILDREN_CARDINALITY 的名稱包含在括號中，好與相同名稱的 MDX 保留關鍵字加以區別。  
  
 範例結果：  
  
|||  
|-|-|  
|MODEL_CATALOG|關聯測試|  
|MODEL_NAME|關聯|  
|NODE_CAPTION|關聯規則模型|  
|NODE_SUPPORT|14879|  
|CHILDREN_CARDINALITY|942|  
|NODE_DESCRIPTION|Association Rules Model; ITEMSET_COUNT=679; RULE_COUNT=263; MIN_SUPPORT=14; MAX_SUPPORT=4334; MIN_ITEMSET_SIZE=0; MAX_ITEMSET_SIZE=3; MIN_PROBABILITY=0.400390625; MAX_PROBABILITY=1; MIN_LIFT=0.14309369632511; MAX_LIFT=1.95758227647523|  
  
 如需這些資料行在關聯模型中的定義，請參閱 [關聯模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
 [回頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query2"></a> 範例查詢 2：從結構描述資料列集取得其他的中繼資料  
 藉由查詢資料採礦結構描述資料列集，您可以找到與 DMX 內容查詢所傳回的相同的資訊。 不過，結構描述資料列集會提供一些其他的資料行，例如上次處理模型的日期、採礦結構，以及用來當做可預測屬性的資料行的名稱。  
  
```  
SELECT MODEL_CATALOG, MODEL_NAME, SERVICE_NAME, PREDICTION_ENTITY,   
MINING_STRUCTURE, LAST_PROCESSED  
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 範例結果：  
  
|||  
|-|-|  
|MODEL_CATALOG|Adventure Works DW Multidimensional 2012|  
|MODEL_NAME|關聯|  
|SERVICE_NAME|關聯規則模型|  
|PREDICTION_ENTITY|v Assoc Seq Line Items|  
|MINING_STRUCTURE|關聯|  
|LAST_PROCESSED|9/29/2007 10:21:24 下午|  
  
 [回頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query3"></a> 範例查詢 3：擷取模型的原始參數  
 下列查詢會傳回單一資料行，其中包含有關在建立模型時所使用參數設定的詳細資料。  
  
```  
SELECT MINING_PARAMETERS   
from $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'Association'  
```  
  
 範例結果：  
  
 MAXIMUM_ITEMSET_COUNT=200000,MAXIMUM_ITEMSET_SIZE=3,MAXIMUM_SUPPORT=1,MINIMUM_SUPPORT=9.40923449156529E-04,MINIMUM_IMPORTANCE=-999999999,MINIMUM_ITEMSET_SIZE=0,MINIMUM_PROBABILITY=0.4  
  
 [回頁首](#bkmk_top2)  
  
## <a name="finding-information-about-rules-and-itemsets"></a>尋找有關規則和項目集的資訊  
 關聯模型有兩種常見用法：探索有關常用項目集的詳細資訊，以及擷取有關特定規則和項目集的詳細資料。 例如，您可能想要擷取計分為特別有趣的規則清單，或建立最常見項目集的清單。 您可以使用 DMX 內容查詢擷取此類資訊。 也可以使用 [Microsoft 關聯檢視器] 瀏覽此資訊。  
  
###  <a name="bkmk_Query4"></a> 範例查詢 4：擷取項目集和產品的清單  
 下列查詢會擷取所有的項目集，並附上列出每個項目集中所包含產品的巢狀資料表。 NODE_NAME 資料行包含項目集在模型內的唯一識別碼，NODE_CAPTION 則提供項目的文字描述。 在此範例中，巢狀資料表會扁平化，使包含兩個產品的項目集會在結果中產品兩個資料列。 如果用戶端支援階層資料，則您可以省略 FLATTENED 關鍵字。  
  
```  
SELECT FLATTENED NODE_NAME, NODE_CAPTION,  
NODE_PROBABILITY, NODE_SUPPORT,  
(SELECT ATTRIBUTE_NAME FROM NODE_DISTRIBUTION) as PurchasedProducts  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 範例結果：  
  
|||  
|-|-|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
|NODE_PROBABILITY|0.291283016331743|  
|NODE_SUPPORT|4334|  
|PURCHASEDPRODUCTS.ATTRIBUTE_NAME|v Assoc Seq Line Items(Sport-100)|  
  
 [回頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query5"></a> 範例查詢 5：傳回前 10 個項目集  
 此範例示範如何使用 DMX 依預設所提供的一些群組和排序函數。 在藉由每個節點的支援進行排序時，查詢會傳回前 10 個項目集。 請注意，您不需要像在 Transact-SQL 中一樣明確地將結果分組，不過可以在每個查詢中只使用一個彙總函式。  
  
```  
SELECT TOP 10 (NODE_SUPPORT),NODE_NAME, NODE_CAPTION  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
```  
  
 範例結果：  
  
|||  
|-|-|  
|NODE_SUPPORT|4334|  
|NODE_NAME|37|  
|NODE_CAPTION|Sport-100 = Existing|  
  
 [回頁首](#bkmk_top2)  
  
## <a name="making-predictions-using-the-model"></a>使用模型進行預測  
 關聯規則模型常用來根據項目集中發現的關聯而產生建議。 因此，當您根據關聯規則模型建立預測查詢時，通常是使用模型中的規則來根據新資料進行猜測。  [PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md) 是可傳回建議的函數，提供數個引數，可用來自訂查詢結果。  
  
 另一個說明關聯模型上的查詢可能有用的範例，是傳回不同規則及項目集的信心，讓您可以比較不同交叉銷售策略的效能。 下列範例說明如何建立此類查詢。  
  
###  <a name="bkmk_Query6"></a> 範例查詢 6：預測相關聯項目  
 這個範例會使用[中繼資料採礦教學課程 &#40;Analysis Services - 資料採礦 &#41;](http://msdn.microsoft.com/library/404b31d5-27f4-4875-bd60-7b2b8613eb1b) 中建立的關聯模型。 該模型示範如何建立預測查詢，以告訴您要向已購買特定產品的客戶建議什麼產品。 此類型的查詢 (在 **SELECT…UNION** 陳述式中向模型提供值) 稱為單一查詢。 因為與新值相對應的可預測模型資料行是巢狀資料表，所以您必須使用一個 **SELECT** 子句將新值對應到巢狀資料表資料行 `[Model]`，並用另一個 **SELECT** 子句將巢狀資料表資料行對應到案例層級資料行 `[v Assoc Seq Line Items]`。 將關鍵 INCLUDE-STATISTICS 加入至查詢可讓您看到建議的機率和支援。  
  
```  
SELECT PredictAssociation([Association].[vAssocSeqLineItems],INCLUDE_STATISTICS, 3)  
FROM [Association]  
NATURAL PREDICTION JOIN   
(SELECT  
(SELECT 'Classic Vest' as [Model])  
AS [v Assoc Seq Line Items])  
AS t  
```  
  
 範例結果：  
  
|模型|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291283|0.252696|  
|Water Bottle|2866|0.19262|0.175205|  
|Patch kit|2113|0.142012|0.132389|  
  
 [回頁首](#bkmk_top2)  
  
###  <a name="bkmk_Query7"></a> 範例查詢 7：判斷相關項目集的信心  
 雖然規則對產生建議很有用，但如果要較深入地分析資料集中的模式，則項目集比較有趣。 例如，如果您對於前述範例查詢所傳回的建議不滿意，則可以檢查其他包含產品 A 的項目集，以進一步了解產品 A 是否為客戶會搭配所有產品類型而購買的配件，或者 A 與特定產品的購買有強烈的關聯性。 探索這些關聯性最簡單的方式，就是在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯檢視器中篩選項目集；不過您可以藉由查詢來擷取相同的資訊。  
  
 下列範例查詢會傳回所有包含 Water Bottle 項目的項目集 (包含單一項目 Water Bottle)。  
  
```  
SELECT TOP 100 FROM   
(  
SELECT FLATTENED NODE_CAPTION, NODE_SUPPORT,   
(SELECT ATTRIBUTE_NAME from NODE_DISTRIBUTION  
WHERE ATTRIBUTE_NAME = 'v Assoc Seq Line Items(Water Bottle)') as D  
FROM Association.CONTENT  
WHERE NODE_TYPE = 7  
) AS Items  
WHERE [D.ATTRIBUTE_NAME] <> NULL  
ORDER BY NODE_SUPPORT DESC  
```  
  
 範例結果：  
  
|NODE_CAPTION|NODE_SUPPORT|D.ATTRIBUTE_NAME|  
|-------------------|-------------------|-----------------------|  
|Water Bottle = Existing|2866|v Assoc Seq Line Items(Water Bottle)|  
|Mountain Bottle Cage = Existing, Water Bottle = Existing|1136|v Assoc Seq Line Items(Water Bottle)|  
|Road Bottle Cage = Existing, Water Bottle = Existing|1068|v Assoc Seq Line Items(Water Bottle)|  
|Water Bottle = Existing, Sport-100 = Existing|734|v Assoc Seq Line Items(Water Bottle)|  
  
 這個查詢不但僅會從巢狀資料表傳回符合準則的資料列，還會從外部或案例資料表傳回所有的資料列。 因此，您必須加入條件來排除目標屬性名稱具有 Null 值的案例資料表資料列。  
  
 [回頁首](#bkmk_top2)  
  
## <a name="function-list"></a>函數清單  
 所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 演算法都支援一組常用的函數。 不過， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 關聯分析演算法支援下表所列出的其他函數。  
  
|||  
|-|-|  
|預測函數|使用方式|  
|[IsDescendant &#40;DMX&#41;](../../dmx/isdescendant-dmx.md)|確定某個節點是否為類神經網路圖中另一個節點的子系。|  
|[IsInNode &#40;DMX&#41;](../../dmx/isinnode-dmx.md)|指示指定的節點是否包含目前案例。|  
|[PredictAdjustedProbability &#40;DMX&#41;](../../dmx/predictadjustedprobability-dmx.md)|傳回加權機率。|  
|[PredictAssociation &#40;DMX&#41;](../../dmx/predictassociation-dmx.md)|預測關聯資料集的成員資格。|  
|[PredictHistogram &#40;DMX&#41;](../../dmx/predicthistogram-dmx.md)|傳回與目前預測值相關之值的資料表。|  
|[PredictNodeId &#40;DMX&#41;](../../dmx/predictnodeid-dmx.md)|傳回每個案例的 Node_ID。|  
|[PredictProbability &#40;DMX&#41;](../../dmx/predictprobability-dmx.md)|傳回預測值的機率。|  
|[PredictSupport &#40;DMX&#41;](../../dmx/predictsupport-dmx.md)|傳回指定狀態的支援值。|  
|[PredictVariance &#40;DMX&#41;](../../dmx/predictvariance-dmx.md)|傳回預測值的變異數。|  
  
## <a name="see-also"></a>請參閱  
 [Microsoft 關聯分析演算法](../../analysis-services/data-mining/microsoft-association-algorithm.md)   
 [Microsoft 關聯分析演算法技術參考](../../analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md)   
 [關聯模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)  
  
  
