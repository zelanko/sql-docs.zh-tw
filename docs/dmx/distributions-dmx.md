---
title: 散發（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: fda2eb169985eb670614f611764fbf149c71a42d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892796"
---
# <a name="distributions-dmx"></a>散發 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中，您可以在採礦結構中定義資料行的內容，以影響當您建立採礦模型時，演算法如何處理這些資料行中的資料。 針對某些演算法，若已知資料行包含值的通用散發，則在處理模型前先定義任何連續資料行的散發很有用。 如果您未定義散發，則產生之採礦模型所做出的預測，可能不如定義了散發的預測那般精確，因為演算法能用來解譯資料的資訊比較少。  
  
 
  [!INCLUDE[msCoName](../includes/msconame-md.md)] 資料採礦演算法支援下列散發類型：  
  
 **一般**  
 連續資料行的值形成一般高斯分佈的長條圖。  
  
 **Log Normal**  
 連續資料行的值形成長條圖，其中值的對數為一般分佈。  
  
 **統一性**  
 連續資料行的值形成平坦曲線，其中所有值的機率都相當之。  
  
 如需有關[!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦演算法的詳細資訊，請參閱[資料採礦演算法 &#40;Analysis Services 資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)。 協力廠商演算法提供者可能支援其他的散發類型。 若要判斷演算法支援哪些散發類型，請使用**SUPPORTED_DISTRIBUTION_FLAGS**架構資料列集。  
  
 如需有關散發類型的詳細資訊，請參閱[資料採礦&#41;的資料行散發 &#40;](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;資料採礦&#41;的內容類型](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
