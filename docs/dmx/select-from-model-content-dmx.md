---
title: 選取 [ &lt;從&gt;模型]。內容（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 61cbacee45147b7b6203e9cb2164c02cdc2c7453
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892835"
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>選取 [ &lt;從&gt;模型]。內容（DMX）
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回指定之資料採礦模型的採礦模型結構描述資料列集。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *運算式清單*  
 從 Content 結構描述資料列集衍生之資料行的逗號分隔清單。  
  
 *model*  
 模型識別碼。  
  
 *條件運算式*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 [**從** _ \<模型_選取]>**。CONTENT**語句會傳回每個演算法特定的內容。 例如，您可能想要使用自訂應用程式中關聯規則模型之所有規則的描述。 您可以使用 [**從\<模型選取]>。** 要在模型的 NODE_RULE 資料行中傳回值的 CONTENT 語句。  
  
 下表列出包含在採礦模型內容中的資料行。  
  
> [!NOTE]  
>  演算法可能對資料行有不同的解譯，以便正確地表示內容。 如需每個演算法的「採礦模型」內容的描述，以及如何解讀及查詢每個模型類型之「採礦模型」內容的秘訣，請參閱[&#40;Analysis Services 資料採礦&#41;的「採礦模型內容](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」。  
  
|CONTENT 資料列集資料行|描述|  
|---------------------------|-----------------|  
|MODEL_CATALOG|目錄名稱。 如果提供者不支援目錄，則為 NULL。|  
|MODEL_SCHEMA|不合格的結構描述名稱。 如果提供者不支援結構描述，則為 NULL。|  
|MODEL_NAME|模型名稱。 這個資料行不能包含 NULL。|  
|ATTRIBUTE_NAME|對應至節點之屬性的名稱。|  
|NODE_NAME|節點的名稱。|  
|NODE_UNIQUE_NAME|模型內節點的唯一名稱。|  
|NODE_TYPE|代表節點類型的整數。 .|  
|NODE_GUID|節點 GUID。 如果沒有 GUID，則為 NULL。|  
|NODE_CAPTION|與節點相關聯的標籤或標題。 主要用於顯示用途。 如果標題不存在，就會傳回 NODE_NAME。|  
|CHILDREN_CARDINALITY|節點擁有的子系數目。|  
|PARENT_UNIQUE_NAME|節點之父系的唯一名稱。|  
|NODE_DESCRIPTION|節點的描述。|  
|NODE_RULE|代表內嵌於節點中之規則的 XML 片段。 XML 字串的格式是以 PMML 標準為基礎。|  
|MARGINAL_RULE|描述父系到節點之路徑的 XML 片段。|  
|NODE_PROBABILITY|結束於節點之路徑的機率。|  
|MARGINAL_PROBABILITY|從父節點到達節點的機率。|  
|NODE_DISTRIBUTION|包含描述節點中值分佈之統計資料的資料表。|  
|NODE_SUPPORT|支援這個節點的案例數目。|  
  
## <a name="examples"></a>範例  
 下列程式碼會針對加入至目標郵寄採礦結構之決策樹模型，傳回父節點的識別碼。  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 預期的結果：  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 下列查詢會使用**IsDescendant**函數來傳回上一個查詢中所傳回之節點的直屬子系。  
  
> [!NOTE]  
>  因為 NODE_NAME 的值是字串，所以您無法使用子 select 語句，將 NODE_ID 當做引數傳回至**IsDescendant**函數。  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 預期的結果：  
  
 由於此模型是決策樹模型，因此模型父節點的下階包含單一臨界統計資料節點、代表可預測屬性的節點，以及包含輸入屬性與值的多個節點。 如需詳細資訊，請參閱 [決策樹模型的採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining)。  
  
## <a name="using-the-flattened-keyword"></a>使用 FLATTENED 關鍵字  
 採礦模型內容經常包含巢狀資料表資料行中，關於模型的有趣資訊。 FLATTENED 關鍵字可讓您從巢狀資料表資料行擷取資料，而不必使用支援階層式資料列集的提供者。  
  
 下列查詢會從貝氏機率分類模型傳回單一節點、臨界統計資料節點 (NODE_TYPE = 26)。 不過，此節點在 NODE_DISTRIBUTION 資料行中包含巢狀資料表。 因此，巢狀資料表資料行是扁平化的，而且會針對巢狀資料表中的每個資料列傳回一個資料列。 純量資料行 MODEL_NAME 的值會針對巢狀資料表中的每個資料列重複。  
  
 同時請注意，如果僅指定巢狀資料表資料行的名稱，就會針對巢狀資料表中的每個資料行傳回一個新的資料行。 根據預設，巢狀資料表的名稱前面會加上每個巢狀資料表資料行的名稱。  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 範例結果︰  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION.ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION.PROBABILITY|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 下列範例示範如何使用子 SELECT 陳述式，從巢狀資料表僅傳回某些資料行。 您可以使用巢狀資料表之資料表名稱的別名來簡化顯示，如下所示。  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 範例結果︰  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>另請參閱  
 [選取 &#40;DMX&#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
