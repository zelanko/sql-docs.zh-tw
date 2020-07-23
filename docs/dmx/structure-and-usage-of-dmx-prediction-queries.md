---
title: DMX 預測查詢的結構和使用方式 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e2aaeedff9eb0d22d6a7175641177f803379adaa
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970267"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 預測查詢的結構和使用方式
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  在中 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，您可以使用資料採礦延伸模組（DMX）中的預測查詢，根據採礦模型的結果，預測新資料集內的未知資料行值。  
  
 您使用的查詢類型依您想要從模型取得的資訊內容而定。 如果您想要即時建立簡單預測，例如知道網站上的潛在客戶是否符合自行車買家的角色，則使用單一查詢。 如果您想要從資料來源中包含的一組案例建立一批預測，則使用一般預測查詢。  
  
## <a name="prediction-types"></a>預測類型  
 您可以使用 DMX 建立下列預測類型：  
  
 預測聯結  
 用於根據採礦模型中存在的模式建立輸入資料的預測。 此查詢語句後面必須接著**ON**子句，以提供模型資料行與輸入資料行之間的聯結條件。  
  
 自然預測聯結  
 用於建立的預測，是以採礦模型中與您所查詢之資料表中的資料行名稱完全相符的資料行名稱為基礎。 此查詢語句不需要**ON**子句，因為聯結條件會根據模型資料行與輸入資料行之間的相符名稱自動產生。  
  
 空白預測聯結  
 用於探索最可能的預測，不必提供輸入資料。 這會傳回只以採礦模型之內容為基礎的預測。  
  
 單一查詢  
 提供資料給查詢以建立預測。 這個陳述式很實用，因為您可以提供單一案例給查詢，快速取得結果。 例如，您可以使用查詢預測身分為女性、35 歲且已婚的某人是否可能採購自行車。 這個查詢不需要外部資料來源。  
  
## <a name="query-structure"></a>查詢結構  
 若要在 DMX 中建立預測查詢，您使用下列元素的組合：  
  
-   **選取 [簡維]**  
  
-   **返回頁首**  
  
-   **從** *\<model>***預測聯結**      
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 預測查詢的**SELECT**元素會定義將出現在結果集內的資料行和運算式，而且可以包含下列資料：  
  
-   從「採礦模型」**預測**或**PredictOnly**資料行。  
  
-   用於建立預測之輸入資料中的任何資料行。  
  
-   傳回資料行的函數。  
  
 **FROM** *\<model>* **預測聯結**元素會定義要用來建立預測的來源資料。 若是單一查詢，這是指派至資料行的一連串值。 若是空白預測聯結，這會保持空白。  
  
 **ON**元素會將在採礦模型中定義的資料行對應至外部資料集內的資料行。 如果是建立空白預測聯結查詢或自然預測聯結，不必包含這個元素。  
  
 您可以使用**WHERE**子句來篩選預測查詢的結果。 您可以使用**TOP**或**ORDER by**子句來選取最有可能的預測。 如需有關使用這些子句的詳細資訊，請參閱[SELECT &#40;DMX&#41;](../dmx/select-dmx.md)。  
  
 如需預測語句語法的詳細資訊，請參閱[從 &#60;模型選取&#62; 預測聯結 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md) ，然後[從 &#60;模型&#62; &#40;DMX&#41;中選取](../dmx/select-from-model-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
