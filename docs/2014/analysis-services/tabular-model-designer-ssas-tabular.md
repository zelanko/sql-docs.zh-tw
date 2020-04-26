---
title: 表格式模型設計師（SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 223a8a300a4f3000512f8d75dfb7595cb52abc08
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067830"
---
# <a name="tabular-model-designer-ssas-tabular"></a>表格式模型設計師 (SSAS 表格式)
  表格式模型設計師是與 Microsoft [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2010 或更新版本整合的一部分，具有特別用來開發專業表格式模型方案的額外專案類型範本。  
  
 本主題的章節：  
  
-   [優點](#bkmk_benefits)  
  
-   [專案範本](#bkmk_proj_temp)  
  
-   [視窗和功能表](#bkmk_wind_men)  
  
-   [Visual Studio 整合](#bkmk_vsint)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a>各種  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]時，用來建立表格式模型的專案範本會加入至可用的專案類型中。 在使用其中一個範本建立新的表格式模型專案之後，您可以使用表格式模型設計師工具和精靈開始撰寫模型。  
  
 除了用於撰寫專業多維度和表格式模型方案的新範本和工具之外， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境也提供偵錯和專案週期功能，確保您能為組織建立最強大的 BI 方案。 如需 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]的詳細資訊，請參閱 [Visual Studio 使用者入門](https://go.microsoft.com/fwlink/?LinkId=206389)。  
  
##  <a name="project-templates"></a><a name="bkmk_proj_temp"></a>專案範本  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]時，下列表格式模型專案範本會加入至商業智慧專案類型中：  
  
 **Analysis Services 表格式專案**  
 這個範本可用來建立新的空白表格式模型專案。  
  
 **從伺服器匯入 (表格式)**  
 這個範本可用來從 Analysis Services 中的現有表格式模型擷取中繼資料，以建立新的表格式模型專案。  
  
 **從 PowerPivot 匯入**  
 這個範本可用來從 [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 檔案擷取中繼資料和其他資料，以建立新的表格式模型專案。  
  
> [!NOTE]  
>  表格式模型專案要求表格式模式的 Analysis Services 伺服器執行個體必須在本機或在網路上執行。  
  
##  <a name="windows-and-menus"></a><a name="bkmk_wind_men"></a> 視窗和功能表  
 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 表格式模型撰寫環境包含下列項目：  
  
### <a name="designer-window"></a>設計師視窗  
 設計師視窗可透過提供模型的視覺表示法，用來撰寫表格式模型。 當您開啟 Model.bim 檔案時，會在設計師視窗中開啟模型。 您可以在設計師視窗中使用兩種不同的檢視模式撰寫模型：  
  
 **資料檢視**  
 資料檢視以表格式的方格格式顯示資料表。 您也可以使用量值方格定義量值，僅針對 [資料檢視] 中的每個資料表顯示。  
  
 **圖表視圖**  
 此圖表檢視以圖形格式顯示資料表，以及資料表之間的關聯性。 您可以篩選資料行、量值、階層及 KPI，也可以選擇使用定義的檢視方塊來檢視模型。  
  
 您可以在上述任一檢視中，執行大部分的模型撰寫工作。  
  
### <a name="solution-explorer"></a>方案總管  
 [方案總管] 視窗以表格式模型專案及其相關項目的邏輯容器來呈現使用中方案。 模型專案 (.smproj) 只包含 References 物件 (空白) 和 Model.bim 檔案。 您可以開啟專案項目進行修改，以及直接從這個檢視執行其他管理工作。  
  
 表格式模型方案通常只包含一個專案；但是，方案也可以包含其他專案，例如 Integration Services 或 Reporting Services 專案。 您可以加入任意數目的檔案，但是這些檔案的類型不得與表格式模型專案檔案的類型相同，且其 [建置動作] 屬性設為 [無] 或 [複製到輸出] 屬性設為 [不要複製]。  
  
 若要檢視方案總管，請按一下 [檢視]**** 功能表，然後按一下方案總管****。  
  
### <a name="properties-window"></a>屬性視窗  
 [屬性] 視窗列出選取物件的屬性。 下列物件具有可在 [屬性] 視窗中檢視及編輯的屬性：  
  
-   Model.bim  
  
-   Table  
  
-   資料行  
  
-   Measure  
  
 [專案屬性] 僅會顯示 [屬性] 視窗中的專案名稱和專案資料夾。 專案也具有您可以使用強制回應屬性對話方塊設定的其他部署選項和部署伺服器設定。 若要檢視這些屬性，請以滑鼠右鍵按一下方案總管**** 中的專案，然後按一下 [屬性]****。  
  
 [屬性] 視窗中的欄位包含內嵌控制項，當您按一下欄位時，即會開啟這些控制項。 編輯控制項的類型會隨著特定屬性而不同。 這些控制項包含編輯方塊、下拉式清單和自訂對話方塊的連結。 呈暗灰色的屬性是唯讀的。  
  
 若要檢視 [屬性]**** 視窗，請按一下 [檢視]**** 功能表，然後按一下 [屬性視窗]****。  
  
### <a name="error-list"></a>錯誤清單  
 [錯誤清單] 視窗包含模型狀態的訊息：  
  
-   安全性最佳作法的通知。  
  
-   資料處理的需求。  
  
-   角色之導出資料行、量值及資料列篩選的語意錯誤資訊。 您可以按兩下導出資料行的錯誤訊息，瀏覽至錯誤的來源。  
  
-   DirectQuery 驗證錯誤。  
  
 依預設，除非傳回錯誤，否則不會顯示 [錯誤清單]****。 但是，您可以隨時檢視 [錯誤清單]**** 視窗。 若要檢視 [錯誤清單]**** 視窗，請按一下 [檢視]**** 功能表，然後按一下 [錯誤清單]****。  
  
### <a name="output"></a>輸出  
 建置和部署資訊會顯示在 [輸出]**** 視窗中 (以及模型進度對話方塊)。 若要檢視 [輸出]**** 視窗，請按一下 [檢視]**** 功能表，然後按一下 [輸出]。  
  
### <a name="menu-items"></a>功能表項目  
 當您安裝 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]時，特別用來撰寫表格式模型的額外功能表項目會加入至 Visual Studio 功能表列。 [模型]**** 功能表可用來啟動資料匯入精靈、檢視現有連接、處理工作空間資料，以及在 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 中瀏覽模型工作空間。 [資料表]**** 功能表用來建立及管理資料表之間的關聯性、建立及管理量值、指定資料表設定、指定計算選項，以及指定其他資料表屬性。 您可以使用 [資料行]**** 功能表在資料表中加入及刪除資料行、隱藏及取消隱藏資料行，以及指定其他資料行屬性，例如資料類型和篩選。 您可以在 [建立]**** 功能表上建立及部署表格式模型方案。 複製/貼上功能包含在 [編輯]**** 功能表中。  
  
 除了這些功能表項目之外，也會將其他設定加入至 [工具] 功能表項目的 Analysis Services 選項。  
  
### <a name="toolbar"></a>工具列  
 Analysis Services 工具列可輕鬆快速地存取最常用的模型撰寫命令。  
  
##  <a name="visual-studio-integration"></a><a name="bkmk_vsint"></a> Visual Studio 整合  
 **原始檔控制**  
 Analysis Services 專案會與選取的原始檔控制外掛程式整合。 如果您已設定 Visual Studio 使用原始檔控制，則可以從 [方案總管] 使用簽入/簽出。 若要設定使用 Team Foundation Server，請參閱 [Configure Visual Studio with Team Foundation Version Control](https://msdn.microsoft.com/library/ms253064.aspx)(使用 Team Foundation 版本控制設定 Visual Studio)。 此外，也支援許多協力廠商原始檔控制外掛程式。  
  
 **字型**  
 表格式模型使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境字型來控制顯示的字型。 如果預設 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 字型不含您的語言所需的全部 Unicode 字元，您可能必須變更此字型。 若要變更字型，請依序按一下 [工具]**** 功能表、[選項]**** 及 [字型和色彩]****。  
  
 **鍵盤快速鍵**  
 您可以透過 [工具] -> [選項] -> [鍵盤] 對話方塊，設定/重新對應 Analysis Services 鍵盤快速鍵。 表格式模型設計師內容支援如建立、儲存、偵錯、新增專案等一些通用的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 快速鍵。 其他表格式模型設計師的特定快速鍵則會在 Analysis Services 內容中。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SSAS 表格式&#41;的表格式模型專案](tabular-models/tabular-model-projects-ssas-tabular.md)   
 [屬性 &#40;SSAS 表格式&#41;](tabular-models/properties-ssas-tabular.md)  
  
  
