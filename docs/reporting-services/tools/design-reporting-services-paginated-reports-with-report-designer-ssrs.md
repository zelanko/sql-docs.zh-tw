---
title: 設計使用報表設計師 (SSRS) 報表 |Microsoft 文件
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], report creation
ms.assetid: 3a26dccc-6ad6-48f5-a882-f96c6c0dd405
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 25e3f58f4c104f6d21d72731fa95cc3f807605da
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291387"
---
# <a name="design-reporting-services-paginated-reports-with-report-designer-ssrs"></a>Reporting Services 分頁的報表與報表設計工具 (SSRS) 的設計

使用報表設計師建立完整功能的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表和報表方案。 報表設計師提供一個圖形介面，您可以在此介面中定義資料來源、資料集與查詢、資料區域與欄位的報表配置位置，以及定義互動式功能，例如搭配使用的參數和報表集。  

報表設計師是  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)](建立商業智慧方案的 Microsoft Visual Studio 環境) 的功能。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]不會包含與 SQL Server。 下載 [SQL Server Data Tools](https://go.microsoft.com/fwlink/?LinkID=616714)。 
  
## <a name="benefits-of-report-projects"></a>報表專案的優點  
報表專案是做為報表定義與資源的容器。 使用專案以執行下列動作：  
  
-   組織一個容器中的報表和相關的項目。  
  
-   測試包含本機報表及相關項目的報表方案。  
  
-   同時部署相關的項目。 使用專案屬性和組態管理以部署至多個環境中。  
  
-   保留一組報告和相關項目的主要複本。 部署後，可以偶爾修改已發行的報表。  
  
 使用本主題中的資訊，為 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 方案中的單一報表專案設計分頁報表和相關項目。 如需 SQL Server Data Tools 中方案和多個專案的詳細資訊，請參閱 [SQL Server Data Tools 中的 Reporting Services](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)。  

  
##  <a name="bkmk_SharedDataSources"></a> Shared Data Sources  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 定義及部署報表方案的共用資料來源。 透過使用 **OverwriteDataSources** 和 **TargetDataSourceFolder** 屬性，即可從專案中的其他項目獨立部署共用資料來源。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
 在報表設計師中，可在 [報表資料] 窗格和 [方案總管] 中工作，以定義用於報表的資料來源。 如需詳細資訊，請參閱 [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane)。 您無法使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 開啟已發行至報表伺服器或 SharePoint 網站的資料來源，但不包含在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 方案中。 針對該功能，請使用[報表產生器撰寫環境 &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md)。  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 是一個用戶端工具。 您可以本機測試電腦上的報表方案，將其部署至測試環境以測試伺服器方案，然後將其部署至實際執行環境。 部署後，請確認資料來源處理延伸模組和資料來源認證已針對報表伺服器環境進行設定。 您可以使用組態管理員，以協助您管理不同部署的屬性。 如需詳細資訊，請參閱 [SQL Server Data Tools &#40;SSDT&#41; 中的 Reporting Services](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)。  
  
 如需詳細資訊，請參閱 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
   
##  <a name="bkmk_SharedDatasets"></a> 共用資料集  
 使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 定義及部署報表方案的共用資料集。 透過使用 **OverwriteDatasets** 和 **TargetDatasetFolder** 屬性，即可從專案中的其他項目獨立部署共用資料集。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
 在報表設計師中，可在 [報表資料] 窗格和 [方案總管] 中工作，以定義用於報表的共用資料集。 如需詳細資訊，請參閱 [Report Data Pane](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_ReportDataPane)。 您無法使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 從報表伺服器或 SharePoint 網站直接開啟已發行的資料集。 針對該功能，請使用共用資料集模式中的[報表產生器撰寫環境 &#40;SSRS&#41;](../../reporting-services/tools/report-builder-authoring-environment-ssrs.md)。  
  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 是一個用戶端工具。 您可以使用查詢設計工具以協助本機建立及測試預覽中的查詢結果。 部署後，您可以從共用資料來源和所根據的報表獨立管理共用資料集。 如需詳細資訊，請參閱[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)、[查詢設計工具 &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md) 和[管理共用資料集](../../reporting-services/report-data/manage-shared-datasets.md)。  
  
##  <a name="bkmk_Reports"></a> 分頁報表  
分頁報表是儲存在報表專案中的檔案。 報表可用為獨立報表、子報表或主報表中鑽研動作的目標。 透過使用 **TargetReportFolder** 和其他屬性，即可從專案中的其他項目獨立部署報表。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
> [!NOTE]  
>  如果您發行至 SharePoint 模式中的報表伺服器，報表設計師專案中無法測試某些報表方案功能。 報表、子報表及鑽研報表的參考都必須使用僅可在部署報表專案後進行測試的完整 URL。 如需詳細資訊，請參閱 [SharePoint 模式在報表伺服器上已發行報表項目的 URL 範例 &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)。  
  
 您可以採用下列方法，將報表加入專案：  
  
-   **加入報表專案。** 依預設，空白報表隨即會在報表設計師中開啟。 如需詳細資訊，請參閱[將新的或現有的報表加入報表專案 &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md)。  
  
-   **加入 [報表精靈] 專案。** 您會在逐步指引下建立報表。 [報表精靈] 會將資料定義與報表設計簡化成一連串的步驟，這些步驟可以產生完成的報表。 您可以加入樣式為您自己的組織自訂精靈。 如需詳細資訊，請參閱[將新的或現有的報表加入報表專案 &#40;SSRS&#41;](../../reporting-services/tools/add-a-new-or-existing-report-to-a-report-project-ssrs.md)。  
  
-   **加入類型報表的項目。** 空白報表隨即會在報表設計師中開啟。  
  
-   **加入現有項目。** 現有的報表定義 (.rdl) 隨即會在報表設計師中開啟。 在舊版 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中開啟報表或專案可能會自動將專案升級成與目前版本相容，以及將報表升級成目前的結構描述。 如需詳細資訊，請參閱 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)。  
  
-   **匯入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Access 報表。** 從 Access 資料庫 (.mdb、.accdb) 或專案 (.adp) 檔案匯入所有報表。 報表設計師會將資料庫或專案檔案中的每一份報表，轉換成 RDL，並將其儲存在報表專案中。 並非所有 Access 報表的功能都會傳送至報表定義 (.rdl) 檔案。 如需詳細資訊，請參閱[從 Microsoft Access 匯入報表 &#40;Reporting Services&#41;](https://msdn.microsoft.com/library/4f29d5b8-b77d-4714-a84a-05523df55646) 和[支援的 Access 報表功能 &#40;SSRS&#41;](https://msdn.microsoft.com/library/7ffec331-6365-4c13-8e58-b77a48cffb44)。  
  
    > [!NOTE]  
    >  您必須將 Access 2002 或更新版本安裝在安裝報表設計師的相同電腦上，才能使用此匯入功能。 匯入報表時，必須能夠使用 Access 報表的資料來源。  
  
-   **直接在 RDL 中工作。** 當您在報表設計師中撰寫報表時，報表會以 XML 格式儲存為報表定義語言 (RDL) 檔案。 您可以在報表設計師、文字編輯工具，或任何可以編輯 XML 的工具中編輯此檔案。  
  
     當您在報表設計師中編輯報表定義來源時，您可在已安裝開發工具之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的目前 RDL 結構描述中處理工作。 建立專案時，結構描述版本可能會根據部署屬性進行變更。 如需詳細資訊，請參閱 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
     直接編輯 RDL 可能會導致無法發行至報表伺服器或無法執行的報表。 使用任何 XML 檔案時，請確認元素中所使用的 XML 特定字元已正確編碼。 當您發行報表時，報表伺服器會使用結構描述來驗證 RDL 檔案中所包含的 XML。  
  
     若要包含不是 RDL 結構描述一部分的元素，請將其放置在自訂元素中。 自訂元素可以透過自訂轉譯延伸模組讀取，但隨附 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的轉譯延伸模組會將其忽略。 例如，您可以使用自訂元素儲存報表中的註解。  
  
     如需詳細資訊，請參閱[報表定義語言 &#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)。  
  
##  <a name="bkmk_ReportParts"></a> 報表組件  
 在報表設計師中，建立專案的資料表、圖表及其他分頁報表項目之後，您可以將它們當作 *「報表組件」* 發行至報表伺服器或與報表伺服器整合的 SharePoint 網站，以供您和其他人員在其他報表中重複使用這些組件。 如需詳細資訊，請參閱[報表設計師中的報表組件 &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)。  
  
 透過使用 **TargetReportPartFolder** 和其他屬性，即可從專案中的其他項目獨立部署報表組件。 如需詳細資訊，請參閱[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
##  <a name="bkmk_Resources"></a> 資源  
 您可以將檔案加入與報表相關但不是由報表伺服器進行處理的專案。 例如，您可以加入圖片影像或空間資料的 ESRI 形狀檔。 如需詳細資訊，請參閱 [Resources](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md#bkmk_Resources)。  
 
##  <a name="bkmk_ReportLayout"></a> Paginated Report Layout  
 若要建立報表配置，請將報表項目和資料區從 [工具箱] 拖曳至設計介面，然後排列它們。 將資料集欄位拖曳至設計介面上的項目，即可將資料加入報表。 若要在 Tablix 資料區中組織群組的資料，請將資料集欄位拖曳至 [群組] 窗格。 因為報表撰寫工具是建立報表定義很重要的方法，所以報表設定的方法在報表建立器和報表設計師之間會相當類似。  
   
##  <a name="bkmk_Preview"></a> Preview a Paginated Report  
 使用 **[預覽]** 確認報表資料和配置設計。 預覽報表時，報表處理器會驗證報表定義和運算式語法，並列出 [Output](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) 視窗中的問題。  
  
> [!NOTE]  
>  預覽報表時，報表的資料會快取至本機電腦上的檔案。 當您再次預覽同一份報表時 (使用相同的查詢、參數和認證)，報表設計師會擷取快取複本，而非重新執行查詢。 資料檔案儲存為 *\<reportname>*.rdl.data 與報表定義檔案相同的目錄中。 您關閉報表設計師時，不會刪除此檔案。  
  
 您可以利用下列方式預覽報表。  
  
-   **預覽檢視。** 按一下 **預覽** 索引標籤。這會在本機執行報表，使用與報表伺服器相同的報表處理與轉譯功能。 顯示的報表是互動式影像；您可以選取參數、按一下連結、檢視文件引導模式，以及展開和摺疊報表的隱藏區域。 您也可以將報表匯出至任何已安裝的轉譯格式。  
  
-   **獨立預覽。** 在瀏覽器中執行本機報表。 透過使用偵錯組態，您也可以使用此模式以偵錯所撰寫的自訂組件。 有三種方法可在偵錯模式中執行專案：  
  
    -   在 **[偵錯]** 功能表上，按一下 **[開始偵錯]**。  
  
    -   在 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 標準工作列上，按一下 **[啟動]** 按鈕。  
  
    -   按下 F5。  
  
     如果您使用建立報表但是未部署報表的專案組態，則在目前組態之 **StartItem** 屬性中所指定的報表，會在另一個預覽視窗中開啟。  
  
    > [!NOTE]  
    >  若要使用偵錯模式，您必須設定啟動項目。 在 [方案總管] 中，以滑鼠右鍵按一下報表專案，再按一下 **[屬性]**，然後在 **[StartItem]** 中選取要顯示的報表名稱。  
  
     如果您想要預覽並非專案之啟動項目的特定報表，請選取建立報表但未部署報表的組態 (例如 DebugLocal 組態)，以滑鼠右鍵按一下報表，然後按一下 **[執行]**。 您必須選擇並未部署報表的組態；否則，報表將會發行至報表伺服器，而非在本機的預覽視窗中顯示。  
  
-   **預覽列印。**  
  
     當您第一次在 [預覽] 模式或預覽視窗中檢視報表時，報表的檢視類似於 HTML 轉譯延伸模組所產生的報表。 這個預覽並不是 HTML，不過報表的配置及分頁與 HTML 的輸出相似。  
  
     您可以切換到預覽列印模式，以變更檢視來顯示列印的報表。 按一下預覽工具列上的 **[預覽列印]** 按鈕。 所顯示的報表就如同在實際頁面上所看到的。 這個檢視與影像和 PDF 轉譯延伸模組所產生的輸出類似。 預覽列印並不是影像或 PDF 檔案，不過報表的配置及分頁與這些格式的輸出相似。 您可以選擇報表影像的大小，例如，設定頁面的寬度。  
  
     列印預覽可協助您識別許多可能會在列印報表時遇到的轉譯問題。 常見的轉譯問題包括：  
  
    -   額外的空白頁面是由於報表對於您針對報表指定的紙張大小太寬。  
  
    -   額外的空白頁面是由於報表包含動態展開以至於超出指定紙張寬度的矩陣。  
  
    -   群組之間的分頁符號未能依照您希望的方式運作。  
  
    -   頁首和頁尾不會如預期顯示。  
  
    -   報表配置需要修改列印格式才能清楚地閱讀。  
   
##  <a name="bkmk_SaveandDeploy"></a> Save and Deploy Paginated Reports  
 在報表設計師中，您可以本機儲存報表和其他專案檔案，或將它們部署至報表伺服器或 SharePoint 網站。 您可以根據所設定的部署屬性，獨立或同時部署共用資料來源、共用資料集、報表、報表資源及報表組件。 如需詳細資訊，請參閱 [Configuration and Deployment Properties](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties)。  
  
 在報表設計師中，請務必了解您設計的報表是使用報表定義結構描述，且此報表定義結構描述是由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 中目前版本的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]所支援。 當您針對特定報表伺服器或 SharePoint 網站設定專案部署屬性並儲存報表時，報表設計師會將報表定義儲存至結構描述中的組建目錄，且此結構描述符合目標報表伺服器上的版本。 若要建立可在下層報表伺服器上發行的報表，報表設計師則會卸除不存在於目標結構描述中的報表項目。 這個動作會自動發生，而不需要提示。 如果出現此錯誤，原始的報表定義會保留在專案資料夾中。 部署的已修改報表定義位於組建資料夾中。  
  
> [!NOTE]  
>  針對偵錯運算式和部署錯誤，您必須檢視組建資料夾中的報表定義。 請勿使用 **[檢視原始檔]**。 **[檢視原始檔]** 會顯示專案資料夾中的報表定義來源。  
  
 如需詳細資訊，請參閱 [Deployment and Version Support in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)。  
  
### <a name="save-a-report-locally"></a>本機儲存報表  
 當您在報表設計師中處理報表或其他專案項目時，檔案會儲存至本機電腦或在其他您擁有其存取權的電腦上進行共用。  
  
 如果您使用的是來源控制軟體，您可以需要在儲存報表時將報表存入來源控制伺服器。 如需詳細資訊，請參閱 [Source Control](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_SourceControl)。  
  
### <a name="deploy-or-publish-paginated-reports"></a>部署或發佈分頁報表  
 從 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，您可以將報表或其他專案項目部署至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器的多個版本。 使用專案組態可控制升級至與目標伺服器相容之結構描述版本的報表定義。 由專案組態所控制的屬性包括目標報表伺服器、建立期間用來暫時儲存用於預覽和部署之報表定義的資料夾，以及錯誤等級。 如需詳細資訊，請參閱[組態和部署屬性](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md#bkmk_ConfigurationandDeploymentProperties)和[設定部署屬性 &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)。  
  
### <a name="export-a-paginated-report-to-a-different-file-format"></a>將分頁報表匯出至不同的檔案格式  
 報表可以匯出為各種格式，而且這些格式會影響隨選報表配置與互動式功能如何運作。 如需各種輸出格式之設計考量的詳細資訊，請參閱[匯出報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)。  
   
##  <a name="bkmk_ReportValidationandErrorLevels"></a> 報表驗證和錯誤等級  
 預覽前和部署期間，將會驗證報表。 建立報表時，可能會發生一些建立問題。 例如，報表包含的字串 (如運算式或查詢) 可能會與專案組態所指定的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本不相容。  
  
 使用 ErrorLevel 屬性管理建立警告與錯誤。 ErrorLevel 屬性所包含的值可以從 0 到 4 (包含)。 這個值會判斷回報為錯誤的建立問題，以及回報為警告的建立問題。 預設值為 2。 這些警告和錯誤會寫入 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的 [[輸出]](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md#bkmk_Output) 視窗中。  
  
 嚴重性層級小於或等於 ErrorLevel 值的問題會回報為錯誤；否則，會將這些問題回報為警告。  
  
 下表列出這些錯誤層級。  
  
|錯誤層級|Description|  
|-----------------|-----------------|  
|0|最嚴重而且無法避免的建立問題，這些問題會導致無法預覽和部署報表。|  
|1|嚴重的建立問題，這些問題會徹底變更報表配置。|  
|2|較不嚴重的建立問題，這些問題會大幅變更報表配置。|  
|3|輕微的建立問題，這些問題會以可能不會注意到的次要方式變更報表配置。|  
|4|僅用於發行警告。|  
  
 當您嘗試預覽或部署的報表包含 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]中新的報表項目時，可以從報表移除這些報表項目。 根據預設，組態的 ErrorLevel 屬性設為 2，這會在移除對應時，使報表的建立失敗。 不過，如果您將 ErrorLevel 屬性的值變更為 0 或 1，就會卸除對應、發出警告，並繼續建立程序。  

## <a name="next-steps"></a>後續步驟

[下載 SQL Server Data Tools](https://go.microsoft.com/fwlink/?LinkID=616714)  
[SQL Server Data Tools 中的 reporting Services](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)   
[查詢設計工具](../../reporting-services/report-data/query-design-tools-ssrs.md)   
[SQL Server 資料工具中的部署和版本支援](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
