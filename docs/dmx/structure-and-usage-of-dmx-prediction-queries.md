---
description: DMX 預測查詢的結構和使用方式
title: DMX 預測查詢的結構和使用方式 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 242e86a0ac74dacd8682825f25adab4a847a82e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500757"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 預測查詢的結構和使用方式
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  在中 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，您可以在資料採礦延伸模組 (DMX) 中使用預測查詢，根據採礦模型的結果來預測新資料集中的未知資料行值。  
  
 您使用的查詢類型依您想要從模型取得的資訊內容而定。 如果您想要即時建立簡單預測，例如知道網站上的潛在客戶是否符合自行車買家的角色，則使用單一查詢。 如果您想要從資料來源中包含的一組案例建立一批預測，則使用一般預測查詢。  
  
## <a name="prediction-types"></a>預測類型  
 您可以使用 DMX 建立下列預測類型：  
  
 預測聯結  
 用於根據採礦模型中存在的模式建立輸入資料的預測。 這個查詢語句後面必須接著一個 **ON** 子句，此子句會在「採礦模型」資料行和輸入資料行之間提供聯結條件。  
  
 自然預測聯結  
 用於建立的預測，是以採礦模型中與您所查詢之資料表中的資料行名稱完全相符的資料行名稱為基礎。 此查詢語句不需要 **ON** 子句，因為聯結條件會根據「採礦模型」資料行和輸入資料行之間的相符名稱自動產生。  
  
 空白預測聯結  
 用於探索最可能的預測，不必提供輸入資料。 這會傳回只以採礦模型之內容為基礎的預測。  
  
 單一查詢  
 提供資料給查詢以建立預測。 這個陳述式很實用，因為您可以提供單一案例給查詢，快速取得結果。 例如，您可以使用查詢預測身分為女性、35 歲且已婚的某人是否可能採購自行車。 這個查詢不需要外部資料來源。  
  
## <a name="query-structure"></a>查詢結構  
 若要在 DMX 中建立預測查詢，您使用下列元素的組合：  
  
-   **選取 [壓平合併]**  
  
-   **返回頁首**  
  
-   **來源** *\<model>***預測聯結**      
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 預測查詢的 **SELECT** 元素會定義將出現在結果集中的資料行和運算式，並可包含下列資料：  
  
-   從採礦模型**預測**或**PredictOnly**資料行。  
  
-   用於建立預測之輸入資料中的任何資料行。  
  
-   傳回資料行的函數。  
  
 **FROM** *\<model>* **預測聯結**元素會定義要用來建立預測的來源資料。 若是單一查詢，這是指派至資料行的一連串值。 若是空白預測聯結，這會保持空白。  
  
 **ON**元素會將採礦模型中所定義的資料行對應至外部資料集中的資料行。 如果是建立空白預測聯結查詢或自然預測聯結，不必包含這個元素。  
  
 您可以使用 **WHERE** 子句來篩選預測查詢的結果。 您可以使用 **TOP** 或 **ORDER by** 子句來選取最有可能的預測。 如需有關使用這些子句的詳細資訊，請參閱 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)。  
  
 如需預測語句語法的詳細資訊，請參閱從 [&#60;模型選取&#62; 預測聯結 &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) ，然後 [從 &#60;模型&#62; &#40;dmx&#41;選取 ](../dmx/select-from-model-dmx.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;DMX&#41; 參考的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [&#40;DMX&#41;的一般預測函數 ](../dmx/general-prediction-functions-dmx.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
