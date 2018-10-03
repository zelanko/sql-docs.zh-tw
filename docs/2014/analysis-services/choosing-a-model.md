---
title: 選擇模型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 4cbde25ffc504e2e2c41bcf6b46cde9d464daa7d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113288"
---
# <a name="choosing-a-model"></a>選擇模型
  **採礦演算法：** 資料採礦*演算法*是從資料建立模式的機制。 此演算法會定義資料的計算方式、關聯性的衍生方式以及模式的儲存方式。 演算法的選擇部分取決於您想要分析的資料類型。 例如，有些演算法只能搭配連續數字使用，有些演算法則最適合與有限數目的相異值搭配使用。  
  
 **採礦模型：** 演算法的資料分析的結果會儲存在*採礦模型*。 採礦模型是規則、統計資料和模式的集合。 *內容*採礦模型的演算法而異，用來處理資料，但可以包含下列項目：  
  
-   If-then 規則，描述交易中的產品如何群組在一起。  
  
-   追蹤導致結果之路徑的決策樹，並包含各種路徑出現的機率。  
  
-   包含適用於整個模型或部分模型之方程式的數學模型。  
  
-   相似項目的集合 (稱為*叢集*或是*區段*) 所定義的特性，兩者共用，以及相似度分數。  
  
-   *節點*在網路中，以連接*邊緣*。 這些節點表示項目或項目群組。 邊緣會根據節點間關聯的強度來計分。  
  
 **使用模型：** 之後建立的模型，您可以使用提供的檢視器來探索它，或是您可以針對模型建立查詢。 查詢可用於：  
  
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
  
-   *迴歸演算法*  
  
     根據資料集內的其他屬性，預測一個或多個連續變數，例如利潤或損失。  
  
-   *分割演算法*  
  
     將項目的資料劃分為具有相似屬性的群組或叢集。  
  
-   *關聯分析演算法*  
  
     尋找資料集內不同屬性之間的相互關聯。 這種演算法最常用來建立關聯規則。 關聯規則可用於購物籃分析。  
  
-   *時序分析演算法*  
  
     摘要資料的時序或時段，例如使用者在導覽網站時所遵循的路徑。  
  
 適用於 Office 的 SQL Server 資料採礦增益集所使用的演算法是以 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供的演算法為基礎。 您也可以使用符合 OLE DB for Data Mining 規格的協力廠商演算法，如果執行個體[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]您所連接之已設定為允許協力廠商演算法。  
  
## <a name="requirements"></a>需求  
 每一種演算法可以處理的資料類型會有所不同。  
  
-   線性迴歸模型只能建立數值模型。 您的輸入變數和目標結果必須是連續的數字類型。 如果您必須混合離散和連續變數，請使用決策樹或估計模型。  
  
-   貝氏機率分類模型需要所有的數字進行分類收納。 如果您使用根據此演算法的其中一個精靈，則會為您自動執行分類收納。  
  
-   決策樹模型可包含離散和連續變數。 不過，視分割樹狀目錄所需，會自動分類收納數字。  
  
-   類神經網路和羅吉斯迴歸模型會自動分類收納作為結果或輸入變數的數字。 如果您想根據其他一些準則群組數字，您應該使用重定標籤工具建立群組，再建立模型。 例如，您可能想要群組中的值**年齡**依十分位數 （10-20、 21-30，所以上），資料行，而不是統計上明顯 （範例可能是 35.6-41.8 年） 的模型找到的群組。  
  
-   關聯模型需要在交易中分組資料，每個群組會代表數個項目或資料列。 如果您使用[關聯精靈&#40;適用於 Excel 的資料採礦用戶端&#41;](associate-wizard-data-mining-client-for-excel.md)精靈 或[購物籃分析&#40;適用於 Excel 的資料表 AnalysisTools&#41; ](shopping-basket-analysis-table-analysistools-for-excel.md)工具，資料應該配置中所示**產生關聯**範例活頁簿索引標籤。  
  
     如果您想要使用外部資料來源中的巢狀的資料表，您必須使用[進階模型化&#40;資料採礦增益集適用於 Excel&#41; ](advanced-modeling-data-mining-add-ins-for-excel.md)模型來建立採礦結構和採礦模型儲存在伺服器上的選項。 Excel 不支援巢狀資料表。  
  
## <a name="feature-selection"></a>特徵選取  
 根據資料集，演算法可能會套用*特徵選取*濾除不適用，資料行，以判斷統計上明顯有關結果的資料行。  
  
 每一種演算法都會使用稍微不同的特徵選取方法 (例如熵或各種資訊分數)，判斷哪些趨勢是重要的，以及哪些差異可以捨棄。  
  
 在適用於 Excel 的資料採礦增益集中，會使用適用於每個演算法的計分方法，自動套用特徵選取。 如果您想影響特徵選取的結果，使用中的精靈**資料採礦**功能區，然後按一下**進階**若要設定使用的參數**演算法參數** 對話方塊。  
  
 如需清單，特徵選取的每個演算法所用的方法，請參閱上的主題[特徵選取&#40;資料採礦&#41;](data-mining/feature-selection-data-mining.md) SQL Server 線上叢書 》 中。  
  
## <a name="list-of-supported-algorithms"></a>支援的演算法清單  
 預設會提供下列演算法。  
  
|演算法名稱|描述|使用於|  
|--------------------|-----------------|-------------|  
|Microsoft 關聯規則|建立規則來描述可能一起出現在交易中的項目。|[關聯精靈&#40;適用於 Excel 的資料採礦用戶端&#41;](associate-wizard-data-mining-client-for-excel.md)<br /><br /> [購物籃分析&#40;AnalysisTools 適用於 Excel 的資料表&#41;](shopping-basket-analysis-table-analysistools-for-excel.md)|  
|Microsoft 群集|識別資料集內的關聯性，這種關聯性可能無法透過偶然的邏輯觀察而衍生。 會使用反覆技巧，將記錄組成包含類似特性的群集。|[偵測類別目錄&#40;適用於 Excel 的資料表分析工具&#41;](detect-categories-table-analysis-tools-for-excel.md)<br /><br /> [叢集精靈&#40;資料採礦適用於 Excel 的增益集&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 決策樹|根據資料集內資料行之間的關聯性做出預測，並將這些關聯性化成特定值上類似樹狀分割序列的模型。<br /><br /> 同時支援離散和連續屬性的預測。|[分類精靈&#40;資料採礦適用於 Excel 的增益集&#41;](classify-wizard-data-mining-add-ins-for-excel.md)<br /><br /> [估計精靈&#40;資料採礦適用於 Excel 的增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)|  
|Microsoft 線性迴歸|如果目標變數與要檢查的變數之間有線性相依性，則會尋找此目標與其輸入之間最有效率的關聯性。<br /><br /> 支援連續屬性的預測。|此演算法可在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用。 在適用於 Office 的資料採礦增益集中，您可以藉由建立結構然後手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 進階模型化&#40;適用於 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。</c0>|  
|Microsoft 羅吉斯迴歸|分析導致結果發生的因數，結果限制為兩個值，通常是事件的發生或不發生。<br /><br /> 同時支援離散和連續屬性的預測。|[根據範例填滿&#40;適用於 Excel 的資料表分析工具&#41;](fill-from-example-table-analysis-tools-for-excel.md)<br /><br /> [搜尋目標狀況&#40;適用於 Excel 的資料表分析工具&#41;](goal-seek-scenario-table-analysis-tools-for-excel.md)<br /><br /> [假設狀況&#40;適用於 Excel 的資料表分析工具&#41;](what-if-scenario-table-analysis-tools-for-excel.md)<br /><br /> [預測計算器&#40;適用於 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)|  
|Microsoft 貝氏機率分類|尋找所有輸入與可預測之資料行之間的關聯性機率。 這個演算法對於快速產生採礦模型來探索關聯性非常實用。<br /><br /> 只支援離散或離散化的屬性。<br /><br /> 會將所有輸入屬性視為獨立。|[分析關鍵影響因數&#40;適用於 Excel 的資料表分析工具&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)|  
|Microsoft 類神經網路|針對可使用大量定型資料但無法使用其他演算法來輕鬆衍生規則的複雜輸入資料或商業問題加以分析。<br /><br /> 可以預測多個屬性。<br /><br /> 可用來分類離散屬性及連續屬性的迴歸。|此演算法可在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用。 在適用於 Office 的資料採礦增益集中，您可以藉由建立結構然後手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 進階模型化&#40;適用於 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。</c0>|  
|Microsoft 時序群集|識別某個時序中類似排序之事件的群集。<br /><br /> 提供一連串分析和群集的組合。|您只能在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中使用此演算法。 不過，在適用於 Office 的資料採礦增益集中，您可以藉由建立結構並手動加入模型，以建立使用此演算法的模型。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 進階模型化&#40;適用於 Excel 的資料採礦增益集&#41;](advanced-modeling-data-mining-add-ins-for-excel.md)。</c0>|  
|Microsoft 時間序列|使用線性決策樹，分析與時間相關的資料。<br /><br /> 模式可用來預測時間序列中的未來值。|[預測&#40;適用於 Excel 的資料表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)<br /><br /> [預測精靈&#40;資料採礦適用於 Excel 的增益集&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)|  
  
## <a name="see-also"></a>另請參閱  
 [適用於 Office 的資料採礦增益集包含的內容](what-s-included-in-the-data-mining-add-ins-for-office.md)  
  
  
