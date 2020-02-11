---
title: 貝氏貝氏機率分類模型的採礦模型內容（Analysis Services 資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- naive bayes model [Analysis Services]
- Bayesian classifiers
- naive bayes algorithms [Analysis Services]
- mining model content, naive bayes models
ms.assetid: 63fa15b0-e00c-4aa3-aa49-335f5572ff7e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b899ef4daba73237490d06df58c3447f6b2356d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66083652"
---
# <a name="mining-model-content-for-naive-bayes-models-analysis-services---data-mining"></a>貝氏機率分類模型的採礦模型內容 (Analysis Services - 資料採礦)
  本主題描述使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 貝式機率分類演算法之模型專用的採礦模型內容。 如需如何解譯所有模型類型共用的統計資料與結構的說明，以及與採礦模型內容相關的一般詞彙說明，請參閱 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。  
  
## <a name="understanding-the-structure-of-a-naive-bayes-model"></a>了解貝式機率分類模型的結構  
 貝式機率分類模型擁有代表模型及其中繼資料的單一父節點，而且在該父節點下，則擁有代表所選取之可預測屬性的所有獨立樹狀結構。 除了屬性的樹狀結構，每個模型都包含一個臨界統計資料節點 (NODE_TYPE = 26)，該節點會提供該組定型案例的描述性統計資料。 如需詳細資訊，請參閱 [臨界統計資料節點中的資訊](#bkmk_margstats)。  
  
 對於每個可預測的屬性和值，此模型都會輸出一個樹狀結構，其中包含描述各種輸入資料行如何影響該特定可預測屬性和值之結果的資訊。 每個樹狀結構都包含可預測的屬性及其值 (NODE_TYPE = 9)，接著是一系列代表輸入屬性 (NODE_TYPE = 10) 的節點。 輸入屬性通常擁有多個值，因此每個輸入屬性 (NODE_TYPE = 10) 都可能擁有多個子節點 (NODE_TYPE = 11)，每個子節點都可用於屬性的特定狀態。  
  
> [!NOTE]  
>  由於貝式機率分類模型不允許使用連續資料類型，因此會將輸入資料行的所有值都視為離散或離散化的值。 您可以指定將值離散化的方式。 如需詳細資訊，請參閱 [變更採礦模型中的資料行離散化](change-the-discretization-of-a-column-in-a-mining-model.md)。  
  
 ![貝氏機率分類的模型內容結構](../media/modelcontentstructure-nb.gif "貝氏機率分類的模型內容結構")  
  
## <a name="model-content-for-a-naive-bayes-model"></a>貝式機率分類模型的模型內容  
 本節僅針對採礦模型內容中與貝式機率分類模型具有特定相關的資料行，提供詳細資料和範例。  
  
 如需結構描述資料列集 (例如 MODEL_CATALOG 和 MODEL_NAME) 中一般用途資料行的詳細資訊 (此處沒有說明)，或採礦模型術語的說明，請參閱 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。  
  
 MODEL_CATALOG  
 模型儲存位置所在資料庫的名稱。  
  
 MODEL_NAME  
 模型的名稱。  
  
 ATTRIBUTE_NAME  
 對應至這個節點之屬性的名稱。  
  
 **模型根**可預測屬性的名稱。  
  
 臨界**統計資料**不適用  
  
 **可預測屬性**可預測屬性的名稱。  
  
 **輸入屬性**輸入屬性的名稱。  
  
 **輸入屬性狀態**僅限輸入屬性的名稱。 若要取得狀態，使用 MSOLAP_NODE_SHORT_CAPTION。  
  
 NODE_NAME  
 節點的名稱。  
  
 此資料行包含與 NODE_UNIQUE_NAME 相同的值。  
  
 如需節點命名慣例的詳細資訊，請參閱 [使用節點名稱與識別碼](#bkmk_nodenames)。  
  
 NODE_UNIQUE_NAME  
 節點的唯一名稱。 系統會根據提供節點間關聯性之資訊的慣例指派唯一名稱。 如需節點命名慣例的詳細資訊，請參閱 [使用節點名稱與識別碼](#bkmk_nodenames)。  
  
 NODE_TYPE  
 貝式機率分類模型會輸出下列節點類型：  
  
|節點類型識別碼|描述|  
|------------------|-----------------|  
|26 (NaiveBayesMarginalStatNode)|包含描述模型整組定型案例的統計資料。|  
|9 (可預測的屬性)|包含可預測屬性的名稱。|  
|10 (輸入屬性)|包含輸入屬性資料行的名稱，以及含有屬性值之子節點的名稱。|  
|11 (輸入屬性狀態)|包含與特定輸出屬性配對之所有輸入屬性的值或離散化的值。|  
  
 NODE_CAPTION  
 與節點關聯的標籤或標題。 這個屬性主要是供顯示之用。  
  
 **模型根**空白  
  
 臨界**統計資料**空白  
  
 **可預測屬性**可預測屬性的名稱。  
  
 **輸入屬性**可預測屬性與目前輸入屬性的名稱。 例如：  
  
 Bike Buyer -> Age  
  
 **輸入屬性狀態**可預測屬性與目前輸入屬性的名稱，加上輸入的值。 例如：  
  
 Bike Buyer -> Age = Missing  
  
 CHILDREN_CARDINALITY  
 節點擁有的子系數目。  
  
 **模型根**模型中可預測屬性的計數加1，用於臨界統計資料節點。  
  
 臨界**統計資料**依定義，沒有子系。  
  
 **可預測屬性** 與目前可預測屬性相關之輸入屬性的計數。  
  
 **輸入屬性**目前輸入屬性之離散或離散化值的計數。  
  
 **輸入屬性狀態**一律為0。  
  
 PARENT_UNIQUE_NAME  
 父節點的唯一名稱。 如需父節點與子節點關聯的詳細資訊，請參閱 [使用節點名稱與識別碼](#bkmk_nodenames)。  
  
 NODE_DESCRIPTION  
 與節點標題相同。  
  
 NODE_RULE  
 節點標題的 XML 表示。  
  
 MARGINAL_RULE  
 與節點規則相同。  
  
 NODE_PROBABILITY  
 與此節點關聯的機率。  
  
 **模型根**一律為0。  
  
 臨界**統計資料**一律為0。  
  
 **可預測屬性** 一律為1。  
  
 **輸入屬性**一律為1。  
  
 **輸入屬性狀態**十進位數，表示目前值的機率。 父系輸入屬性節點下，所有輸入屬性狀態的值總和為 1。  
  
 MARGINAL_PROBABILITY  
 與節點機率相同。  
  
 NODE_DISTRIBUTION  
 包含節點之機率長條圖的資料表。 如需詳細資訊，請參閱 [NODE_DISTRIBUTION 資料表](#bkmk_nodedist)。  
  
 NODE_SUPPORT  
 支援這個節點的案例數目。  
  
 **模型根**定型資料中所有案例的計數。  
  
 臨界**統計資料**一律為0。  
  
 **可預測屬性**定型資料中所有案例的計數。  
  
 **輸入屬性**定型資料中所有案例的計數。  
  
 **輸入屬性狀態**定型資料中僅包含此特定值的案例計數。  
  
 MSOLAP_MODEL_COLUMN  
 主要用於顯示用途。 通常和 ATTRIBUTE_NAME 相同。  
  
 MSOLAP_NODE_SCORE  
 代表模型中屬性或值的重要性。  
  
 **模型根**一律為0。  
  
 臨界**統計資料**一律為0。  
  
 **可預測屬性** 一律為0。  
  
 **輸入屬性**目前輸入屬性與目前可預測屬性的有趣性分數。  
  
 **輸入屬性狀態**一律為0。  
  
 MSOLAP_NODE_SHORT_CAPTION  
 文字字串，表示資料行的名稱或值。  
  
 **模型根**著  
  
 臨界**統計資料**著  
  
 **可預測屬性** 可預測屬性的名稱。  
  
 **輸入屬性**輸入屬性的名稱。  
  
 **輸入屬性狀態**輸入屬性的值或離散化值。  
  
##  <a name="bkmk_nodenames"></a>使用節點名稱和識別碼  
 在貝式機率分類中之節點的命名，可提供節點類型的其他資訊，讓您更容易了解模型中資訊間的關聯性。 下表顯示指派給不同節點類型之識別碼的慣例。  
  
|節點類型|節點識別碼的慣例|  
|---------------|----------------------------|  
|模型根 (1)|一律是 0。|  
|臨界統計資料節點 (26)|任意的識別碼值。|  
|可預測的屬性 (9)|開頭為 10000000 的十六進位數字<br /><br /> 例如，100000001、10000000b|  
|輸入屬性 (10)|兩部分的十六進位數字，其中第一部分永遠為 20000000，而第二部分開頭為相關可預測屬性的十六進位識別碼。<br /><br /> 例如：20000000b00000000<br /><br /> 在此情況下，相關的可預測屬性為 10000000b。|  
|輸入屬性狀態 (11)|三部分的十六進位數字，其中第一部分永遠為 30000000，第二部分開頭為相關可預測屬性的十六進位識別碼，而第三部分代表值的識別碼。<br /><br /> 例如：30000000b00000000200000000<br /><br /> 在此情況下，相關的可預測屬性為 10000000b。|  
  
 您可以使用識別碼將輸入屬性和狀態與可預測的屬性產生關聯。 例如，下列查詢會針對代表模型 `TM_NaiveBayes`之輸入屬性與可預測屬性可能組合的節點，傳回名稱和標題。  
  
```  
SELECT NODE_NAME, NODE_CAPTION  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 10  
```  
  
 預期的結果：  
  
|NODE_NAME|NODE_CAPTION|  
|----------------|-------------------|  
|20000000000000001|Bike Buyer -> Commute Distance|  
|20000000000000002|Bike Buyer -> English Education|  
|20000000000000003|Bike Buyer -> English Occupation|  
|20000000000000009|Bike Buyer -> Marital Status|  
|2000000000000000a|Bike Buyer -> Number Children At Home|  
|2000000000000000b|Bike Buyer -> Region|  
|2000000000000000c|Bike Buyer -> Total Children|  
  
 接著，您可以使用父節點的識別碼來擷取子節點。 下列查詢會擷取包含 `Marital Status` 屬性值的節點，以及每個節點的機率。  
  
```  
SELECT NODE_NAME, NODE_CAPTION, NODE_PROBABILITY  
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 11  
AND [PARENT_UNIQUE_NAME] = '20000000000000009'  
```  
  
> [!NOTE]  
>  資料行 PARENT_UNIQUE_NAME 的名稱必須括在括號內，以便與同名的保留關鍵字區別。  
  
 預期的結果：  
  
|NODE_NAME|NODE_CAPTION|NODE_PROBABILITY|  
|----------------|-------------------|-----------------------|  
|3000000000000000900000000|Bike Buyer -> Marital Status = Missing|0|  
|3000000000000000900000001|Bike Buyer -> Marital Status = S|0.457504004|  
|3000000000000000900000002|Bike Buyer -> Marital Status = M|0.542495996|  
  
##  <a name="bkmk_nodedist"></a>NODE_DISTRIBUTION 資料表  
 巢狀資料表資料行 NODE_DISTRIBUTION 通常包含節點中值分佈的統計資料。 在貝式機率分類模型中，僅會針對下列節點填入此資料表：  
  
|節點類型|巢狀資料表的內容|  
|---------------|-----------------------------|  
|模型根 (1)|空白。|  
|臨界統計資料節點 (24)|對於整組定型資料，包含所有可預測屬性和輸入屬性的摘要資訊。|  
|可預測的屬性 (9)|空白。|  
|輸入屬性 (10)|空白。|  
|輸入屬性狀態 (11)|針對可預測值與輸入屬性值的這個特定組合，包含描述定型資料中值分佈的統計資料。|  
  
 您可以使用節點識別碼或節點標題來擷取詳細資料的遞增層級。 例如，下列查詢僅針對與值 `'Marital Status = S'`相關的輸入屬性節點，從 NODE_DISTRIBUTION 資料表擷取特定的資料行。  
  
```  
SELECT FLATTENED NODE_CAPTION,  
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT], [PROBABILITY], VALUETYPE  
FROM NODE_DISTRIBUTION) as t  
FROM TM_NaiveBayes.content  
WHERE NODE_TYPE = 11  
AND NODE_CAPTION = 'Bike Buyer -> Marital Status = S'  
```  
  
 預期的結果：  
  
|NODE_CAPTION|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|t.PROBABILITY|t.VALUETYPE|  
|-------------------|-----------------------|------------------------|---------------|-------------------|-----------------|  
|Bike Buyer -> Marital Status = S|Bike Buyer|Missing|0|0|1|  
|Bike Buyer -> Marital Status = S|Bike Buyer|0|3783|0.472934117|4|  
|Bike Buyer -> Marital Status = S|Bike Buyer|1|4216|0.527065883|4|  
  
 在這些結果中，SUPPORT 資料行的值會顯示購買自行車之客戶的計數，以及指定的婚姻狀況。 PROBABILITY 資料行包含每個屬性值的機率 (僅針對此節點計算)。 如需 NODE_DISTRIBUTION 資料表所用詞彙的一般定義，請參閱 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)。  
  
###  <a name="bkmk_margstats"></a>臨界統計資料節點中的資訊  
 在貝式機率分類模型中，臨界統計資料節點的巢狀資料表包含整組定型資料的值分佈。 例如，下表包含模型 `TM_NaiveBayes`的巢狀 NODE_DISTRIBUTION 資料表中，統計資料的部分清單：  
  
|ATTRIBUTE_NAME|ATTRIBUTE_VALUE|支援|PROBABILITY|variance|VALUETYPE|  
|---------------------|----------------------|-------------|-----------------|--------------|---------------|  
|Bike Buyer|Missing|0|0|0|1|  
|Bike Buyer|0|8869|0.507263784|0|4|  
|Bike Buyer|1|8615|0.492736216|0|4|  
|Marital Status|Missing|0|0|0|1|  
|Marital Status|S|7999|0.457504004|0|4|  
|Marital Status|M|9485|0.542495996|0|4|  
|Total Children|Missing|0|0|0|1|  
|Total Children|0|4865|0.278254404|0|4|  
|Total Children|3|2093|0.119709449|0|4|  
|Total Children|1|3406|0.19480668|0|4|  
  
 包含 `Bike Buyer` 資料行，因為臨界統計資料節點永遠包含可預測屬性及其可能值的描述。 列出的其他所有資料行代表輸入屬性，以及模型中所使用的值。 值只能是遺失、離散或離散化。  
  
 在貝式機率分類模型中，可能沒有連續屬性，因此，所有數值資料都會以離散 (VALUE_TYPE = 4) 或離散化 (VALUE_TYPE = 5) 代表。  
  
 `Missing`值（VALUE_TYPE = 1）會加入至每個輸入和輸出屬性，以代表不存在於定型資料中的潛在值。 您必須仔細區別字串「遺失」和預設 `Missing` 值「遺失」。 如需詳細資訊，請參閱 [遺漏值 &#40;Analysis Services - 資料採礦&#41;](missing-values-analysis-services-data-mining.md)預先定義的模型旗標外，協力廠商外掛程式也可能擁有其他的模型旗標。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Analysis Services 的採礦模型內容-資料採礦&#41;](mining-model-content-analysis-services-data-mining.md)   
 [資料採礦模型檢視器](data-mining-model-viewers.md)   
 [資料採礦查詢](data-mining-queries.md)   
 [Microsoft Naive Bayes Algorithm](microsoft-naive-bayes-algorithm.md)  
  
  
