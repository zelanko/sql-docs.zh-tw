---
title: "表格式模型設計師 |Microsoft 文件"
ms.date: 10/19/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.custom: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
caps.latest.revision: "22"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 14a6ca056a079b4a51813783883cc09c5f53e8ad
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="tabular-model-designer-ssas"></a>表格式模型設計師 (SSAS)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]表格式模型設計師屬於[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、 整合與 Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，具有特別用來開發專業表格式模型方案的額外專案類型範本。  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 可從 Web 免費下載安裝。 如需詳細資訊，請參閱[下載 SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)。    
  
##  <a name="bkmk_benefits"></a> 優點  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，用來建立表格式模型的專案範本會加入至可用的專案類型中。 在使用其中一個範本建立新的表格式模型專案之後，您可以使用表格式模型設計師工具和精靈開始撰寫模型。  
  
 除了用於撰寫專業多維度和表格式模型方案的新範本和工具之外， [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 環境也提供偵錯和專案週期功能，確保您能為組織建立最強大的 BI 方案。 如需 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]的詳細資訊，請參閱 [Visual Studio 使用者入門](http://go.microsoft.com/fwlink/?LinkId=206389)。  
  
##  <a name="bkmk_proj_temp"></a>專案範本  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，下列表格式模型專案範本會加入至商業智慧專案類型中：  
  
 **Analysis Services 表格式專案**  
 這個範本可用來建立新的空白表格式模型專案。 當您建立專案時會指定相容性層級。
  
 **從伺服器匯入 (表格式)**  
 這個範本可用來從 Analysis Services 中的現有表格式模型擷取中繼資料，以建立新的表格式模型專案。  
  
 舊版模型具有舊版相容性層級。 您可以藉由匯入模型定義之後變更相容性層級屬性升級。  
  
 **匯入自 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**  
 這個範本可用來從 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 檔案擷取中繼資料和其他資料，以建立新的表格式模型專案。  
  
##  <a name="bkmk_wind_men"></a> 視窗和功能表  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 表格式模型撰寫環境包含下列項目：  
  
### <a name="designer-window"></a>設計工具視窗  
 設計師視窗可透過提供模型的視覺表示法，用來撰寫表格式模型。 當您開啟 Model.bim 檔案時，會在設計師視窗中開啟模型。 您可以在設計師視窗中使用兩種不同的檢視模式撰寫模型：  
  
 **資料檢視**  
 資料檢視以表格式的方格格式顯示資料表。 您也可以使用量值方格定義量值，僅針對 [資料檢視] 中的每個資料表顯示。  
  
 **圖表檢視**  
 此圖表檢視以圖形格式顯示資料表，以及資料表之間的關聯性。 您可以篩選資料行、量值、階層及 KPI，也可以選擇使用定義的檢視方塊來檢視模型。  
  
 您可以在上述任一檢視中，執行大部分的模型撰寫工作。  
  
### <a name="view-code-window"></a>檢視程式碼視窗  
 當您在方案總管中以滑鼠右鍵按一下檔案並選取 [檢視程式碼] 時，即可檢視 Model.bim 檔案背後的程式碼。 在 1200年或更新版本的相容性層級的表格式模型，模型定義是以 JSON 表示。  
  
 請注意，您需要提供 JSON 編輯器的完整版 Visual Studio。 如果您不需要商業版本中的額外功能，您可以下載並安裝 [免費的 Visual Studio Community Edition](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) 。  
  
### <a name="solution-explorer"></a>方案總管  
 [方案總管] 視窗以表格式模型專案及其相關項目的邏輯容器來呈現使用中方案。 模型專案 (.smproj) 只包含 References 物件 (空白) 和 Model.bim 檔案。 您可以開啟專案項目進行修改，以及直接從這個檢視執行其他管理工作。  
  
 表格式模型方案通常只包含一個專案；但是，方案也可以包含其他專案，例如 Integration Services 或 Reporting Services 專案。 您可以加入任意數目的檔案，但是這些檔案的類型不得與表格式模型專案檔案的類型相同，且其 [建置動作] 屬性設為 [無] 或 [複製到輸出] 屬性設為 [不要複製]。  
  
 若要檢視方案總管，請按一下 [檢視] 功能表，然後按一下方案總管。  

### <a name="tabular-model-explorer"></a>表格式模型總管
  第一個可用在 2016 年 8 月版本 (14.0.60812.0) 的[SQL Server Data Tools](https://msdn.microsoft.com/mt186501)，表格式模型總管可以幫助您瀏覽表格式模型中的中繼資料物件。

 若要顯示表格式模型總管，請按一下 [檢視] > [其他視窗]，然後按一下 [Tabular Model Explorer (表格式模型總管)]。
   
  ![表格式模型總管](../../analysis-services/tabular-models/media/tabular-model-explorer.png) 
  
 表格式模型總管 會組織一個非常類似表格式模型的結構描述樹狀結構中的中繼資料物件。 「資料來源」、「檢視方塊」、「關聯性」、「角色」、「資料表」和「翻譯」對應至最上層結構描述物件。 有一些例外狀況 (尤其是 KPI 和量值)，就技術上而言，它們不是最上層物件，而是模型中各種資料表的子物件。 不過，合併所有 KPI 和量值的最上層容器即可輕鬆地使用這些物件，特別是您的模型包含非常大量的資料表時。 量值也會列在其對應的父資料表下方，因此，您必須清楚了解實際的父子式關聯性。 如果您在最上層 [量值] 容器中選取量值，則也會選取其資料表下之子集合中的相同量值，反之亦然。  
 
 表格式模型總管中的物件節點會連結至適當的功能表選項，這些功能表選項到目前為止是隱藏在 Visual Studio 中的 [模型]、[資料表] 和 [資料行] 功能表下方。 您可以使用滑鼠右鍵按一下物件，以探索物件類型的選項。 並非所有物件節點類型都有內容功能表，但後續版本會推出其他選項和增強功能。 

 表格式模型總管也提供方便使用的搜尋功能。 只要在 [搜尋] 方塊中輸入名稱的某個部分，表格式模型總管就會縮小樹狀檢視以找到相符項目。 
  
### <a name="properties-window"></a>屬性視窗  
 [屬性] 視窗列出選取物件的屬性。 下列物件具有可在 [屬性] 視窗中檢視及編輯的屬性：  
  
-   Model.bim  
  
-   Table  
  
-   資料行  
  
-   [量值]  
  
 [專案屬性] 僅會顯示 [屬性] 視窗中的專案名稱和專案資料夾。 專案也具有您可以使用強制回應屬性對話方塊設定的其他部署選項和部署伺服器設定。 若要檢視這些屬性，請以滑鼠右鍵按一下方案總管中的專案，然後按一下 [屬性]。  
  
 [屬性] 視窗中的欄位包含內嵌控制項，當您按一下欄位時，即會開啟這些控制項。 編輯控制項的類型會隨著特定屬性而不同。 這些控制項包含編輯方塊、下拉式清單和自訂對話方塊的連結。 呈暗灰色的屬性是唯讀的。  
  
 若要檢視 [屬性] 視窗，請按一下 [檢視] 功能表，然後按一下 [屬性視窗]。  
  
### <a name="error-list"></a>錯誤清單  
 [錯誤清單] 視窗包含模型狀態的訊息：  
  
-   安全性最佳作法的通知。  
  
-   資料處理的需求。  
  
-   角色之導出資料行、量值及資料列篩選的語意錯誤資訊。 您可以按兩下導出資料行的錯誤訊息，瀏覽至錯誤的來源。  
  
-   DirectQuery 驗證錯誤。  
  
 依預設，除非傳回錯誤，否則不會顯示 [錯誤清單]。 但是，您可以隨時檢視 [錯誤清單] 視窗。 若要檢視 [錯誤清單] 視窗，請按一下 [檢視] 功能表，然後按一下 [錯誤清單]。  
  
### <a name="output"></a>輸出  
 建置和部署資訊會顯示在 [輸出] 視窗中 (以及模型進度對話方塊)。 若要檢視 [輸出] 視窗，請按一下 [檢視] 功能表，然後按一下 [輸出]。  
  
### <a name="menu-items"></a>功能表項目  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]時，特別用來撰寫表格式模型的額外功能表項目會加入至 Visual Studio 功能表列。 [模型] 功能表可用來啟動資料匯入精靈、檢視現有連接、處理工作空間資料，以及在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel 中瀏覽模型工作空間。 [資料表] 功能表用來建立及管理資料表之間的關聯性、建立及管理量值、指定資料表設定、指定計算選項，以及指定其他資料表屬性。 您可以使用 [資料行] 功能表在資料表中加入及刪除資料行、隱藏及取消隱藏資料行，以及指定其他資料行屬性，例如資料類型和篩選。 您可以在 [建立] 功能表上建立及部署表格式模型方案。 複製/貼上功能包含在 [編輯] 功能表中。  
  
 除了這些功能表項目之外，也會將其他設定加入至 [工具] 功能表項目的 Analysis Services 選項。  
  
### <a name="toolbar"></a>工具列  
 Analysis Services 工具列可輕鬆快速地存取最常用的模型撰寫命令。  
  
##  <a name="bkmk_vsint"></a>Visual Studio 整合  
 **原始檔控制**  
 Analysis Services 專案會與選取的原始檔控制外掛程式整合。 如果您已設定 Visual Studio 使用原始檔控制，則可以從 [方案總管] 使用簽入/簽出。 若要設定使用 Team Foundation Server，請參閱 [Configure Visual Studio with Team Foundation Version Control](http://msdn.microsoft.com/library/ms253064.aspx)(使用 Team Foundation 版本控制設定 Visual Studio)。 此外，也支援許多協力廠商原始檔控制外掛程式。  
  
 **字型**  
 表格式模型使用 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 環境字型來控制顯示的字型。 如果預設 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 字型不含您的語言所需的全部 Unicode 字元，您可能必須變更此字型。 若要變更字型，請依序按一下 [工具] 功能表、[選項] 及 [字型和色彩]。  
  
 **鍵盤快速鍵**  
 您可以透過 [工具] -> [選項] -> [鍵盤] 對話方塊，設定/重新對應 Analysis Services 鍵盤快速鍵。 表格式模型設計師內容支援如建立、儲存、偵錯、新增專案等一些通用的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 快速鍵。 其他表格式模型設計師的特定快速鍵則會在 Analysis Services 內容中。  
  
## <a name="see-also"></a>另請參閱  
 [表格式模型專案 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md)   
 [屬性 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/properties-ssas-tabular.md)  
  
  
