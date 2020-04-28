---
title: ALTER 採礦結構（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5535428d89a0d14b60e3ac79d281f63b4c69bfb5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68889868"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  建立以現有採礦結構為基礎的新採礦模型。  當您使用**ALTER database**語句來建立新的採礦模型時，該結構必須已經存在。 相反地，當您使用語句時，[建立 &#40;DMX&#41;的「採礦模型](../dmx/create-mining-model-dmx.md)」時，您會建立模型，並同時自動產生其基礎的「採礦結構」。  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>引數  
 *structure*  
 要對其加入採礦模型之採礦結構的名稱。  
  
 *模型*  
 採礦模型的唯一名稱。  
  
 *資料行定義清單*  
 資料行定義的逗號分隔清單。  
  
 *嵌套資料行定義清單*  
 取自巢狀資料表之資料行的逗號分隔清單 (如果適用的話)。  
  
 *嵌套篩選準則*  
 套用至巢狀資料表中資料行的篩選運算式。  
  
 *演算法*  
 提供者所定義的資料採礦演算法名稱。  
  
> [!NOTE]  
>  您可以使用 DMSCHEMA_MINING_SERVICES 資料列[集](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)來抓取目前提供者所支援的演算法清單。 若要查看目前實例中支援的演算法[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，請參閱[資料採礦屬性](https://docs.microsoft.com/analysis-services/server-properties/data-mining-properties)。  
  
 *參數清單*  
 選擇性。 提供者自訂之演算法參數的逗號分隔清單。  
  
 *篩選準則*  
 套用至案例資料表中之資料行的篩選運算式。  
  
## <a name="remarks"></a>備註  
 如果採礦結構包含複合索引鍵，採礦模型就必須包含結構中定義的所有索引鍵資料行。  
  
 如果模型不需要可預測資料行 (例如使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 群集與 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時序群集演算法建立的模型)，您就不必在陳述式中包含資料行定義。 產生之模型中的所有屬性都會當成輸入處理。  
  
 在適用于案例資料表的**WITH**子句中，您可以指定篩選和鑽取的選項：  
  
-   新增**filter**關鍵字和篩選準則。 篩選器會套用到採礦模型中的案例。  
  
-   新增 [**鑽取**關鍵字]，讓採礦模型的使用者向下切入到案例資料的模型結果。 在資料採礦延伸模組 (DMX) 中，只有在建立模型時才能啟用鑽研。  
  
 若要同時使用案例篩選和鑽取，請使用下列範例所示的語法，結合單一**WITH**子句中的關鍵字：  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>資料行定義清單  
 請藉由指定資料行定義清單 (其中包含每個資料行的下列資訊) 來定義模型的結構：  
  
-   名稱 (強制的)  
  
-   別名 (選擇性)  
  
-   模型旗標  
  
-   預測要求，表示資料行是否包含可預測的值（由**PREDICT**或**PREDICT_ONLY**子句表示）  
  
 使用下列資料行定義清單的語法來定義單一資料行：  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>資料行名稱和別名  
 在資料行定義清單中使用的資料行名稱，必須是採礦結構中所使用的資料行名稱。 不過，您也可以選擇定義別名來代表採礦模型中的結構資料行。 您也可以為相同的結構資料行建立多個資料行定義，然後為每個資料行副本指派不同的別名及預測使用方式。 根據預設，如果沒有定義別名，就會使用結構資料行名稱。 如需詳細資訊，請參閱[建立模型資料行的別名](https://docs.microsoft.com/analysis-services/data-mining/create-an-alias-for-a-model-column)。  
  
 針對嵌套的資料表資料行，您可以指定嵌套資料表的名稱，將資料類型指定為 [**資料表**]，然後提供要包含在模型中的嵌套資料行清單，並以括弧括住。  
  
 您可以將篩選準則運算式加在巢狀資料表資料行定義之後，以定義套用至巢狀資料表的篩選運算式。  
  
### <a name="modeling-flags"></a>模型旗標  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援下列用於採礦模型資料行的模型旗標：  
  
> [!NOTE]  
>  NOT_NULL 模型旗標適用於採礦結構資料行。 如需詳細資訊，請參閱 [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)。  
  
|||  
|-|-|  
|詞彙|定義|  
|**回歸輸入變數**|指示演算法可以在迴歸演算法的迴歸公式中使用指定的資料行。|  
|**MODEL_EXISTENCE_ONLY**|指出屬性資料行的值是否比屬性的存在更重要。|  
  
 您可以為一個資料行定義多個模型旗標。 如需有關如何使用模型旗標的詳細資訊，請參閱[&#40;DMX&#41;的模型旗標](../dmx/modeling-flags-dmx.md)。  
  
### <a name="prediction-clause"></a>預測子句  
 預測子句描述如何使用預測資料行。 下表列出可能的子句。  
  
|||  
|-|-|  
|**PREDICT**|這個資料行可以由模型預測，而其值可以用來當做輸入以預測其他可預測資料行的值。|  
|**PREDICT_ONLY**|這個資料行可以依模型預測，但是其值不能用於輸入案例中以預測其他可預測資料行的值。|  
  
## <a name="filter-criteria-expressions"></a>篩選準則運算式  
 您可以定義篩選來限制用於採礦模型中的案例。 篩選可套用至案例資料表中的資料行或巢狀資料表中的資料列，或套用至兩者。  
  
 篩選準則運算式是經過簡化的 DMX 述詞，與 WHERE 子句類似。 篩選運算式限於使用基本數學運算子、純量和資料行名稱的公式。 EXISTS 運算子則是例外；如果子查詢至少傳回一個資料列，該運算子就會評估為 True。 述詞可以使用常見的邏輯運算子 AND、OR 和 NOT 等來結合。  
  
 如需有關與採礦模型搭配使用之篩選的詳細資訊，請參閱[&#40;Analysis Services 資料採礦&#41;的採礦模型篩選](https://docs.microsoft.com/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)。  
  
> [!NOTE]  
>  篩選中的資料行必須是採礦結構資料行。 您無法在模型資料行或別名資料行上建立篩選。  
  
 如需 DMX 運算子和語法的詳細資訊，請參閱[採礦模型資料行](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)。  
  
## <a name="parameter-definition-list"></a>參數定義清單  
 您可以將演算法參數加入至參數清單，以調整模型的效能和功能。 可以使用的參數是依照您在 USING 子句中指定的演算法而定。 如需與每個演算法相關聯的參數清單，請參閱[資料採礦演算法 &#40;Analysis Services 資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)。  
  
 參數清單的語法如下：  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>範例 1：將模型加入至結構  
 下列範例會將貝氏貝氏機率分類採礦模型新增至**新的郵寄**採礦結構，並將屬性狀態的最大數目限制為50。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>範例 2：將篩選模型加入至結構  
 下列範例會將「採礦模型`Naive Bayes Women`」新增至新的「**郵件**」採礦結構。 新模型的基本結構與在範例 1 中加入的採礦模型相同；不過這個模型將取自採礦結構的案例限制為年過 50 的女性客戶。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>範例 3：將篩選模型加入至具有巢狀資料表的結構  
 下列範例將採礦模型加入至購物籃採礦結構的修改版本中。 範例中使用的採礦結構已經過修改，以加入**區域**資料行（其中包含用戶端區域的屬性）和**收入群組**資料行（使用 [**高** **]、[中]** 或 [**低**] 值來分類客戶收入）。  
  
 此採礦結構也會包含列出客戶已購買之項目清單的巢狀資料表。  
  
 因為採礦結構包含巢狀資料表，所以您可以在案例資料表、巢狀資料表 (或這兩者) 上定義篩選。 此範例結合了案例篩選和巢狀資料列篩選，將案例限制為已購買其中一款公路胎型號的富有歐洲客戶。  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
