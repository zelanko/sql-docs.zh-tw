---
title: SELECT FROM&lt;模型&gt;預測 JOIN (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PREDICTION
- PREDICTION_JOIN
- SELECT
- join
- FROM
- PREDICTION JOIN
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- PREDICTION JOIN statement
- natural prediction joins [DMX]
- open query predictions
- singleton query predictions [DMX]
- SELECT FROM <model> PREDICTION JOIN statement
ms.assetid: 7ca37fec-4a50-4d79-b1d6-1c7c12176946
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 77afa48b63dd145406cdead7e7b0b0bf675aedb5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>SELECT FROM&lt;模型&gt;預測 JOIN (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  使用採礦模型預測外部資料來源中的資料行狀態。 **PREDICTION JOIN**陳述式符合來源查詢中每個案例的模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引數  
 *n*  
 選擇性。 指定要傳回多少資料列的整數。  
  
 *select 運算式清單*  
 從採礦模型衍生之資料行識別碼與運算式的逗號分隔清單。  
  
 *model*  
 模型識別碼。  
  
 *子選擇*  
 內嵌的 SELECT 陳述式。  
  
 *來源資料查詢*  
 來源查詢。  
  
 *聯結的對應清單*  
 選擇性。 比較模型中的資料行與來源查詢中的資料行的邏輯運算式。  
  
 *條件運算式*  
 選擇性。 限制從資料行清單傳回之值的條件。  
  
 *expression*  
 選擇性。 傳回純量值的運算式。  
  
## <a name="remarks"></a>備註  
 ON 子句會定義來源查詢中的資料行與採礦模型中的資料行之間的對應。 這個對應用於將來源查詢中的資料行導向採礦模型中的資料行，使資料行能做為建立預測時的輸入。 中的資料行\<*聯結的對應清單*> 相關使用等號 （=），如下列範例所示：  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 您若是在 ON 子句中繫結巢狀資料表，請確定是將索引鍵資料行繫結至任何非索引鍵資料行，讓演算法能夠正確地識別巢狀資料行的記錄屬於哪個案例。  
  
 預測聯結的來源查詢可以是資料表或單一查詢。  
  
 您可以指定不會傳回資料表運算式中的預測函數\< *select 運算式清單*> 而\<*條件運算式*>。  
  
 **NATURAL PREDICTION JOIN**會自動對應在一起的來源查詢中的資料行名稱符合模型中的資料行名稱。 如果您使用**自然預測**，您可以省略 ON 子句。  
  
 WHERE 條件僅能套用到可預測的資料行或相關的資料行。  
  
 ORDER BY 子句僅能接受單一資料行做為引數，也就是說，您無法排序一個以上的資料行。  
  
## <a name="example-1-singleton-query"></a>範例 1：單一查詢  
 下列範例顯示如何建立查詢，以預測某個特定的人是否會即時購買自行車。 在此查詢中，資料不會儲存在資料表或其他資料來源中，但是會直接輸入到查詢中。 查詢中的個人有下列特徵：  
  
-   35 歲  
  
-   擁有一棟房子  
  
-   擁有兩部車  
  
-   家裡有兩個小孩  
  
 查詢使用 TM Decision Tree 採礦模型和關於主體的已知的特性，會傳回布林值，描述個人是否購買自行車，以及一組表格式值，傳回[PredictHistogram &#40; DMX &#41;](../dmx/predicthistogram-dmx.md)函式，說明如何進行預測。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>範例 2：使用 OPENQUERY  
 下列範例顯示如何使用儲存在外部資料集中的潛在客戶清單，建立批次預測查詢。 因為資料表已定義的執行個體的資料來源檢視的一部分[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，查詢就可以使用[OPENQUERY](../dmx/source-data-query-openquery.md)來擷取資料。 因為資料表中的資料行名稱不同的採礦模型**ON**子句必須用來在資料表中的資料行對應到模型中的資料行。  
  
 查詢會傳回資料表中每個人的名字與姓氏，以及表示每個人是否可能購買自行車，其中 0 表示「可能不會購買自行車」，而 1 表示「可能會購買自行車」。 最後一個資料行包含預測結果的機率。  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 若要將資料集限制為僅預測購買自行車的客戶，然後依客戶名稱排序清單，您可以將 WHERE 子句和 ORDER BY 子句加入到先前的範例中：  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>範例 3：預測關聯  
 下列範例顯示如何使用從 [!INCLUDE[msCoName](../includes/msconame-md.md)] 關聯分析演算法建立之模型建立預測。 關聯模型的預測可用於建議相關的產品。 例如，下列查詢會傳回最可能一起購買的三項產品：  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 [預測 &#40; DMX &#41;](../dmx/predict-dmx.md)函式是多型態類型，並可以搭配所有模型類型。 您可以使用 value3 做為函數的引數，以限制查詢所傳回的項目數目。 **選取**遵循 NATURAL PREDICTION JOIN 子句的清單提供要用於預測做為輸入的值。  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 範例結果：  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 包含可預測屬性 `[v Assoc Seq Line Items]` 的資料行是資料表資料行，因此，查詢會傳回包含巢狀資料表的單一資料行。 根據預設，巢狀資料表資料行的名稱為 `Expression`。 如果您的提供者不支援階層式資料列集，您可以使用**FLATTENED**關鍵字，讓結果更容易檢視，在此範例所示。  
  
## <a name="see-also"></a>請參閱  
 [SELECT &#40; DMX &#41;](../dmx/select-dmx.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
