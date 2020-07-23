---
title: 模型旗標（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7e05d629f46f1c94bbe9305510daf37c09a39c9b
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969019"
---
# <a name="modeling-flags-dmx"></a>模型旗標 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的模型旗標，為資料採礦演算法提供案例資料表中所定義資料的其他資訊。 演算法可以使用此一資訊建立更精確的資料採礦模型。 您可以在採礦結構資料行與採礦模型資料行上定義模型旗標。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援下列模型旗標：  
  
 **非 Null**  
 屬性資料行的值絕對不能包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在模型培訓處理過程中遇到這個屬性資料行的 Null 值，將會產生錯誤。 這個旗標是在採礦結構資料行定義。  
  
 **回歸輸入變數**  
 指示演算法可以在迴歸演算法的迴歸公式中使用指定的資料行。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 線性迴歸與 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法支援這個旗標，而這個旗標是在採礦模型資料行定義。  
  
 **MODEL_EXISTENCE_ONLY**  
 屬性存在比屬性資料行的值更重要。 這個旗標是在採礦模型資料行定義。  
  
 協力廠商演算法可能支援其他的模型旗標。 若要判斷演算法支援的模型旗標，請使用**SUPPORTED_MODELING_FLAGS**架構資料列集。 您也可以查詢伺服器上的採礦服務，以判斷特定演算法支援的模型旗標。 例如，下列查詢會在目前的伺服器上，傳回 Microsoft 線性迴歸演算法支援的模型旗標：  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 預期的結果：  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>在採礦模型上指定模型旗標  
 如需支援在「 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 採礦結構」資料行上指定旗標的語法範例，請參閱[CREATE &#40;DMX&#41;的「採礦結構](../dmx/create-mining-structure-dmx.md)」。  
  
 如需在「採礦模型」資料行上指定模型 flga 之語法的範例，請參閱[ALTER &#40;DMX&#41;的採礦結構](../dmx/alter-mining-structure-dmx.md)。  
  
 如需使用「採礦模型資料行」的詳細資訊，請參閱「[採礦模型資料行](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns)」。  
  
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
  
  
