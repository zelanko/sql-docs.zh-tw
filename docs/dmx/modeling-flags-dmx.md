---
title: 模型旗標 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17280abc62cd75122fde1f54b321ca9b51a1b1d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62502887"
---
# <a name="modeling-flags-dmx"></a>模型旗標 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  您可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的模型旗標，為資料採礦演算法提供案例資料表中所定義資料的其他資訊。 演算法可以使用此一資訊建立更精確的資料採礦模型。 您可以在採礦結構資料行與採礦模型資料行上定義模型旗標。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援下列模型旗標：  
  
 **NOT NULL**  
 屬性資料行的值絕對不能包含 Null 值。 如果 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在模型培訓處理過程中遇到這個屬性資料行的 Null 值，將會產生錯誤。 這個旗標是在採礦結構資料行定義。  
  
 **REGRESSOR**  
 指示演算法可以在迴歸演算法的迴歸公式中使用指定的資料行。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 線性迴歸與 [!INCLUDE[msCoName](../includes/msconame-md.md)] 決策樹演算法支援這個旗標，而這個旗標是在採礦模型資料行定義。  
  
 **MODEL_EXISTENCE_ONLY**  
 屬性存在比屬性資料行的值更重要。 這個旗標是在採礦模型資料行定義。  
  
 協力廠商演算法可能支援其他的模型旗標。 若要判斷哪些模型旗標的演算法支援，請使用**SUPPORTED_MODELING_FLAGS**結構描述資料列。 您也可以查詢伺服器上的採礦服務，以判斷特定演算法支援的模型旗標。 例如，下列查詢會在目前的伺服器上，傳回 Microsoft 線性迴歸演算法支援的模型旗標：  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 預期的結果：  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>在採礦模型上指定模型旗標  
 如需語法的範例可[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]支援的指定旗標，採礦結構資料行，請參閱[CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)。  
  
 如需採礦模型資料行上指定模型旗標的語法的範例，請參閱 < [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)。  
  
 如需有關使用採礦模型資料行的詳細資訊，請參閱[採礦模型資料行](../analysis-services/data-mining/mining-model-columns.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](../dmx/data-mining-extensions-dmx-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [資料採礦延伸模組&#40;DMX&#41;函式參考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;運算子參考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [資料採礦延伸模組&#40;DMX&#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [資料採礦延伸模組&#40;DMX&#41;語法慣例](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [一般預測函數&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [DMX 預測查詢的結構和使用方式](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 陳述式](../dmx/understanding-the-dmx-select-statement.md)  
  
  
