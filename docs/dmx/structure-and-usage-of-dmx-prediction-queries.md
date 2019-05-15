---
title: 結構和 DMX 預測查詢的使用方式 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37ff157cbddb0894880f12097c977b923d92f177
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981910"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 預測查詢的結構和使用方式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，您可以使用預測查詢中的資料採礦延伸模組 (DMX) 預測未知的資料行的值，在新的資料集，根據採礦模型的結果。  
  
 您使用的查詢類型依您想要從模型取得的資訊內容而定。 如果您想要即時建立簡單預測，例如知道網站上的潛在客戶是否符合自行車買家的角色，則使用單一查詢。 如果您想要從資料來源中包含的一組案例建立一批預測，則使用一般預測查詢。  
  
## <a name="prediction-types"></a>預測類型  
 您可以使用 DMX 建立下列預測類型：  
  
 預測聯結  
 用於根據採礦模型中存在的模式建立輸入資料的預測。 此查詢陳述式後面必須接著**ON**提供採礦模型資料行的輸入資料行之間的聯結條件的子句。  
  
 自然預測聯結  
 用於建立的預測，是以採礦模型中與您所查詢之資料表中的資料行名稱完全相符的資料行名稱為基礎。 此查詢陳述式不需要**ON**子句，因為聯結條件會自動產生根據採礦模型資料行的輸入資料行之間比對的名稱。  
  
 空白預測聯結  
 用於探索最可能的預測，不必提供輸入資料。 這會傳回只以採礦模型之內容為基礎的預測。  
  
 單一查詢  
 提供資料給查詢以建立預測。 這個陳述式很實用，因為您可以提供單一案例給查詢，快速取得結果。 例如，您可以使用查詢預測身分為女性、35 歲且已婚的某人是否可能採購自行車。 這個查詢不需要外部資料來源。  
  
## <a name="query-structure"></a>查詢結構  
 若要在 DMX 中建立預測查詢，您使用下列元素的組合：  
  
-   **選取 [壓平合併]**  
  
-   **TOP**  
  
-   **從***\<模型 >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 **選取**預測查詢的項目定義的資料行和運算式，會出現在結果集，並可以包含下列資料：  
  
-   **預測**或是**PredictOnly**從採礦模型的資料行。  
  
-   用於建立預測之輸入資料中的任何資料行。  
  
-   傳回資料行的函數。  
  
 **FROM** *\<模型 >* **PREDICTION JOIN**項目會定義要用來建立預測的來源資料。 若是單一查詢，這是指派至資料行的一連串值。 若是空白預測聯結，這會保持空白。  
  
 **ON**元素會對應至外部資料集中的資料行的採礦模型中定義的資料行。 如果是建立空白預測聯結查詢或自然預測聯結，不必包含這個元素。  
  
 您可以使用**其中**子句篩選預測查詢的結果。 您可以使用**頂端**或是**ORDER BY**子句選取最可能的預測。 如需使用這些子句的詳細資訊，請參閱 <<c0> [ 選取&#40;DMX&#41;](../dmx/select-dmx.md)。</c0>  
  
 預測陳述式之語法的詳細資訊，請參閱[FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41; ](../dmx/select-from-model-prediction-join-dmx.md)並[SELECT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
