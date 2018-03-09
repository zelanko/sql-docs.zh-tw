---
title: "資料採礦專案 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 543d70fc-34d2-42dd-8d6d-0543109f94d0
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f545d90cd695eef78f4ae8b33eef7f2f32e9439f
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/23/2018
---
# <a name="data-mining-projects"></a>資料採礦專案
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
資料採礦專案為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 方案的一部分。 在設計過程中，您在此專案中建立的物件可當做工作空間資料庫的一部分來測試及查詢。 當您希望使用者能夠查詢或瀏覽專案中的物件時，您必須將此專案部署到以多維度模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。  
  
 本主題為您提供理解及建立資料採礦專案所需的基本資訊。  
  
 [建立資料採礦專案](#bkmk_Overview)  
  
 [資料採礦專案中的物件](#bkmk_Objects)  
  
-   [資料來源](#bkmk_DataSources)  
  
-   [資料來源檢視](#bkmk_DSV)  
  
-   [採礦結構](#bkmk_Structures)  
  
-   [採礦模型](#bkmk_Models)  
  
 [使用完成的資料採礦專案](#bkmk_Complete)  
  
-   [檢視及瀏覽模型](#bkmk_ViewExplore)  
  
-   [測試和驗證模型](#bkmk_Validate)  
  
-   [建立預測](#bkmk_Predict)  
  
 [以程式設計方式存取資料採礦專案](#bkmk_API)  
  
##  <a name="bkmk_Overview"></a> 建立資料採礦專案  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，您會使用 [OLAP 和資料採礦專案] 範本建立資料採礦專案。 您也可以使用 AMO 來以程式設計的方式建立資料採礦專案。 個別資料採礦物件則可以使用 Analysis Services 指令碼語言 (ASSL) 來編寫指令碼。 如需詳細資訊，請參閱[多維度模型資料存取 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)。  
  
 如果您在現有方案中建立資料採礦專案，預設會將資料採礦物件部署到與方案檔同名的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中。 您可以使用 [專案屬性] 對話方塊來變更這個名稱和目標伺服器。 如需詳細資訊，請參閱[設定 Analysis Services 專案屬性 &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)。  
  
> [!WARNING]  
>  若要成功建立及部署專案，您必須能夠存取以 OLAP/資料採礦模式執行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體。 您不能在支援表格式模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體上開發或部署資料採礦方案，也不能直接使用來自 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 活頁簿或使用記憶體中資料存放區之表格式模型中的資料。 若要判斷您具有的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體是否可以支援資料採礦，請參閱 [判斷 Analysis Services 執行個體的伺服器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)。  
  
 在您建立的每一個資料採礦專案中，您將遵循以下步驟進行：  
  
1.  選擇「資料來源」，例如 Cube、資料庫或甚至是 Excel 或文字檔案，其中包含您將用於建立模型的原始資料。  
  
2.  在資料來源中定義用於分析的資料子集，並將其儲存為「資料來源檢視」。  
  
3.  定義「採礦結構」來支援模型化。  
  
4.  將「採礦模型」加入至採礦結構，方法是選擇「演算法」及指定演算法將如何處理資料。  
  
5.  在模型中填入選取的資料或是經過篩選的資料子集來定型模型。  
  
6.  瀏覽、測試和重建模型。  
  
 當專案完成之後，您可以部署專案以供使用者瀏覽或查詢，或是提供應用程式中採礦模型的程式設計方式存取，以支援預測和分析。  
  
  
##  <a name="bkmk_Objects"></a> 資料採礦專案中的物件  
 所有資料採礦專案都包含以下四種類型的物件。 您可以擁有所有類型的多個物件。  
  
-   資料來源  
  
-   資料來源檢視  
  
-   採礦結構  
  
-   採礦模型  
  
 例如，單一資料採礦專案可包含多個資料來源的參考，其中每一個資料來源都支援多個資料來源檢視。 而每一個資料來源檢視可以支援多個採礦結構，每一個採礦結構則有多個相關的採礦模型。  
  
 此外，您的專案可能會包含外掛程式演算法、自訂組件或自訂預存程序，但是這裡不會描述這些物件。 如需詳細資訊，請參閱 [開發人員指南 (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md)。  
  
  
###  <a name="bkmk_DataSources"></a> Data Sources  
 資料來源會定義 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 伺服器用來連接到資料來源的連接字串和驗證資訊。 資料來源可以包含多個資料表或檢視表，它可以像是單一 Excel 活頁簿或文字檔一樣簡單，或者像是線上分析處理 (OLAP) 資料庫或大型關聯式資料庫一樣複雜。  
  
 單一資料採礦專案可以參考多個資料來源。 雖然採礦模型一次只能使用一個資料來源，但是專案可以有多個模型在不同的資料來源上繪製。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支援許多外部提供者的資料，而且 SQL Server 資料採礦可以同時使用關聯式資料和 Cube 資料當做資料來源。 但是，如果您開發這兩種類型的專案 (以關聯式來源為根據的模型和以 OLAP Cube 為根據的模型)，您可能會想要在不同的專案中開發及管理這些項目。  
  
-   通常以 OLAP Cube 為根據的模型應該在 OLAP 設計方案內開發。 其中一個原因是因為以 Cube 為根據的模型必須處理此 Cube 才能更新資料。 一般來說，只有當 Cube 資料是資料儲存和存取的主要方式，或者您需要多維度專案所建立的彙總、維度和屬性時，才應該使用 Cube 資料。  
  
-   如果您的專案只使用關聯式資料，您應該在個別的專案內建立關聯式模型，好讓您只有在必要時才會重新處理其他物件。 在許多情況下，用來支援 Cube 建立的暫存資料庫或資料倉儲已經包含執行資料採礦所需的檢視表，而且您可以將這些檢視表用於資料採礦，而不需使用 Cube 中的彙總和維度。  
  
-   您不能直接使用記憶體中或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 資料來建立資料採礦模型。  
  
 資料來源只會識別伺服器或提供者及一般類型的資料。 如果您需要變更資料格式和彙總，請使用資料來源檢視物件。  
  
 若要控制處理資料來源中之資料的方式，您可以加入衍生的資料行或計算、修改彙總，或是重新命名資料來源檢視中的資料行 (您也可以處理下游資料，方法是修改採礦結構資料行，或是在採礦模型資料行層級使用模型旗標和篩選)。  
  
 如果需要清理資料，或者資料倉儲中的資料必須加以修改才能建立其他變數、變更資料類型或建立替代彙總，您可能需要建立其他專案類型來支援資料採礦。 如需這些相關專案的詳細資訊，請參閱 [資料採礦方案的相關專案](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)。  
  
  
###  <a name="bkmk_DSV"></a> Data Source Views  
 當您已經定義資料來源的這個連接之後，可以建立一個檢視表，以識別與模型相關的特定資料。  
  
 資料來源檢視也會讓您自訂將資料來源中的資料提供給採礦模型的方式。 您可以修改資料結構，使它與您的專案關係更加密切，或僅選擇特定種類的資料。  
  
 例如，您可以使用「資料來源檢視」編輯器進行以下作業：  
  
-   建立衍生的資料行，例如日期部分、子字串等。  
  
-   使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (例如 GROUP BY) 來彙總值  
  
-   暫時限制資料或取樣資料  
  
 如需如何修改資料來源檢視內之資料的詳細資訊，請參閱 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
> [!WARNING]  
>  如果您要篩選資料，您可以在資料來源檢視中進行，但是也可以在採礦模型層級建立資料的篩選。 因為篩選定義儲存在採礦模型中，所以使用模型篩選器會更容易判斷之前用來定型模型的資料。 此外，您也可以使用不同的篩選準則建立多個相關模型。 如需詳細資訊，請參閱[採礦模型的篩選 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)。  
  
 請注意，您建立的資料來源檢視可以包含未直接用於分析的其他資料。 例如，您可能會將用於測試、預測或鑽研的資料加入至資料來源檢視。 如需這些用途的詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md) 和[鑽研](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
  
###  <a name="bkmk_Structures"></a> Mining Structures  
 一旦您建立資料來源和資料來源檢視之後，您必須在專案內定義「採礦結構」(Mining Structure) 來選取與您的商務問題最密切相關的資料行。 採礦結構會告知專案，資料來源檢視中的哪些資料行實際上應該用於模型化、定型和測試。  
  
 若要加入新的採礦結構，請啟動資料採礦精靈。 此精靈會自動定義採礦結構、帶領您進行選擇資料的程序，並可選擇性地讓您將初始採礦模型加入至結構中。 在採礦結構內，您會從資料來源檢視或 OLAP Cube 中選擇資料表和資料行，然後定義資料表之間的關聯性 (如果您的資料包含巢狀資料表)。  
  
 您所選擇的資料在資料採礦精靈中會有非常不同的面貌，這取決於您使用關聯式資料來源或線上分析處理 (OLAP) 資料來源而定。  
  
-   當您從關聯式資料來源中選擇資料時，設定採礦結構會非常簡單：從資料來源檢視中選擇資料行，並設定其他自訂內容 (例如別名)，或是定義資料行中的值應該如何群組或分類收納。 如需詳細資訊，請參閱 [建立關聯式採礦結構](../../analysis-services/data-mining/create-a-relational-mining-structure.md)。  
  
-   當您使用 OLAP Cube 中的資料時，採礦結構必須在與 OLAP 方案相同的資料庫中。  若要建立採礦結構，您會從 OLAP 方案的維度和相關量值中選取屬性。 數值通常會在量值中，而類別變數則會在維度中。 如需詳細資訊，請參閱 [建立 OLAP 採礦結構](../../analysis-services/data-mining/create-an-olap-mining-structure.md)。  
  
-   您也可以使用 DMX 來定義採礦結構。 如需詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 資料定義陳述式](../../dmx/dmx-statements-data-definition.md)。  
  
 在您建立初始採礦結構之後，您可以複製和修改結構資料行，並為結構資料行建立別名。  
  
 每一個採礦結構都可以包含多個採礦模型。 因此，一旦您完成之後，您可以再次開啟採礦結構，並使用 [Data Mining Designer](../../analysis-services/data-mining/data-mining-designer.md) 將其他採礦模型加入至結構中。  
  
 您也可以選擇將資料分成定型資料集 (用於建立模型) 和鑑效組資料集 (用於測試或驗證您的採礦模型)。  
  
> [!WARNING]  
>  某些模型類型 (例如時間序列模型) 不支援建立鑑效組資料集，因為這些類型需要用於定型的連續資料數列。 如需詳細資訊，請參閱 [Training and Testing Data Sets](../../analysis-services/data-mining/training-and-testing-data-sets.md)。  
  
  
###  <a name="bkmk_Models"></a> Mining Models  
 採礦模型會定義演算法或您將在資料上使用的分析方法。 您可以將一個或多個採礦模型加入至每個採礦結構。  
  
 根據您的需求而定，您可以將許多模型結合成單一專案，或是針對每個類型的模型或分析工作建立個別的專案。  
  
 在您建立結構和模型之後，您可以透過產生資料之數學模型的演算法，執行資料來源檢視中的資料來「處理」每個模型。 此程序也就是所謂的「定型模型」。 如需詳細資訊，請參閱[處理需求和考量 &#40;資料採礦&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)。  
  
 模型經過處理之後，您可以使用視覺的方式瀏覽採礦模型，並據此建立預測查詢。 如果已經快取定型程序中的資料，您可以使用「鑽研」查詢，傳回有關在模型中使用之案例的詳細資訊。  
  
 當您想要在實際用途中使用模型時 (例如，用來進行預測或是依一般使用者瀏覽)，您可以將模型部署至另一部伺服器。 如果您將來需要重新處理模型，您也必須同時匯出基礎採礦結構的定義 (同時也必須匯出資料來源和資料來源檢視的定義)。  
  
 當您部署模型時，您也必須確保正確的處理選項會在結構和模型上設定，而且潛在使用者擁有執行查詢、檢視模型或鑽研至結構或模型資料所需的權限。 如需詳細資訊，請參閱[安全性概觀 &#40;資料採礦&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)。  
  
  
##  <a name="bkmk_Complete"></a> 使用完成的資料採礦專案  
 本章節摘要列出您可以使用完成之資料採礦專案的方式。 您可以建立精確度圖表、瀏覽和驗證資料，並將資料採礦模式提供給使用者使用。  
  
> [!WARNING]  
>  您搭配資料採礦模型使用的圖表、查詢和視覺效果不會儲存為資料採礦專案的一部分，而且也無法部署。 如果您需要保存這些物件，您必須儲存所呈現的內容或是為其撰寫指令碼 (如每個物件所述內容來處理)。  
  
  
###  <a name="bkmk_ViewExplore"></a> View and Explore Models  
 在您建立模型之後，您可以使用視覺工具和查詢來探索模型中的模式，並深入了解基礎模式和統計資料。 在資料採礦設計師的 [採礦模型檢視器] 索引標籤中，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會提供每個採礦模型類型的檢視器，您可以使用這些檢視器來瀏覽採礦模型。  
  
 這些視覺效果是暫時性的，而且當您結束 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的工作階段時會關閉而不儲存。 因此，如果您需要將這些視覺效果匯出到另一個應用程式或簡報或是進行進一步分析，請使用檢視器介面上每一個索引標籤或窗格中提供的 [複製] 命令。  
  
 適用於 Excel 的資料採礦增益集也提供一個 Visio 範本，您可用來在 Visio 圖表中呈現您的模型，並使用 Visio 工具為圖表加上註解和修改圖表。 如需詳細資訊，請參閱 [Microsoft Office 2007 適用之 Microsoft SQL Server 2008 SP2 資料採礦增益集](http://go.microsoft.com/fwlink/?LinkID=123146)。  
  
  
###  <a name="bkmk_Validate"></a> Test and Validate Models  
 建立模型後，您可以調查結果，並判定效能最佳的模型。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供幾個圖表，您可使用這些圖表來提供可用於直接比較採礦模型，並選擇最精確或最實用之採礦模型的工具。 這些工具包括增益圖、收益圖表和分類矩陣。 您可以使用資料採礦設計師的 [採礦精確度圖表] 索引標籤來產生這些圖表。  
  
 您也可以使用交叉驗證報表執行資料的反覆次取樣，以判斷模型是否偏差為特定的資料集。 報表提供的統計資料可以用客觀的方式比較模型，並評估定型資料的品質。  
  
 請注意，這些報表和圖表不會與專案一起儲存或儲存在 ssASnoversion 資料庫中，所以如果您需要保留或複製結果，您應該儲存結果，或是使用 DMX 或 AMO 來撰寫物件的指令碼。 您也可以使用預存程序進行交叉驗證。  
  
 如需詳細資訊，請參閱[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)。  
  
  
###  <a name="bkmk_Predict"></a> Create Predictions  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供一種稱為資料採礦延伸模組 (DMX) 的查詢語言，這種語言是建立預測的基礎而且非常容易撰寫指令碼。 為了幫助您建立 DMX 預測查詢， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會提供可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用的查詢產生器。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的查詢編輯器也有許多 DMX 範本。如果您是預測查詢的新手，我們建議您最好使用資料採礦設計師和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]兩者中所提供的查詢產生器。 如需詳細資訊，請參閱 [Data Mining Tools](../../analysis-services/data-mining/data-mining-tools.md)。  
  
 您在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中所建立的預測不會保存下來，所以如果您的查詢很複雜或者您需要重新產生結果，我們建議您最好將預測查詢儲存至 DMX 查詢檔案、為其編寫指令碼，或是在 Integration Services 封裝中內嵌查詢。  
  
  
##  <a name="bkmk_API"></a> 以程式設計方式存取資料採礦物件  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供數個工具，讓您以程式設計的方式來使用資料採礦專案和專案中的物件。 DMX 語言提供的陳述式可讓您用來建立資料來源和資料來源檢視，以及建立、定型和使用資料採礦結構和模型。 如需詳細資訊，請參閱[資料採礦延伸模組 &#40;DMX&#41; 參考](../../dmx/data-mining-extensions-dmx-reference.md)。  
  
 您也可以使用 Analysis Services 指令碼語言 (ASSL) 或使用分析管理物件 (AMO) 來執行這些工作。 如需詳細資訊，請參閱 [在 Analysis Services 中使用 XMLA 進行開發](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)。  
  
  
## <a name="related-tasks"></a>相關工作  
 下列主題描述如何使用資料採礦精靈來建立資料採礦專案和關聯的物件。  
  
|工作|主題|  
|-----------|------------|  
|描述如何處理採礦結構資料行|[建立關聯式採礦結構](../../analysis-services/data-mining/create-a-relational-mining-structure.md)|  
|提供有關如何加入新的採礦模型及處理結構和模型的詳細資訊|[將採礦模型加入結構 &#40;Analysis Services-資料採礦 &#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|提供資源的連結，這些資源可幫助您自訂演算法來建立採礦模型|[自訂採礦模型和結構](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|提供有關每一個採礦模型檢視器之資訊的連結|[資料採礦模型檢視器](../../analysis-services/data-mining/data-mining-model-viewers.md)|  
|了解如何建立增益圖、收益圖或分類矩陣，或是測試採礦結構|[測試和驗證 &#40;資料採礦&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|了解如何處理選項和權限|[處理資料採礦物件](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|提供有關 Analysis Services 的詳細資訊|[多維度模型資料庫 ](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md)|  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦設計師](../../analysis-services/data-mining/data-mining-designer.md)   
 [建立使用 SQL Server Data Tools &#40; 多維度模型SSDT &#41;](../../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [工作空間資料庫](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)  
  
  
