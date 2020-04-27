---
title: 適用于 Excel 的資料採礦用戶端（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Data Mining Client
- wizards
- getting started
ms.assetid: e075e2de-11cc-4f71-9603-0b161bca8a24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c2f11ecbdf90aeeb5e0e5a3ef097152898042d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086424"
---
# <a name="data-mining-client-for-excel-sql-server-data-mining-add-ins"></a>適用於 Excel 的資料採礦用戶端 (SQL Server 資料採礦增益集)
  適用於 Excel 的資料採礦用戶端是可讓您執行一般資料採礦工作 (從資料清理到模型建立與預測查詢) 的一組工具。 您可以使用 Excel 資料表或範圍中的資料，或是存取外部資料來源。  
  
 ![DM](media/dm-tabletools.gif "DM")  
  
-   [使用資料](#bkmk_Data)  
  
     將資料載入 Excel 中、清理資料、檢查極端值，以及建立統計摘要。 您也可以使用外部資料執行不同類型的取樣、分析資料和測試模型。 資料採礦用戶端是準備資料進行分析的最簡單方式，不需使用複雜字集或 ETL 程序。  
  
-   [建立模型和分析](#bkmk_Model)  
  
     這些工具提供廣為人知且經過實證測試的資料採礦演算法的精靈介面，這些演算法包括叢集 (K-means 和 EM)、關聯分析、時間序列分析和決策樹。 每個精靈的進階模型選項可讓您選擇不同的演算法 (例如，貝氏機率分類或類神經網路) 及自訂行為 (例如，群集種子或初始取樣大小)。  
  
     所有資料採礦演算法都裝載在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 的執行個體中，提供您更強大的功能來建立複雜模型。  
  
-   [測試、查詢和驗證模型](#bkmk_Validate)  
  
     資料採礦用戶端提供用來測試模型的業界標準工具，包括增益圖和交叉驗證。 提供的精靈可讓您輕鬆測試資料集的有效性及其精確度。 查詢精靈會建立查詢來使用模型進行預測和計分。  
  
-   [視圖模型](#bkmk_ViewModels)  
  
     大部分工具所產生的圖表都可以直接儲存至 Excel。 使用[Excel 中的流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)工具來探索模型。  
  
-   [管理、文件與部署](#bkmk_UsageMgmt)  
  
     適用於 Excel 的資料採礦用戶端會維護與伺服器之間的使用中連接，好讓您可以將資料採礦模型儲存到伺服器，以供進一步測試使用，或是部署至實際執行伺服器以獲得較大的延展性。  
  
##  <a name="work-with-data"></a><a name="bkmk_Data"></a>使用資料  
 [**資料準備**] 群組包含下列的嚮導，可協助您在準備資料採礦工作時，檢查和清除資料。 此外，大部分的精靈還可以讓您將資料分成定型集和測試集。  
  
 [流覽資料 &#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 針對建立和儲存模型，增益集支援以下這些資料連接：  
  
-    伺服器的連接，用於儲存及處理模型。  
  
-   選用的外部資料來源連接。 您可以使用可定義為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源的任何類型資料來建立模型，或者是直接使用已存在 Excel 中的資料。  
  
 [流覽資料 &#40;SQL Server 資料採礦增益集&#41;](explore-data-sql-server-data-mining-add-ins.md)  
 [**流覽資料**] wizard 可協助您瞭解資料表中的資料類型和數量，方法是以圖表方式繪製所選資料行的分佈和值，一次一個。  
  
 [SQL Server 資料採礦增益集的範例資料 &#40;&#41;](sample-data-sql-server-data-mining-add-ins.md)  
 為定型和測試模型而建立正確類型的資料是資料採礦的一個重要部分，但是如果沒有正確的工具，也是會乏味無趣。 **範例資料**嚮導可讓您輕鬆地將用於模型的資料分割成兩個群組，一個用於建立模型，另一個用於測試它。 您可以使用隨機取樣或超取樣。  
  
 [預測計算器 &#40;適用于 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 [**移除**極端值] wizard 提供數個工具，可供您識別並適當地處理極端值。 它會顯示值的散發以及極端值和其他資料的關聯性，並讓您決定是要移除或變更極端值。  
  
 [預測計算器 &#40;適用于 Excel 的資料表分析工具&#41;](prediction-calculator-table-analysis-tools-for-excel.md)  
 重新**標記**的嚮導可協助您建立資料的新標籤，讓您更容易瞭解分析的結果。 例如，您可以使用更具描述性的名稱來重新命名某個資料範圍，或者可以從清單中選擇代表性的值。  
  
##  <a name="build-models-and-analyze"></a><a name="bkmk_Model"></a>建立模型和分析  
 工具列之 [**資料模型**化] 區段上的選項可讓您從資料衍生模式;根據屬性來群組資料列，或流覽關聯。 此工具功能區中的精靈是根據 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中提供之功能強大的資料採礦演算法。 這些精靈可讓您自訂此演算法的行為及使用各種資料來源，與適用於 Excel 的資料表分析工具中的類似工具不同。  
  
 [適用于 Excel 的資料採礦增益集&#41;的分類嚮導 &#40;](classify-wizard-data-mining-add-ins-for-excel.md)  
 [**分類**] wizard 可協助您根據 excel 資料表、excel 範圍或外部資料源中的現有資料，建立分類模型。 分類模型會擷取可指示資料相似性的模式，並協助您根據值的分組來做出預測。 例如，分類模型可能會用來根據收入或花費模式預測風險。  
  
 [**分類**] wizard 支援使用這些 Microsoft 資料採礦演算法：決策樹演算法、羅吉斯回歸、貝氏機率分類、類神經網路。  
  
 [評估 Wizard &#40;適用于 Excel 的資料採礦增益集&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
 **估計**的 wizard 可協助您建立估計模型。 估計模型會從資料擷取模式，並使用該模式來預測數值結果，例如貨幣、銷售量、日期或時間。  
  
 **估計**wizard 會使用這些 Microsoft 資料採礦演算法：決策樹、線性回歸、羅吉斯回歸和類神經網路。  
  
 [&#40;適用于 Excel 的資料表分析工具分析關鍵影響因數&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 叢集精靈可協助您建立叢集模型。 群集模型會偵測共用類似特性的資料列群組。 這個精靈對於瀏覽所有資料類型中的模式很有協助。  
  
 叢集**嚮導會使用 Microsoft 群集演算法**，其中包含 K 表示和 EM。  
  
 [&#40;適用于 Excel&#41;的資料採礦用戶端相關聯的 Wizard](associate-wizard-data-mining-client-for-excel.md)  
 [**關聯**] wizard 可協助您使用 Microsoft 關聯規則演算法建立資料採礦模型，這會偵測經常發生的共同專案或事件。 這類關聯模型對於提出建議特別有用。  
  
 [**關聯**] 嚮導會使用 Microsoft 關聯規則演算法。  
  
 [&#40;適用于 Excel 的資料採礦增益集&#41;的預測 Wizard](forecast-wizard-data-mining-add-ins-for-excel.md)  
 [**預測**] wizard 可協助您預測時間序列中的值。 通常您在預測中所使用的資料會包含某種時間序列，可能是日期戳記或某種序列識別碼，而您則用它來衍生模式以供預測未來值使用。  
  
 [**預測**] wizard 會使用 Microsoft 時間序列演算法。  
  
 [適用于 Excel&#41;的先進模型化 &#40;資料採礦增益集](advanced-modeling-data-mining-add-ins-for-excel.md)  
 已經很熟悉資料採礦了嗎？ 您可以使用 [ **Advanced** data 模型化] 選項來建立自訂資料結構，並使用其他工具和嚮導中未包含的自訂來建立模型。  
  
##  <a name="test-query-and-validate-models"></a><a name="bkmk_Validate"></a>測試、查詢和驗證模型  
 使用 [**精確度和驗證**] 工具列上的 [嚮導]，即可使用業界標準的測試來驗證模型的正確性，以及評估建立模型之資料集的可用性。  
  
 [&#40;適用于 Excel 的資料表分析工具分析關鍵影響因數&#41;](analyze-key-influencers-table-analysis-tools-for-excel.md)  
 藉由產生增益圖或散佈圖圖表來評估資料採礦模型的效能。  
  
 [SQL Server 資料採礦增益集的分類矩陣 &#40;&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
 藉由建立圖表來摘要列出分類模型所做的正確和不正確的預測，協助您評估此模型的效能。  
  
 [收益圖 &#40;SQL Server 資料採礦增益集&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
 藉由繪製預測的精確度連同根據此預測所採取之動作的成本與優點，協助您了解資料採礦模型的影響。  
  
 [SQL Server 資料採礦增益集的交叉驗證 &#40;&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
 建立一份報表來摘要列出橫跨許多資料集子集之模型的精確度，好讓您可以判斷此模型的穩定度為何。  
  
 您可以使用 Excel 資料表中的資料做為針對伺服器上儲存之採礦模型所發出的預測查詢輸入。  
  
 [查詢 &#40;SQL Server 資料採礦增益集&#41;](query-sql-server-data-mining-add-ins.md)  
 **查詢**嚮導可協助您針對現有的資料採礦模型建立預測。  
  
 [進階資料採礦查詢編輯器](advanced-data-mining-query-editor.md)  
 對於進階使用者，此工具提供了 DMX 的拖放介面。 您可以輕鬆地建立預測查詢或新的模型，而不用擔心語法。  
  
##  <a name="view-models"></a><a name="bkmk_ViewModels"></a>視圖模型  
 您建立的模型會自動開啟進行瀏覽。 不過，您也可以在伺服器上瀏覽模型並產生新的視覺效果。 使用[Visio 圖形](viewing-data-mining-models-in-visio-data-mining-add-ins.md)將模型圖表匯出到可自訂的畫布。  
  
 [在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
 使用針對每一種模型類型所自訂的互動式圖形，檢視您所建立的模型。  
  
 [記載 &#40;適用于 Excel 的資料採礦增益集&#41;的採礦模型](documenting-mining-models-data-mining-add-ins-for-excel.md)  
 此精靈會建立報表，以提供資料集的統計摘要和有關模型的中繼資料，藉此協助調查與解譯。  
  
##  <a name="manage-document-and-deploy"></a><a name="bkmk_UsageMgmt"></a>管理、記載及部署  
 這些工具可協助您連接到資料採礦伺服器、管理和匯出模型，以及監視資料採礦活動。  
  
 [管理 &#40;SQL Server 資料採礦增益集的模型&#41;](manage-models-sql-server-data-mining-add-ins.md)  
 如果您具有必要的權限，您可以刪除、修改、重新命名或處理現有的採礦模型和結構，而不需離開 Excel。  
  
 [適用于 Excel&#41;的追蹤 &#40;資料採礦用戶端](trace-data-mining-client-for-excel.md)  
 按一下 [**追蹤**] 以查看 Excel 用戶端與[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]伺服器之間互動的持續性捕捉。 所有活動都會儲存為 DMX 或 XMLA 陳述式，好讓您可以針對資料採礦工作階段進行疑難排解，或是儲存資訊供日後使用。  
  
 [連接到資料採礦伺服器](connect-to-a-data-mining-server.md)  
 若要將 Excel 當做資料採礦的用戶端使用，您必須建立與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接， 此連接讓您能夠存取 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎。 如果您有權限，此連接也可讓您儲存已發現的任何模式，並修改現有的資料採礦物件。  
  
 [**連接**] 工具列會提供用來管理實例之[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]連接的嚮導。 若要使用資料採礦工具和演算法，您必須定義與 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體的連接。 您可以在安裝增益集時建立連接，或稍後新增連接。  
  
 **快速入門**  
 按一下 [**消費者入門**] 按鈕，啟動設定向導，引導您建立與實例的連接[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，並取得執行資料採礦所需的許可權。  
  
 **說明**  
 [說明] 下拉式功能表提供線上說明、網站和設定**嚮導的連結**，可協助您完成設定並開始進行資料採礦。  
  
 說明頁面也會連結到線上資源，包括增益集的說明以及其他影片、示範和範例。  
  
## <a name="see-also"></a>另請參閱  
 [適用于 Excel 的資料表分析工具](table-analysis-tools-for-excel.md)   
 [針對 Visio 資料採礦圖表進行疑難排解 &#40;SQL Server 資料採礦增益集&#41;](troubleshooting-visio-data-mining-diagrams-sql-server-data-mining-add-ins.md)  
  
  
