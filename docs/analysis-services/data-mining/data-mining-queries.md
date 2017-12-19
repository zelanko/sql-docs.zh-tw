---
title: "資料採礦查詢 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- prediction queries [Analysis Services]
- queries [DMX], creating
- prediction queries [DMX]
- Prediction Query Builder
- mining models [Analysis Services], querying
ms.assetid: 802806a6-69bb-4c3c-b9aa-d1a1ddfc7fc2
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: f836f060a52db56267cd943c1dea018c9b0732a3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="data-mining-queries"></a>資料採礦查詢
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]資料採礦查詢可以用於許多用途。 您可以：  
  
-   將模型套用到新的資料，以做出單一或多個預測。 您可以在批次中提供輸入值當做參數。  
  
-   取得用於定型的資料統計摘要。  
  
-   擷取模式和規則，或是產生一般案例設定檔來表示模型中的某個模式。  
  
-   擷取迴歸公式及其他說明模式的計算。  
  
-   取得特定模式所適合的案例。  
  
-   擷取模型中所使用之個別案例的詳細資料，包括未用於分析中的資料。  
  
-   透過加入新資料或執行跨預測來重塑模型。  
  
 本節提供您開始使用資料採礦查詢所需的資訊概觀。 它會描述您可以針對資料採礦物件建立的查詢類型、引入查詢工具和查詢語言，並提供您可以針對模型建立之查詢範例的連結，這些模型是之前使用 SQL Server 資料採礦中所提供的演算法所建立。  
  
 [了解資料採礦查詢](#bkmk_Understand)  
  
 [查詢工具和介面](#bkmk_Interfaces)  
  
 [不同模型類型的查詢](#bkmk_ModelTypes)  
  
 [需求](#bkmk_Reqs)  
  
##  <a name="bkmk_Understand"></a> 了解資料採礦查詢  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦支援以下類型的查詢：  
  
-   [預測查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
     根據模型中的模式並從輸入資料進行推斷的查詢。  
  
-   [內容查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)  
  
     傳回中繼資料、統計資料，以及有關模型本身之其他資訊的查詢。  
  
-   [鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
     可以針對模型擷取基礎案例資料，或甚至擷取模型中未使用之結構中之資料的查詢。  
  
-   [資料定義查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/data-definition-queries-data-mining.md)  
  
     不會從模型中傳回資訊，而是用來建立模型和結構，或更新模型或結構中之資料的查詢。  
  
 在建立查詢之前，建議您先熟悉 SQL Server 所提供之每一個資料採礦演算法所建立的模型之間的差異。  
  
-   使用針對每種演算法類型所提供的自訂資料採礦檢視器，瀏覽及探索每一個模型類型。 如需詳細資訊，請參閱[採礦模型檢視器工作和使用說明](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)。  
  
-   使用 Microsoft 一般內容樹狀檢視器來檢閱每一種模型類型的模型內容。 若要解譯此資訊，請參閱 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)。  
  
##  <a name="bkmk_Interfaces"></a> 查詢工具和介面  
 您可以使用 SQL Server 提供的其中一種查詢工具，以互動方式建立資料採礦查詢。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都會提供圖形化預測查詢產生器。 如果您之前未使用過預測查詢產生器，建議您按照＜ [Basic Data Mining Tutorial](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c) ＞中的步驟執行操作來了解介面。 如需步驟的快速概觀，請參閱 [使用預測查詢產生器來建立預測查詢](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)。  
  
 預測查詢產生器對於啟動您之後將要自訂的查詢很有幫助。 您可以輕鬆加入資料來源，並將其對應到資料行，然後切換到 DMX 檢視，並加入 WHERE 子句或其他函數來自訂查詢。  
  
 一旦您熟悉資料採礦模型以及如何建立查詢之後，您也可以使用資料採礦延伸模組 (DMX) 直接撰寫查詢。 DMX 是一種類似於 Transact-SQL 的查詢語言，您可以從許多不同的用戶端來使用它。 DMX 是用來建立自訂預測和複雜查詢的工具選擇。 如需 DMX 的簡介，請參閱[使用 DMX 建立並查詢資料採礦模型：教學課程 &#40;Analysis Services - 資料採礦&#41;](http://msdn.microsoft.com/library/145b81a7-c0c3-4ca3-bb32-0b482423b9a0)。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中都有提供 DMX 編輯器。 您也可以使用預測查詢產生器開始查詢，然後將檢視變更為文字編輯器，並將 DMX 陳述式複製到另一個用戶端。 如需詳細資訊，請參閱 [資料採礦查詢工具](../../analysis-services/data-mining/data-mining-query-tools.md)。  
  
 您可以程式設計方式撰寫 DMX 陳述式，然後使用 AMO 或 XMLA 從用戶端將其傳送到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器。 但是，DMX 是您必須用來針對採礦模型建立查詢的語言。  
  
 您也可以使用根據資料採礦結構描述資料列集的動態管理檢視 (DMV) 來查詢中繼資料、統計資料和部分模型內容。 這些 DMV 可讓您藉由輸入 SELECT 陳述式來輕鬆擷取有關此模型的資訊；但是，您不能建立預測。 如需 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 所支援之 DMV 的詳細資訊，請參閱[使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)。  
  
 最後，您可以使用＜ [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)＞或＜ [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)＞建立資料採礦查詢以供 Integration Services 封裝使用。 此控制流程工作支援多種類型的 DMX 查詢，而資料流程轉換則只支援使用資料流程中之資料的查詢，也就是使用 PREDICTION JOIN 語法的查詢。  
  
##  <a name="bkmk_ModelTypes"></a> 不同模型類型的查詢  
 建立模型時所使用的演算法會大幅影響您可以從資料採礦查詢中取得的資訊類型。 差異的原因是因為每一個演算法都會以不同方式處理資料，並儲存不同種類的模式。 例如，某些演算法會建立叢集，其他演算法則會建立樹狀目錄。 因此，您可能需要使用特殊的預測和查詢函數 (根據您所使用的模型類型而定)。  
  
 下列清單提供您可以在查詢中使用之函數的摘要：  
  
-   **一般預測函數：****Predict** 函數是多型的，這表示它適用於所有模型類型。 這個函數將會自動偵測您所使用之模型的類型，並提示您輸入其他參數。 如需詳細資訊，請參閱 [Predict &#40;DMX&#41](../../dmx/predict-dmx.md)。  
  
    > [!WARNING]  
    >  並非所有模型都會用來做預測。 例如，您可以建立沒有可預測屬性的叢集模型。 但是，即使模型沒有可預測屬性，您也可以建立預測查詢來傳回模型中其他類型的實用資訊。  
  
-   **自訂預測函數：** 每一個模型類型都會提供一組預測函數，這些函數是設計來處理該演算法所建立的模式。  
  
     例如， **Lag** 函數是針對時間序列模型所提供，可讓您檢視模型所使用的歷程記錄資料。 對於叢集模型而言，類似 **ClusterDistance** 的函數更有意義。  
  
     如需有關每一種模型類型所支援之函數的詳細資訊，請參閱以下連結：  
  
    |||  
    |-|-|  
    |[關聯模型查詢範例](../../analysis-services/data-mining/association-model-query-examples.md)|[Microsoft 貝氏機率分類演算法](../../analysis-services/data-mining/microsoft-naive-bayes-algorithm.md)|  
    |[叢集模型查詢範例](../../analysis-services/data-mining/clustering-model-query-examples.md)|[Neural Network Model Query Examples](../../analysis-services/data-mining/neural-network-model-query-examples.md)|  
    |[決策樹模型查詢範例](../../analysis-services/data-mining/decision-trees-model-query-examples.md)|[Sequence Clustering Model Query Examples](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)|  
    |[線性迴歸模型查詢範例](../../analysis-services/data-mining/linear-regression-model-query-examples.md)|[Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md)|  
    |[羅吉斯迴歸模型查詢範例](../../analysis-services/data-mining/logistic-regression-model-query-examples.md)||  
  
     您也可以呼叫 VBA 函數，或是建立您自己的函數。 如需詳細資訊，請參閱[函數 &#40;DMX&#41](../../dmx/functions-dmx.md)。  
  
-   **一般統計資料：**有許多函數幾乎可以搭配任何模型類型使用，以便傳回一組標準的描述性統計資料，例如標準差。  
  
     例如， **PredictHistogram** 函數會傳回一個資料表，列出指定之資料行的所有狀態。  
  
     如需詳細資訊，請參閱[一般預測函數 &#40;DMX&#41](../../dmx/general-prediction-functions-dmx.md)。  
  
-   **自訂統計資料：**為每種模型類型提供其他支援函數，以便產生與特定分析工作有關的統計資料。  
  
     例如，當您使用叢集模型時，您可以使用 **PredictCaseLikelihood**函數傳回與特定案例和叢集相關的可能性分數。 但是，如果您建立了線性迴歸模型，您對於擷取係數和攔截會更感興趣 (您可以使用內容查詢來擷取)。  
  
-   **模型內容函數：**所有模型的「內容」都以標準化格式表示，好讓您使用簡單查詢擷取資訊。 可以使用 DMX 來針對模型內容建立查詢。 您也可以使用資料採礦結構描述資料列集來取得某個類型的模型內容。  
  
     在模型內容中，傳回之資料表的每一個資料列或節點意義會因為用來建立模型的演算法類型以及資料行的資料類型而不同。 如需詳細資訊，請參閱 [內容查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)。  
  
##  <a name="bkmk_Reqs"></a> 需求  
 您必須先處理資料採礦模型，才可以針對模型建立查詢。 處理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件需要特殊權限。 如需有關處理採礦模型的詳細資訊，請參閱[處理需求和考量 &#40;資料採礦&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 若要針對資料採礦模型執行查詢，您需要不同層級的權限 (視您執行的查詢類型而定)。 例如，鑽研至案例或結構資料通常需要額外權限，這些權限可以在採礦結構物件或採礦模型物件上設定。  
  
 但是，如果您的查詢使用外部資料並包含類似 OPENROWSET 或 OPENQUERY 的陳述式，您所查詢的資料庫必須啟用這些陳述式，而且您必須擁有基礎資料庫物件的權限。  
  
 如需有關執行資料採礦查詢所需之安全性內容的詳細資訊，請參閱[安全性概觀 &#40;資料採礦&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="in-this-section"></a>本節內容  
 本節的主題會詳細介紹每一種類型的資料採礦查詢，並提供如何針對資料採礦模型建立查詢之詳細範例的連結。  
  
 [預測查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/prediction-queries-data-mining.md)  
  
 [內容查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)  
  
 [鑽研查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)  
  
 [資料定義查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/data-definition-queries-data-mining.md)  
  
 [資料採礦查詢工具](../../analysis-services/data-mining/data-mining-query-tools.md)  
  
## <a name="related-tasks"></a>相關工作  
 使用這些連結以了解如何建立及使用資料採礦查詢。  
  
|工作|連結|  
|-----------|-----------|  
|檢視有關資料採礦查詢的教學課程和逐步解說|[第 6 課：建立及處理預測 &#40;基本資料採礦教學課程&#41;](http://msdn.microsoft.com/library/b213cb58-2c40-4c89-b08b-d3c36a4afad3)<br /><br /> [時間序列預測 DMX 教學課程](http://msdn.microsoft.com/library/38ea7c03-4754-4e71-896a-f68cc2c98ce2)|  
|使用 SQL Server Management Studio 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|[在 SQL Server Management Studio 中建立 DMX 查詢](../../analysis-services/data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [使用預測查詢產生器來建立預測查詢](../../analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)<br /><br /> [將預測函數套用至模型](../../analysis-services/data-mining/apply-prediction-functions-to-a-model.md)<br /><br /> [手動編輯預測查詢](../../analysis-services/data-mining/manually-edit-a-prediction-query.md)|  
|使用預測查詢中所用的外部資料|[為預測查詢選擇和對應輸入資料](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md)<br /><br /> [為預測查詢選擇和對應輸入資料](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md)|  
|使用查詢的結果|[檢視及儲存預測查詢的結果](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md)|  
|使用 Management Studio 中提供的 DMX 和 XMLA 查詢範本|[根據範本建立單一預測查詢](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)<br /><br /> [使用 XMLA 建立資料採礦查詢](../../analysis-services/data-mining/create-a-data-mining-query-by-using-xmla.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 範本](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|了解內容查詢及參閱範例的詳細資訊|[建立採礦模型內容查詢](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)<br /><br /> [查詢用於建立採礦模型的參數](../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md)<br /><br /> [內容查詢 &#40;資料採礦&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)|  
|設定查詢選項，以及疑難排解查詢權限和問題|[針對資料採礦查詢變更逾時值](../../analysis-services/data-mining/change-the-time-out-value-for-data-mining-queries.md)|  
|在 Integration Services 中使用資料採礦元件|[Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [Data Mining Query Transformation](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|  
  
## <a name="see-also"></a>請參閱  
 [資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [採礦模型內容 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)  
  
  
