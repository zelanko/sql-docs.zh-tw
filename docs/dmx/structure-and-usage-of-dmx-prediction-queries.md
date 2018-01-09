---
title: "結構和使用方式的 DMX 預測查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- prediction joins [DMX]
- empty prediction joins [DMX]
- natural prediction joins [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- queries [DMX], prediction queries
- singleton query predictions [DMX]
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: 098bdaa6-9e7d-4e13-a9aa-eb17ce1750e6
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5f25d8ecd230ca4d2e7aa6a694536e71f5dd0f4e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 預測查詢的結構和使用方式
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，您可以使用預測查詢中的資料採礦延伸模組 (DMX) 來預測新的資料集，根據採礦模型的結果中的未知資料行值。  
  
 您使用的查詢類型依您想要從模型取得的資訊內容而定。 如果您想要即時建立簡單預測，例如知道網站上的潛在客戶是否符合自行車買家的角色，則使用單一查詢。 如果您想要從資料來源中包含的一組案例建立一批預測，則使用一般預測查詢。  
  
## <a name="prediction-types"></a>預測類型  
 您可以使用 DMX 建立下列預測類型：  
  
 預測聯結  
 用於根據採礦模型中存在的模式建立輸入資料的預測。 此查詢陳述式後面必須接著**ON** ，提供採礦模型資料行和輸入資料行之間的聯結子句。  
  
 自然預測聯結  
 用於建立的預測，是以採礦模型中與您所查詢之資料表中的資料行名稱完全相符的資料行名稱為基礎。 此查詢陳述式不需要**ON**子句，因為聯結條件會自動產生根據採礦模型資料行和輸入資料行之間的比對的名稱。  
  
 空白預測聯結  
 用於探索最可能的預測，不必提供輸入資料。 這會傳回只以採礦模型之內容為基礎的預測。  
  
 單一查詢  
 提供資料給查詢以建立預測。 這個陳述式很實用，因為您可以提供單一案例給查詢，快速取得結果。 例如，您可以使用查詢預測身分為女性、35 歲且已婚的某人是否可能採購自行車。 這個查詢不需要外部資料來源。  
  
## <a name="query-structure"></a>查詢結構  
 若要在 DMX 中建立預測查詢，您使用下列元素的組合：  
  
-   **選取 [簡維]**  
  
-   **TOP**  
  
-   **從***\<模型 >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 **選取**預測查詢的項目定義的資料行和運算式將會出現在結果集，並可以包含下列資料：  
  
-   **預測**或**PredictOnly**從採礦模型的資料行。  
  
-   用於建立預測之輸入資料中的任何資料行。  
  
-   傳回資料行的函數。  
  
 **FROM** *\<模型 >* **PREDICTION JOIN**項目會定義要用來建立預測的來源資料。 若是單一查詢，這是指派至資料行的一連串值。 若是空白預測聯結，這會保持空白。  
  
 **ON**元素會對應至外部資料集中的資料行的採礦模型中定義的資料行。 如果是建立空白預測聯結查詢或自然預測聯結，不必包含這個元素。  
  
 您可以使用**其中**子句篩選預測查詢的結果。 您可以使用**頂端**或**ORDER BY**子句選取最可能的預測。 如需有關使用這些子句的詳細資訊，請參閱[SELECT &#40; DMX &#41;](../dmx/select-dmx.md)。  
  
 預測陳述式之語法的詳細資訊，請參閱[SELECT FROM &#60; 模式 &#62;預測聯結 &#40; DMX &#41;](../dmx/select-from-model-prediction-join-dmx.md)和[SELECT FROM &#60; 模型 &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md)。  
  
## <a name="see-also"></a>請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [資料採礦延伸模組 &#40; DMX &#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [一般預測函數 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
