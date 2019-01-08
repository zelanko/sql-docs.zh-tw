---
title: 模型篩選語法和範例 (Analysis Services-資料採礦) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- model filter [data mining]
- filter syntax [data mining]
- filters [data mining]
- filters [Analysis Services]
ms.assetid: c729d9b3-8fda-405e-9497-52b2d7493eae
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5c9c148995dfe83d24798c31900874e4fe3e80df
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405363"
---
# <a name="model-filter-syntax-and-examples-analysis-services---data-mining"></a>模型篩選語法和範例 (Analysis Services - 資料採礦)
  本節提供了有關模型篩選語法的詳細資訊，以及範例運算式。  
  
 
  
##  <a name="bkmk_Syntax"></a> Filter Syntax  
 篩選運算式通常相當於 WHERE 子句的內容。 您可以使用邏輯運算子 `AND`、`OR` 和 `NOT` 來連接多項條件。  
  
 在巢狀資料表中，您也可以使用 `EXISTS` 和 `NOT EXISTS` 運算子。 如果子查詢至少傳回一個資料列，`EXISTS` 條件就會評估為 `true`。 在您想要將模型限制為包含巢狀資料表中特定值的案例中，這會很有用：例如，至少購買過一次某個項目的客戶。  
  
 如果子查詢中指定的條件不存在，`NOT EXISTS` 條件就會評估為 `true`。 例如，當您想要將模型限制為從未購買過特定項目的客戶時。  
  
 一般語法如下：  
  
```  
<filter>::=<predicate list>  | ( <predicate list> )  
<predicate list>::= <predicate> | [<logical_operator> <predicate list>]   
<logical_operator::= AND| OR  
<predicate>::= NOT <predicate>|( <predicate> ) <avPredicate> | <nestedTablePredicate> | ( <predicate> )   
<avPredicate>::= <columnName> <operator> <scalar> | <columnName> IS [NOT] NULL  
<operator>::= = | != | <> | > | >= | < | <=  
<nestedTablePredicate>::= EXISTS (<subquery>)  
<subquery>::=SELECT * FROM <columnName>[ WHERE  <predicate list> ]  
```  
  
 *filter*  
 包含一個或多個由邏輯運算子連接的述詞。  
  
 *predicate list*  
 一個或多個由邏輯運算子分隔的有效篩選運算式。  
  
 *columnName*  
 採礦結構資料行的名稱。  
  
 logical operator  
 `AND`, `OR`, `NOT`  
  
 *avPredicate*  
 只能套用至純量採礦結構資料行的篩選運算式。 *avPredicate* 運算式可用於模型篩選或巢狀資料表篩選中。  
  
 使用下列任何運算子的運算式只能套用至連續資料行。 所解碼的字元：  
  
-   **\<** (小於)  
  
-   **>** (大於)  
  
-   **>=** (大於或等於)  
  
-   **\<=** (小於或等於)  
  
> [!NOTE]  
>  不論資料類型為何，這些運算子都無法套用至 `Discrete`、`Discretized` 或 `Key` 類型的資料行。  
  
 使用下列任何運算子的運算式可以套用至連續、離散、離散化或索引鍵資料行：  
  
-   **=** (等於)  
  
-   **!=** (不等於)  
  
-   **是 NULL**  
  
 如果 *avPredicate*套用至離散化資料行，篩選中所用的值就可以是特定值區中的任何值。  
  
 換言之，雖然您沒有將條件定義為 `AgeDisc = '25-35'`，但是系統仍會計算並使用該間隔中的值。  
  
 例如：  `AgeDisc = 27`  表示與 27 位於相同間隔中的任何值，在此情況中就是 25-35。  
  
 *nestedTablePredicate*  
 套用至巢狀資料表的篩選運算式。 它只能用於模型篩選中。  
  
 *nestedTablePredicate*的子查詢引數只能套用至資料表採礦結構資料行。  
  
 子查詢  
 SELECT 陳述式，後面接著一個有效的述詞或述詞清單。  
  
 所有述詞都必須屬於 *avPredicates*中所描述的類型。 此外，這些述詞只能參考目前巢狀資料表中由 *columnName*引數所識別的資料行。  
  
### <a name="limitations-on-filter-syntax"></a>篩選語法的限制  
 下列限制會套用至篩選：  
  
-   篩選只能包含簡易述詞。 這些述詞包括數學運算子、純量和資料行名稱。  
  
-   篩選語法不支援使用者定義函數。  
  
-   篩選語法不支援非布林運算子，例如加號或減號。  
  
## <a name="examples-of-filters"></a>篩選的範例  
 下列範例將示範套用至採礦模型之篩選的使用方式。 如果您使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 來建立篩選運算式，在 [篩選] 對話方塊的 [屬性] 視窗和 [運算式] 窗格中，您只會看見顯示在 WITH FILTER 關鍵字之後的字串。 在該處加入採礦結構定義的目的是為了讓人更容易了解資料行類型和使用方式。  
  
###  <a name="bkmk_Ex1"></a> 範例 1:一般案例層級的篩選  
 這則範例會顯示一個簡易篩選，它可將模型中使用的案例限制為職業是建築師而且年齡超過 30 歲的客戶。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_1  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH FILTER (Age > 30 AND Occupation='Architect')  
```  
  

  
###  <a name="bkmk_Ex2"></a> 範例 2:使用巢狀資料表屬性的案例層級篩選  
 如果您的採礦結構包含巢狀資料表，就可以篩選巢狀資料表中是否存某個值，或篩選包含特定值的巢狀資料表資料列。 這則範例會將模型所使用的案例限制為年齡超過 30 歲而且至少有一次購買包含牛奶的客戶。  
  
 如此範例所示，篩選僅使用模型中包含的資料行並非必要條件。 巢狀資料表 **Products** 屬於採礦結構的一部分，但是不包含在採礦模型中。 不過，您仍然可以篩選巢狀資料表中的值和屬性。 若要檢視這些案例的詳細資料，您必須啟用鑽研。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_2  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT  
)  
WITH DRILLTHROUGH,   
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk')  
)  
```  
  
 
  
###  <a name="bkmk_Ex3"></a> 範例 3︰多個巢狀資料表屬性的案例層級篩選  
 此範例顯示三個部分的篩選：第一個條件會套用至案例資料表、第二個條件會套用至巢狀資料表中的屬性，而第三個條件會套用至其中一個巢狀資料表資料行中的特定值。  
  
 篩選中的第一個條件 `Age > 30`會套用至案例資料表中的資料行。 其餘條件則會套用至巢狀資料表。  
  
 第二個條件 `EXISTS (SELECT * FROM Products WHERE ProductName='Milk'`會檢查巢狀資料表中是否至少有一次購買包含牛奶。 第三個條件 `Quantity>=2`表示客戶必須在單一交易中，至少購買過兩個單位的牛奶。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_3  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
)  
)  
FILTER (Age > 30 AND EXISTS (SELECT * FROM Products WHERE ProductName='Milk'  AND Quantity >= 2)   
)  
```  
  

  
###  <a name="bkmk_Ex4"></a> 範例 4︰巢狀資料表屬性不存在的案例層級篩選  
 這則範例會顯示如何透過篩選巢狀資料表中不存在的屬性，將案例限制為沒有購買特定項目的客戶。 在此範例中，模型是使用年齡超過 30 歲而且從未購買過牛奶的客戶進行培訓。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_4  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName  
)  
)  
FILTER (Age > 30 AND NOT EXISTS (SELECT * FROM Products WHERE ProductName='Milk') )  
```  
  

  
###  <a name="bkmk_Ex5"></a> 範例 5:多個巢狀資料表值的篩選  
 此範例的目的是要顯示巢狀資料表篩選。 巢狀資料表篩選是在案例篩選之後套用的，而且只會限制巢狀資料表資料列。  
  
 這個模型可能會包含多個具有空白巢狀資料表的案例，因為沒有指定 EXISTS。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_5  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
WITH DRILLTHROUGH  
```  
  

  
###  <a name="bkmk_Ex6"></a> 範例 6:巢狀資料表屬性的篩選和 EXISTS  
 在此範例中，巢狀資料表的篩選會將資料列限制為包含牛奶或瓶裝水的資料列。 然後，系統會使用 `EXISTS` 陳述式來限制模型中的案例。 這樣做可確保巢狀資料表不是空的。  
  
```  
ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_6  
(  
CustomerId,  
Age,  
Occupation,  
MaritalStatus PREDICT,  
Products PREDICT  
(  
ProductName KEY,  
Quantity        
) WITH FILTER(ProductName='Milk' OR ProductName='bottled water')  
)  
FILTER (EXISTS (Products))  
```  
  

  
###  <a name="bkmk_Ex7"></a> 範例 7:複雜的篩選組合  
 這個模型的狀況與範例 4 的狀況很相似，但是更為複雜。 巢狀的資料表中， **ProductsOnSale**，具有篩選條件`(OnSale)`表示的值**OnSale**必須是`true`中所列產品**ProductName**. 其中， **OnSale** 是結構資料行。  
  
 第二個部分的篩選器，如**ProductsNotOnSale**，會重複此語法，但是它會篩選產品的值**OnSale**是`not true``(!OnSale)`。  
  
 最後，這些條件會組合並在案例資料表中加入一項額外的限制。 其結果是針對年齡超過 25 歲的所有客戶，根據 **ProductsOnSale** 清單中包含的案例來預測 **ProductsOnSale** 清單中的購買產品。  
  
 `ALTER MINING STRUCTURE MyStructure  ADD MINING MODEL MyModel_7`  
  
 `(`  
  
 `CustomerId,`  
  
 `Age,`  
  
 `Occupation,`  
  
 `MaritalStatus,`  
  
 `ProductsOnSale`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(OnSale),`  
  
 `ProductsNotOnSale PREDICT ONLY`  
  
 `(`  
  
 `ProductName KEY`  
  
 `) WITH FILTER(!OnSale)`  
  
 `)`  
  
 `WITH DRILLTHROUGH,`  
  
 `FILTER (EXISTS (ProductsOnSale) AND EXISTS(ProductsNotOnSale) AND Age > 25)`  
  
  
  
###  <a name="bkmk_Ex8"></a> 範例 8:日期的篩選  
 您可以篩選日期輸入資料行，就如同任何其他資料一樣。 日期/時間類型的資料行中包含的日期為連續日期，因此您可以使用如大於 (>) 或小於 (<) 等運算子指定日期範圍。 如果您的資料來源不是以 Continuous 資料類型而是離散或文字值來表示日期，則無法篩選日期範圍，而必須指定個別的離散值。  
  
 不過，如果篩選所使用的日期資料行也是時間序列模型的索引鍵資料行，則無法在模型的日期資料行上建立篩選。 這是因為時間序列模型和時序群集模型中，日期資料行可能會當做 `KeyTime` 或 `KeySequence` 類型處理。  
  
 如果您必須在時間序列模型中篩選連續值，可以在採礦結構中建立資料行的複本，然後在新的資料行上篩選模型。  
  
 例如，下列運算式代表已加入至預測模型中 `Continuous` 類型之日期資料行的篩選。  
  
 `=[DateCopy] > '12:31:2003:00:00:00'`  
  
> [!NOTE]  
>  請注意，您加入至模型的額外資料行可能會影響結果。 因此，如果您不想要在序列計算中使用資料行，應該只將資料行加入至採礦結構，而不是加入至模型。 您也可以將資料行上的模型旗標設定為 `PredictOnly` 或 `Ignore`。 如需詳細資訊，請參閱[模型旗標 &#40;資料採礦&#41;](modeling-flags-data-mining.md)。  
  
 對於其他模型類型，日期可以當做輸入準則或篩選準則，就如同任何其他資料行一樣。 不過，如果您必須使用 `Continuous` 資料類型不支援的特定資料粒度層級，可以使用運算式擷取要用於篩選和分析的單位，在資料來源中建立衍生值。  
  
> [!WARNING]  
>  當您指定日期作為篩選準則時，不論目前作業系統的日期格式為何，都必須使用下列格式： `mm/dd/yyyy`。 任何其他格式都會產生錯誤。  
  
 例如，如果您想要篩選客服中心結果，只顯示週末，可以在資料來源檢視中建立運算式以擷取每個日期的工作天名稱，然後將該工作天名稱值用於輸入或當做篩選的離散值。 請記得，重複值會影響模型，因此您應該只使用其中一個資料行，而不是日期資料行加上衍生值。  
  
 
  
## <a name="see-also"></a>另請參閱  
 [採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](mining-models-analysis-services-data-mining.md)   
 [測試及驗證 &#40;資料採礦&#41;](testing-and-validation-data-mining.md)  
  
  
