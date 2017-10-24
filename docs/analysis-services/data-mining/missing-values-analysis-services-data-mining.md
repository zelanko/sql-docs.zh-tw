---
title: "遺漏值 (Analysis Services-資料採礦) |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attributes [data mining]
- MISSING_VALUE_SUBSTITUTION
- MissingValueSubstitution property
- MISSING_VALUE_SUBSTITUTION parameter
- null values [Analysis Services]
- coding [Data Mining]
ms.assetid: 2b34abdc-7ed4-4ec1-8780-052a704d6dbe
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d71fe57dc5fcd59453d470f92b3dd900d5bde544
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="missing-values-analysis-services---data-mining"></a>遺漏值 (Analysis Services - 資料採礦)
  正確地處理  *「遺漏值」* (Missing value) 是有效模型中很重要的一部分。 本節描述何謂遺漏值，以及您在建立資料採礦結構及採礦模型時，可用來處理遺漏值的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 功能。  
  
## <a name="definition-of-missing-values-in-data-mining"></a>資料採礦中遺漏值的定義  
 遺漏值可能代表許多不同的情況。 可能是欄位不適用、事件未發生或資料無法使用。 輸入資料的人員可能不知道正確的值，或者未注意欄位是否填入。  
  
 不過，在很多資料採礦的案例中，遺漏值會提供很重要的資訊。 遺漏值的意義是絕大多數取決於內容。 例如，遺漏發票明細中的日期值和缺少資料行中的員工雇用日期，兩者意義明顯不同。 一般而言， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將遺漏值視為具有資訊價值，並調整機率以在計算中併入遺漏值。 這麼做可確保模型的平衡，而不會賦予現有的案例過重的加權。  
  
 因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供了兩種截然不同的機制，用於管理和計算遺漏的值。 第一種方法是控制採礦結構層級的空值處理。 第二種方法則依據每個演算法的實作而有所不同，不過通常是定義遺漏值的處理方式以及在模型中允許空值的計算方式。  
  
## <a name="specifying-handling-of-nulls"></a>指定空值的處理  
 在資料來源中，很多情形都代表遺漏值，如：空值、試算表中的空白資料格、N/A 或其他代碼值，或任何假造的值 (如 9999)。 不過基於資料採礦的目的，只會將空值視為遺漏的值。 若您的資料含有預留位置值而非空值，這就可能會影響模型的結果，因此您應該將其取代為空值，或盡可能推斷出正確的值。 有多種工具可用來推斷及填入適當的值，例如 SQL Server Integration Services 中的查閱轉換或資料設定檔工作，或是 Data Mining Add-Ins for Excel 中提供的 Fill By Example 工具。  
  
 若您正在建立模型的工作指出資料行絕對不能有遺漏值，則您在定義採礦結構時，應該在資料行中套用 **NOT_NULL** 模型旗標。 此旗標表示若沒有適當的值時，處理就會失敗。 如果在處理模型時發生此錯誤，您可以記錄錯誤，並採取步驟來修正提供給模型的資料。  
  
## <a name="calculation-of-the-missing-state"></a>遺漏狀態計算  
 對資料採礦演算法而言，遺漏值也具有資訊價值。 在案例資料表中， **Missing** 與其他狀態一樣是有效的狀態； 此外，資料採礦模型也可以使用其他值來預測是否遺漏了值。 換句話說，遺漏值這件事並不等於錯誤。  
  
 當您建立採礦模型時， **Missing** 狀態會自動加入模型以供所有離散資料行使用。 例如，若 [性別] 輸入資料行含有「男」和「女」兩種可能值，則第三個值會自動加入以代表 **Missing** 值，而顯示資料行所有值散發的長條圖一定會包含具有 **Missing** 值的案例計數。 如果「性別」資料行未遺漏任何值，則長條圖會顯示在 0 個案例中找到「遺漏」狀態。  
  
 預設包含 **Missing** 狀態是合乎常理的，因為資料可能並不具備所有可能值的範例，而且您也不想只因為資料中沒有範例而讓模型排除可能的值。 例如，如果某個店家的銷售資料顯示已購買特定產品的所有客戶剛好都是女性，您不會想建立一個模型來預測只有女性可能會購買該產品。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會針對額外未知的值加入預留位置 (稱為 **Missing**)，當作容納其他可能狀態的方式。  
  
 例如，下表顯示針對 Bike Buyer 教學課程所建立的決策樹模型中 (All) 節點的值散發。 在範例案例中，[Bike Buyer] 資料行是可預測的屬性，其中 1 代表「是」，而 0 代表「否」。  
  
|Value|案例|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 此散發顯示大約一半的客戶已購買腳踏車，另一半則沒有。 這個特定資料集非常清楚，因此每個案例在 [Bike Buyer] 資料行中都有一個值，而 **Missing** 值為 0。 不過，如果任何案例在 [Bike Buyer] 欄位中有一個 Null 值，則 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會將該資料行計為具有 **Missing** 值的案例。  
  
 如果輸入是連續的資料行，則模型會將屬性的兩個可能狀態製為表格： **Existing** 和 **Missing**。 換言之，資料行會包含某個數值類型的值或不包含任何值。 對於擁有值的案例，模型會計算平均標準差以及其他有用的統計資料。 對於沒有值的案例，模型則會提供 **Missing** 值的計數並據此調整預測。 調整預測的方法會根據演算法而異，相關說明請見下一章節。  
  
> [!NOTE]  
>  對於巢狀資料表中的屬性而言，遺漏值沒有很高的資訊價值。 例如，如果客戶尚未購買產品，則巢狀的 **Products** 資料表就不會有對應該產品的資料列，採礦模型也不會為遺漏的產品建立屬性。 不過，如果您對尚未購買特定產品的客戶感興趣，可以藉由在模型篩選中使用 NOT EXISTS 陳述式，建立會針對巢狀資料表中不存在的產品進行篩選的模型。 如需詳細資訊，請參閱 [將篩選套用至採礦模型](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
## <a name="adjusting-probability-for-missing-states"></a>調整遺漏狀態的機率  
 除了計算值以外， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也可以計算整個資料集中任何值的機率。 **Missing** 值的情況也是如此。 例如，下列資料表顯示前述範例中案例的機率：  
  
|Value|案例|機率|  
|-----------|-----------|-----------------|  
|0|9296|50.55%|  
|1|9098|49.42%|  
|Missing|0|0.03%|  
  
 當案例數為 0 時， **Missing** 值的機率計算為 0.03% 可能看起來很奇怪。 事實上，這個行為是經過設計的，代表可讓模型正常處理未知值的調整。  
  
 一般而言，機率是由理想案例除以所有可能案例來計算。 在此案例中，演算法會計算符合特定條件 ([Bike Buyer] = 1 或 [Bike Buyer] = 0) 的案例總和，然後將該數目除以資料列的總計。 不過，為了計算 **Missing** 案例，所以會在所有可能案例數中加入 1。 結果是未知案例的機率不再為零，但為很小的數目，代表狀態僅為不太可能，而非不可能。  
  
 加入這個微小的 **Missing** 值並不會變更預測器的結果，但可以為歷程記錄資料不支援所有可能結果的案例建立更好的模型。  
  
> [!NOTE]  
>  資料採礦提供者處理遺漏值的方式各有不同。 例如，某些提供者假設巢狀資料行中的遺漏資料是疏鬆的表示，但非巢狀資料行中的遺漏資料則是隨機遺漏。  
  
 如果您確定資料中已指定了所有結果而想避免調整機率，則應該在採礦結構中的資料行上設定 NOT_NULL 模型旗標。  
  
> [!NOTE]  
>  每種演算法 (包括您從協力廠商外掛程式取得的自訂演算法) 在處理遺漏值的方式上也各不相同。  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>在決策樹模型中對遺漏值的特別處理  
 Microsoft 決策樹演算法計算遺漏值機率的方法與其他演算法不同。 決策樹演算法不是只會在案例總數上加 1，而是會使用有些許不同的公式來調整 **Missing** 狀態。  
  
 在決策樹模型中， **Missing** 狀態的機率計算方式如下：  
  
 StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStates)  
  
決策樹演算法提供額外的調整，以協助演算法補償模型中，可能會導致在定型期間排除許多狀態上的篩選器存在。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，如果某狀態存在於定型期間，但在特定節點中剛好沒有任何支援，則會進行標準調整。 不過，如果在定型期間都沒有遇到某狀態，則演算法會將機率設為剛好為零。 這項調整不只會套用至 **Missing** 狀態，也會套用至存在於定型資料、但因為模型篩選而沒有任何支援的其他狀態。  
  
 這項額外的調整產生下列公式：  
  
 如果狀態在定型集中沒有任何支援，則 StateProbability = 0.0。  
  
 ELSE StateProbability = (NodePriorProbability)* (StateSupport + 1) / (NodeSupport + TotalStatesWithNonZeroSupport)  
  
 這項調整的結果是可以維持樹狀目錄的穩定性。  
  
## <a name="related-tasks"></a>相關工作  
 下列主題提供有關如何處理遺漏值的詳細資訊。  
  
|工作|連結|  
|-----------|-----------|  
|將旗標加入個別模型資料行，以控制遺漏值的處理|[檢視或變更模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|設定採礦模型的屬性以控制遺漏值的處理|[變更採礦模型的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)|  
|了解如何在 DMX 中指定模型旗標|[模型旗標 &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|改變採礦結構處理遺漏值的方式|[變更採礦結構的屬性](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [模型旗標 &#40;資料採礦&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  

