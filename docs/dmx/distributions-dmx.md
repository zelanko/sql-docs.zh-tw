---
title: 散發 (DMX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- column distributions [DMX]
- distributions [DMX]
- DMX [Analysis Services], distributions
- Data Mining Extensions [Analysis Services], distributions
ms.assetid: cfbb9f38-ae71-401e-867f-15c6a2b6fb97
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 11f328f7020a22fe5dbf087163bc4b54d2b45e60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="distributions-dmx"></a>散發 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，您可以定義在採礦結構中，以影響您建立採礦模型時演算法如何處理這些資料行中的資料的資料行的內容。 針對某些演算法，若已知資料行包含值的通用散發，則在處理模型前先定義任何連續資料行的散發很有用。 如果您未定義散發，則產生之採礦模型所做出的預測，可能不如定義了散發的預測那般精確，因為演算法能用來解譯資料的資訊比較少。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] 資料採礦演算法支援下列散發類型：  
  
 **標準模式**  
 連續資料行的值形成一般高斯分佈的長條圖。  
  
 **Log Normal**  
 連續資料行的值形成長條圖，其中值的對數為一般分佈。  
  
 **統一**  
 連續資料行的值形成平坦曲線，其中所有值的機率都相當之。  
  
 如需有關[!INCLUDE[msCoName](../includes/msconame-md.md)]資料採礦演算法，請參閱[資料採礦演算法&#40;Analysis Services-資料採礦&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。 協力廠商演算法提供者可能支援其他的散發類型。 若要判斷哪一個發佈類型演算法支援，請使用**SUPPORTED_DISTRIBUTION_FLAGS**結構描述資料列。  
  
 如需有關散發類型的詳細資訊，請參閱[資料行散發&#40;資料採礦&#41;](../analysis-services/data-mining/column-distributions-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 [內容類型 & #40; 資料採礦 & #41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [資料採礦延伸模組 & #40; DMX & #41;參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組&#40;DMX&#41;函數參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組 & #40; DMX & #41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [結構和使用方式的 DMX 預測查詢](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
