---
title: 測試和驗證 （資料採礦） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- testing data mining models
- comparing mining models
- continuous attribute charts
- data mining [Analysis Services], models
- charts [Analysis Services]
- predictive modeling [Analysis Services]
- mining models [Analysis Services], validating
- validating data mining models
- viewing mining accuracy
- confidence scores [data mining]
- displaying mining accuracy
- predictions [Analysis Services], comparing mining models
- scoring [data mining]
- lift charts [Analysis Services]
- classification matrix [Analysis Services]
- CRISP-DM
- accuracy testing [data mining]
ms.assetid: 197144f5-21ed-4009-b448-fe412fb3916c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 159760722a62969b79ce738e7928739ff2bb15ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082794"
---
# <a name="testing-and-validation-data-mining"></a>測試和驗證 (資料採礦)
  驗證是評估採礦模型對實際資料的執行效能有多好的處理程序。 在部署採礦模型至生產環境之前，先了解其品質和特性以驗證採礦模型是很重要的。  
  
 本章介紹一些與模型品質相關的基本概念，也描述在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中提供的模型驗證策略。 如需模型驗證如何配合較大型資料採礦處理的概觀，請參閱 [資料採礦方案](data-mining-solutions.md)。  
  
## <a name="methods-for-testing-and-validation-of-data-mining-models"></a>測試的方法和資料採礦模型的驗證  
 有多種方法可以評估資料採礦模型的品質和特性。  
  
-   您可以使用各種統計驗證量值來判斷資料或模型中是否有問題。  
  
-   也可以將資料分隔成定型集和測試集以測試預測的精確度。  
  
-   您也可以要求商務專家檢閱資料採礦模型的結果，以判斷找到的模式在目標商務案例中是否具有意義。  
  
 上述所有方法在資料採礦方法中都很有用，可在您建立、測試和精簡模型以解決特定問題時反覆使用。 沒有任何一項規則能完整地可以告訴您模型是否夠好，或是資料是否足夠。  
  
## <a name="definition-of-criteria-for-validating-data-mining-models"></a>驗證資料採礦模型的準則定義  
 資料採礦的量值一般可分為精確度、可靠性和效益等類別目錄。  
  
 *「精確度」* (Accuracy) 是一種量值，代表模型可將結果與所提供資料中的屬性相互關聯的程度。 精確度有多種量值，但所有的精確度量值都是依所使用的資料而定。 事實上，值可能會遺失或僅是近似值，或者資料可能已由多項處理序變更。 特別是在瀏覽和開發階段中，您可能會決定接受資料中特定的錯誤量 (尤其是當資料的特性相當統一時)。 例如，根據過去的銷售量而預測特定店家銷售額的模型，可能會具有強烈的關聯性而且非常正確，即使該店家過去一直使用錯誤的會計方法； 因此，精確度的測量必須藉由可靠性的評估來平衡。  
  
 *「可靠性」* 評估資料採礦模型在不同的資料集上執行的方式。 如果不管所提供的測試資料為何，資料採礦模型都會產生相同的預測類型或找到相同的一般模式類型，則該模型就是可靠的。 例如，您針對使用錯誤會計方法的店家所產生的模型，就無法通用於其他店家，因此並不可靠。  
  
 *「效益」* 包含多種標準，可表示模型是否提供有用的資訊。 例如，將店家地點與銷售額相互關聯的資料採礦模型可能既精確又可靠，但效益卻可能不高，因為無法新增更多位於相同地點的店家來廣泛應用該結果。 此外，該模型也無法回答為何特定地點的銷售額較高的基本商務問題。 您也可能發現看來成功的模型實際上卻沒有意義，因為它是根據資料中的交叉相互關聯而定。  
  
## <a name="tools-for-testing-and-validation-of-mining-models"></a>測試的工具和資料採礦模型的驗證  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援資料採礦方案的多種驗證方法，且這些方法支援資料採礦測試方法的所有階段。  
  
-   將資料分割到定型集和測試集中。  
  
-   篩選模型，以定型和測試相同來源資料的不同組合。  
  
-   測量 *「增益」* (Lift) 和 *「改善」*(Gain)。 *「增益圖」* (Lift chart) 是當您將使用資料採礦模型而獲得的改進與隨機猜測進行比較時，將改進的程度視覺化的方法。  
  
-   執行資料集的「交叉驗證」  
  
-   產生 *「分類矩陣」*(Classification matrices)。 這些圖表可將良好和不正確的猜測排序成資料表，即可快速簡易地量測出模型在預測目標值時精確度。  
  
-   建立 *「散佈圖」* (Scatter plot) 評估迴歸公式的適合度。  
  
-   您可建立 *「收益圖」* (Profit chart)，將財務收益或成本與採礦模型使用方式產生關聯，以便評估建議的值。  
  
 這些度量的目的不是用來回答資料採礦模型是否能解答您的商務疑問，而是提供客觀的測量，以供您評估預測分析資料的可靠性，並引導您判斷開發程序是否需要使用特定的反覆運算。  
  
 本節中的主題提供每一種方法的概觀，並逐步引導您使用 SQL Server 資料採礦所建立之測量模型精確度的程序。  
  
### <a name="related-topics"></a>相關主題  
  
|主題|連結|  
|------------|-----------|  
|了解如何使用精靈或 DMX 命令來設定測試資料集|[定型和測試資料集](training-and-testing-data-sets.md)|  
|了解如何測試採礦結構中資料的散發及代表意義|[交叉驗證 &#40;Analysis Services - 資料採礦&#41;](cross-validation-analysis-services-data-mining.md)|  
|了解 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)]中提供的精確度圖表類型。|[增益圖 &#40;Analysis Services - 資料採礦&#41;](lift-chart-analysis-services-data-mining.md)<br /><br /> [收益圖 &#40;Analysis Services - 資料採礦&#41;](profit-chart-analysis-services-data-mining.md)<br /><br /> [散佈圖 &#40;Analysis Services - 資料採礦&#41;](scatter-plot-analysis-services-data-mining.md)|  
|了解如何建立分類矩陣 (也稱為混淆矩陣) 以評估真肯定、誤判、真否定、誤否定的數量。|[分類矩陣 &#40;Analysis Services - 資料採礦&#41;](classification-matrix-analysis-services-data-mining.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦工具。](data-mining-tools.md)   
 [資料採礦方案](data-mining-solutions.md)   
 [測試及驗證工作與操作方法 &#40;資料採礦&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
  
