---
title: 選擇模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining algorithms
- mining models
- mining structures
- data mining models
- data mining structures
ms.assetid: 444bbf9c-cec8-460e-881d-38784fb146fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd75efa13d6761c058b9e3b1f1878036d3d3e928
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088086"
---
# <a name="choosing-a-model"></a>選擇模型
  **挖掘演算法：** 資料採礦*演算法*是從資料建立模式的機制。 此演算法會定義資料的計算方式、關聯性的衍生方式以及模式的儲存方式。 演算法的選擇部分取決於您想要分析的資料類型。 例如，有些演算法只能搭配連續數字使用，有些演算法則最適合與有限數目的相異值搭配使用。  
  
 [**採礦模型]：** 演算法的資料分析結果會儲存在「*採礦模型*」中。 採礦模型是規則、統計資料和模式的集合。 「採礦模型」的*內容*取決於您用來處理資料的演算法，但可以包含下列各項：  
  
-   If-then 規則，描述交易中的產品如何群組在一起。  
  
-   追蹤導致結果之路徑的決策樹，並包含各種路徑出現的機率。  
  
-   包含適用於整個模型或部分模型之方程式的數學模型。  
  
-   類似專案 *（稱為「* 叢集」或「*區段*」）的集合，由它們所共用的特性和相似性分數所定義。  
  
-   網路中的*節點*，以*邊緣*連接。 這些節點表示項目或項目群組。 邊緣會根據節點間關聯的強度來計分。  
  
 **使用模型：** 建立模型之後，您可以使用提供的檢視器來探索它，也可以針對模型建立查詢。 查詢可用於：  
  
-   預測未來值。  
  
-   產生一組相關的產品或建議的產品。  
  
-   傳回模型中的規則、模式或公式。  
  
-   取得模型中的中繼資料。  
  
-   提供機率並支援所有或部分預測的分數。  
  
## <a name="types-of-machine-learning-algorithms"></a>機器學習演算法的類型  
 由於不同類型的演算法會以不同的方式使用資料，所以當您建立模型時，必須選取適合目標及要分析之資料的演算法。  
  
 適用於 Excel 的資料採礦增益集包括以下廣泛的演算法類型：  
  
-   *分類演算法*。  
  
     根據資料集內的其他屬性，預測一個或多個離散變數。  
  
-   *回歸演算法*  
  
     根據資料集內的其他屬性，預測一個或多個連續變數，例如利潤或損失。  
  
-   *分割演算法*  
  
     將項目的資料劃分為具有相似屬性的群組或叢集。  
  
-   *關聯分析演算法*  
  
     尋找資料集內不同屬性之間的相互關聯。 這種演算法最常用來建立關聯規則。 關聯規則可用於購物籃分析。  
  
-   *時序分析演算法*  
  
     摘要資料的時序或時段，例如使用者在導覽網站時所遵循的路徑。  
  
 適用於 Office 的 SQL Server 資料採礦增益集所使用的演算法是以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的演算法為基礎。 如果您連接的實例[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]已設定為允許協力廠商演算法，則您也可以使用符合資料採礦規格之 OLE DB 的協力廠商演算法。  
  
## <a name="requirements"></a>需求  
 每一種演算法可以處理的資料類型會有所不同。  
  
-   線性迴歸模型只能建立數值模型。 您的輸入變數和目標結果必須是連續的數字類型。 如果您必須混合離散和連續變數，請使用決策樹或估計模型。  
  
-   貝氏機率分類模型需要所有的數字進行分類收納。 如果您使用根據此演算法的其中一個精靈，則會為您自動執行分類收納。  
  
-   決策樹模型可包含離散和連續變數。 不過，視分割樹狀目錄所需，會自動分類收納數字。  
  
-   類神經網路和羅吉斯迴歸模型會自動分類收納作為結果或輸入變數的數字。 如果您想根據其他一些準則群組數字，您應該使用重定標籤工具建立群組，再建立模型。 例如，您可能會想要依十分位數（10-20、21-30 等等）將**年齡**資料行中的值分組，而不是由模型發現的統計重要群組（範例可能是 35.6-41.8 年）。  
  
-   關聯模型需要在交易中分組資料，每個群組會代表數個項目或資料列。 如果您使用 [[關聯] wizard &#40;[適用于 excel 的資料採礦用戶端&#41;](associate-wizard-data-mining-client-for-excel.md) Wizard] 或 [[購物籃分析] &#40;[適用于 excel&#41;工具的資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md) ]，則應該配置資料，如範例活頁簿的 [**關聯**] 索引標籤所示。  
  
     如果您想要使用外部資料源中的嵌套資料表，您必須使用[適用于 Excel 的 Advanced model &#40;資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)模型化選項來建立儲存在伺服器上的「採礦結構」和「採礦模型」。 Excel 不支援巢狀資料表。  
  
## <a name="feature-selection"></a>特徵選取  
 根據資料集而定，此演算法可能會套用*特徵選取*、得費勁篩選不實用的資料行，以及判斷哪些資料行與結果有統計的重要性。  
  
 每一種演算法都會使用稍微不同的特徵選取方法 (例如熵或各種資訊分數)，判斷哪些趨勢是重要的，以及哪些差異可以捨棄。  
  
 在適用於 Excel 的資料採礦增益集中，會使用適用於每個演算法的計分方法，自動套用特徵選取。 如果您想要影響特徵選取的結果，請使用 [**資料採礦**] 功能區中的 [嚮導]，然後按一下 [ **Advanced** ]，使用 [**演算法參數**] 對話方塊來設定參數。  
  
 如需每個演算法所使用的特徵選取方法清單，請參閱 SQL Server 線上叢書中的[功能選取 &#40;資料採礦&#41;](data-mining/feature-selection-data-mining.md)的主題。  
  
## <a name="list-of-supported-algorithms"></a>支援的演算法清單  
 預設會提供下列演算法。  
  
|演算法名稱|描述|使用於|  
|--------------------|-----------------|-------------|  
|Microsoft 關聯規則|建立規則來描述可能一起出現在交易中的項目。|[&#40;適用于 Excel&#41;的資料採礦用戶端相關聯的 Wizard](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [適用于 Excel&#41;的購物籃分析 &#40;資料表 AnalysisTools](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft 群集|識別資料集內的關聯性，這種關聯性可能無法透過偶然的邏輯觀察而衍生。 會使用反覆技巧，將記錄組成包含類似特性的群集。|[偵測適用于 Excel&#41;&#40;資料表分析工具的分類](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [叢集 Wizard &#40;適用于 Excel 的資料採礦增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 決策樹|根據資料集內資料行之間的關聯性做出預測，並將這些關聯性化成特定值上類似樹狀分割序列的模型。<br /><br /> 同時支援離散和連續屬性的預測。|[適用于 Excel 的資料採礦增益集&#41;的分類嚮導 &#40;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [評估 Wizard &#40;適用于 Excel 的資料採礦增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 線性迴歸|如果目標變數與要檢查的變數之間有線性相依性，則會尋找此目標與其輸入之間最有效率的關聯性。<br /><br /> 支援連續屬性的預測。|此演算法可在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用。 在適用於 Office 的資料採礦增益集中，您可以藉由建立結構然後手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱[Advanced 模型化 &#40;適用于 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 羅吉斯迴歸|分析導致結果發生的因數，結果限制為兩個值，通常是事件的發生或不發生。<br /><br /> 同時支援離散和連續屬性的預測。|[&#40;適用于 Excel 的資料表分析工具&#41;的範例填滿](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [&#40;適用于 Excel&#41;的資料表分析工具的目標搜尋案例](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [適用于 Excel 的資料表分析工具 &#40;假設案例&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [預測計算器 &#40;適用于 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft 貝氏機率分類|尋找所有輸入與可預測之資料行之間的關聯性機率。 這個演算法對於快速產生採礦模型來探索關聯性非常實用。<br /><br /> 只支援離散或離散化的屬性。<br /><br /> 會將所有輸入屬性視為獨立。|[&#40;適用于 Excel 的資料表分析工具分析關鍵影響因數&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Microsoft 類神經網路|針對可使用大量定型資料但無法使用其他演算法來輕鬆衍生規則的複雜輸入資料或商業問題加以分析。<br /><br /> 可以預測多個屬性。<br /><br /> 可用來分類離散屬性及連續屬性的迴歸。|此演算法可在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用。 在適用於 Office 的資料採礦增益集中，您可以藉由建立結構然後手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱[Advanced 模型化 &#40;適用于 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 時序群集|識別某個時序中類似排序之事件的群集。<br /><br /> 提供一連串分析和群集的組合。|您只能在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用此演算法。 不過，在適用於 Office 的資料採礦增益集中，您可以藉由建立結構並手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱[Advanced 模型化 &#40;適用于 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。|  
|Microsoft 時間序列|使用線性決策樹，分析與時間相關的資料。<br /><br /> 模式可用來預測時間序列中的未來值。|[適用于 Excel&#41;的預測 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)<br /><br /> [&#40;適用于 Excel 的資料採礦增益集&#41;的預測 Wizard](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Office 的資料採礦增益集包含的內容](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
