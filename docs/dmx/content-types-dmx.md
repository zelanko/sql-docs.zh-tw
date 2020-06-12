---
title: 內容類型（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 30f5496247bb817d4ea7da08f95fe4a1b54dea5d
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669791"
---
# <a name="content-types-dmx"></a>內容類型 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  資料採礦演算法需要資料類型之外的其他資訊才能正確作用，例如內容類型。 內容類型協助演算法決定如何處理資料行中的資料。  
  
 每一種演算法支援特定的內容類型。 例如，[!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類演算法不能使用連續資料行。 若要在 [!INCLUDE[msCoName](../includes/msconame-md.md)] 貝氏機率分類模型中使用連續資料行，就必須分隔資料行中的資料。 有些演算法需要特定內容類型才能正確作用。 例如，[!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法需要索引鍵時間資料行，以識別收集資料的一段時間。  
  
 如需支援之內容類型的完整描述 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ，請參閱[&#40;資料採礦&#41;的內容類型](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services-資料採礦&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [&#40;DMX&#41; 語法元素的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; Operator Reference &#40;的資料採礦延伸模組](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [&#40;DMX&#41;的一般預測函數](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
