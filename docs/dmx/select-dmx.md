---
title: 選取 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: def96304f13f57095679056e6eab0a004b5c47d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37989877"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  **選取**陳述式中的資料採礦延伸模組 (DMX) 用於資料採礦的下列工作：  
  
-   瀏覽現有採礦模型的內容  
  
-   從現有的採礦模型建立預測  
  
-   建立現有採礦模型的副本  
  
-   瀏覽採礦結構  
  
 雖然這個陳述式的完整語法很複雜，不過用於瀏覽模型及其基礎結構的主要子句可以摘要說明如下：  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>FLATTENED  
 某些資料採礦用戶端不能接受資料採礦提供者所提供的階層式格式結果集。 用戶端可能缺少處理階層的能力，或者可能必須將結果儲存在單一反正規化資料表中。 若要將巢狀資料表中的資料轉換到扁平化資料表，必須要求查詢結果扁平化。  
  
 若要將查詢結果扁平化，使用**選取 **語法搭配**FLATTENED**選項，如下列範例所示：  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>頂端\<n > 和 ORDER BY  
 您可以使用運算式中，排序查詢的結果，並就可以使用的組合傳回結果的子集**ORDER BY**並**頂端**子句。 這在您只想將結果傳送至最可能的回應者的目標郵寄等狀況中很有用。 您可以排序目標郵寄的預測機率的預測查詢的結果，並只傳回前\<n > 的結果。  
  
## <a name="select-list"></a>選取清單  
 *\<選取清單 >* 可以包含純量資料行參考、 預測函數和運算式。 可使用的選項是根據演算法及下列內容而定：  
  
-   您是否查詢採礦結構或採礦模型  
  
-   您是否查詢內容或案例  
  
-   來源資料是否為關聯式資料表或 Cube  
  
-   您是否進行預測  
  
 在許多案例中，您可以使用別名，或根據選取清單中的項目建立簡單運算式。 例如，下列範例顯示模型資料行上的簡單運算式：  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 下列範例會針對包含預測函數結果的資料行建立別名：  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 您可以限制傳回查詢所使用的案例**其中**子句。 **何處**子句會指定該資料行中的參考**位置**運算式必須有相同的語意中的資料行參考*\<選取清單 >* 的**選取**陳述式，而且只能傳回布林運算式。 語法**其中**子句如下所示  
  
```  
WHERE < condition expression >  
```  
  
 選取清單及**何處**子句**選取**陳述式必須遵循下列規則：  
  
-   選取清單必須包含不傳回布林結果的運算式。 您可以修改運算式，但是運算式必須傳回非布林結果。  
  
-   **其中**子句必須包含傳回布林結果的運算式。 您可以修改子句，但是子句必須傳回布林結果。  
  
## <a name="predictions"></a>預測  
 您可以使用兩種類型的語法來建立預測：  
  
-   [SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [SELECT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 第一種類型的預測可以讓您即時或批次建立複雜的預測。  
  
 第二種預測類型會在採礦模型裡的可預測資料行上建立空白的預測聯結，並傳回資料行的最可能狀態。 這個查詢的結果完全以採礦模型的內容為準。  
  
 您可以插入到來源查詢的 SELECT FROM PREDICTION JOIN 陳述式的 select 陳述式，使用下列語法。  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 如需建立預測查詢的詳細資訊，請參閱[結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)。  
  
## <a name="clause-syntax"></a>子句語法  
 由於與瀏覽的複雜性**選取**陳述式、 詳細的語法元素與引數會依子句說明。 如需有關每個子句的詳細資訊，請按一下以下清單中的主題：  
  
 [SELECT DISTINCT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
 [SELECT FROM&#60;模型&#62;。內容&#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
 [SELECT FROM&#60;模型&#62;。案例&#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
 [SELECT FROM&#60;模型&#62;。SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [SELECT FROM&#60;模型&#62;。DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [SELECT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)  
  
 [SELECT FROM&#60;結構&#62;。案例](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)  
  
  
