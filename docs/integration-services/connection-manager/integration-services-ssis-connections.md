---
title: Integration Services (SSIS) 連線 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.asvs.connectionmanager.f1
- sql13.dts.designer.adddtsconnection.f1
helpviewer_keywords:
- Integration Services packages, connections
- SSIS packages, connections
- sources [Integration Services], connections
- packages [Integration Services], connections
- destinations [Integration Services], connections
- tasks [Integration Services], connections
- connections [Integration Services], about connections
- connections [Integration Services]
- SQL Server Integration Services packages, connections
ms.assetid: 72f5afa3-d636-410b-9e81-2ffa27772a8c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4efe82fa71303bdaf4f8615c80ce45ae3dfda857
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52514121"
---
# <a name="integration-services-ssis-connections"></a>Integration Services (SSIS) 連接
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝會使用連接來執行不同的工作以及實作 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 功能：  
  
-   連接至來源和目的地資料存放區，例如文字、XML、Excel 活頁簿，以及用來擷取及載入資料的關聯式資料庫。  
  
-   連接至內含參考資料的關聯式資料庫，以執行完全查閱或模糊查閱。  
  
-   連接至關聯式資料庫，以執行 SQL 陳述式 (例如 SELECT、DELETE 和 INSERT 命令) 以及預存程序。  
  
-   連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以執行維護和轉換工作，例如備份資料庫及傳送登入。  
  
-   在文字和 XML 檔案中寫入記錄項目，並將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表和封裝組態寫入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
-   連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，以建立部分轉換在執行工作時所需要的暫存工作資料表。  
  
-   連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案和資料庫，以存取資料採礦模型、處理 Cube 和維度並執行 DDL 程式碼。  
  
-   指定現有檔案和資料或建立新檔案和資料夾，以便搭配「Foreach 迴圈」列舉值和工作一起使用。  
  
-   連接至訊息佇列，並連接至 Windows Management Instrumentation (WMI)、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO)、Web 及郵件伺服器。  
  
 若要建立這些連接， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用連接管理員，如下節中所述。  
  
## <a name="connection-managers"></a>連接管理員  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用連接管理員做為連接的邏輯表示法。 在設計階段，您可以設定連接管理員的屬性，以描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在封裝執行時建立的實體連接。 例如，連接管理員會包含您可在設計階段設定的 **ConnectionString** 屬性；在執行階段，會使用連接字串屬性中的值建立實體連接。  
  
 封裝可使用連接管理員類型的多個執行個體，並且您可以在每個執行個體上設定屬性。 在執行階段，連接管理員類型的每個執行個體都會建立具有不同屬性的連接。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會提供不同類型的連接管理員，可讓封裝連接到各種資料來源和伺服器：  
  
-   當您安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時，安裝程式會安裝內建的連接管理員。  
  
-   有些連接管理員可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 網站下載。  
  
-   如果現有的連接管理員不符合您的需求，您可以建立自己的自訂連接管理員。  

### <a name="package-level-and-project-level-connection-managers"></a>套件層級及專案層級的連線管理員
您可以在封裝層級或專案層級建立連接管理員。 在專案層級建立的連接管理員可在專案中的所有封裝上使用。 而在封裝層級建立的連接管理員則可在該特定封裝上使用。  
  
 您將使用在專案層級建立的連接管理員取代資料來源，以共用來源的連接。 若要在專案層級加入連接管理員，則 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案必須使用專案部署模型。 當專案設定為使用該模型時，[連線管理員] 資料夾會出現在方案總管中，而 [資料來源] 資料夾則會從方案總管移除。  
  
> [!NOTE]  
>  若您想使用封裝中的資料來源，便需要將專案轉換為封裝部署模型。  
>   
>  如需兩個模型及將專案轉換為專案部署模型的詳細資訊，請參閱[部署 Integration Services (SSIS) 專案及套件](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)。

### <a name="built-in-connection-managers"></a>內建的連接管理員  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的連接管理員類型。  
  
|類型|Description|主題|  
|----------|-----------------|-----------|  
|ADO|連接到 ActiveX Data Objects (ADO) 物件。|[ADO 連線管理員](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|使用 .NET 提供者連接到資料來源。|[ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|CACHE|從資料流程或快取檔案 (.caw) 中讀取資料，而且可以將資料儲存至快取檔案。|[快取連接管理員](../../integration-services/connection-manager/cache-connection-manager.md)|  
|DQS|連接至 Data Quality Services 伺服器及伺服器上的 Data Quality Services 資料庫。|[DQS 清理連接管理員](../../integration-services/connection-manager/dqs-cleansing-connection-manager.md)|  
|EXCEL|連接到 Excel 活頁簿檔案。|[Excel 連接管理員](../../integration-services/connection-manager/excel-connection-manager.md)|  
|FILE|連接到檔案或資料夾。|[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)|  
|FLATFILE|連接到單一一般檔案中的資料。|[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)|  
|FTP|連接到 FTP 伺服器。|[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)|  
|HTTP|連接到 Web 伺服器。|[HTTP 連接管理員](../../integration-services/connection-manager/http-connection-manager.md)|  
|MSMQ|連接到訊息佇列。|[MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)|  
|MSOLAP100|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的執行個體。|[Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)|  
|MULTIFILE|連接到多個檔案和資料夾。|[多重檔案連線管理員](../../integration-services/connection-manager/multiple-files-connection-manager.md)|  
|MULTIFLATFILE|連接到多個資料檔案和資料夾。|[多重一般檔案連線管理員](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|  
|OLEDB|使用 OLE DB 提供者連接到資料來源。|[OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|使用 ODBC 連接到資料來源。|[ODBC 連線管理員](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|SMOServer|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 伺服器。|[SMO 連接管理員](../../integration-services/connection-manager/smo-connection-manager.md)|  
|SMTP|連接到 SMTP 郵件伺服器。|[SMTP 連接管理員](../../integration-services/connection-manager/smtp-connection-manager.md)|  
|SQLMOBILE|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 壓縮資料庫。|[SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
|WMI|連接到伺服器，並指定該伺服器上 Windows Management Instrumentation (WMI) 管理的範圍。|[WMI 連線管理員](../../integration-services/connection-manager/wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>可下載的連接管理員  
 下表列出您可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 網站下載的其他連接管理員類型。  
  
> [!IMPORTANT]  
>  下表所列出的連線管理員只可搭配 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 和 [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]使用。  
  
|類型|Description|主題|  
|----------|-----------------|-----------|  
|ORACLE|連線到 Oracle \<版本資訊\> 伺服器。|Oracle 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面上的 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)。|  
|SAPBI|連接到 SAP NetWeaver BI 7 系統。|SAP BI 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面的＜ [Microsoft SQL Server 2008 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=262016)＞。|  
|TERADATA|連線到 Teradata \<版本資訊\> 伺服器。|Teradata 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面上的 [Microsoft Connectors for Oracle and Teradata by Attunity](https://go.microsoft.com/fwlink/?LinkId=251526)。|  
  
### <a name="custom-connection-managers"></a>自訂連接管理員  
 您也可以撰寫自訂連接管理員。 如需詳細資訊，請參閱＜ [Developing a Custom Connection Manager](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)＞。  
  
## <a name="create-connection-managers"></a>建立連線管理員
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含各種連接管理員，以符合連接到不同類型伺服器和資料來源之工作的需要。 連接管理員可由在不同類型資料儲存區中擷取和載入之資料的資料流程元件使用，也可由將記錄寫入伺服器、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表或檔案的記錄提供者使用。 例如，具有傳送郵件工作的封裝使用 SMTP 連接管理員類型，來連接到 Simple Mail Transfer Protocol (SMTP) 伺服器。 具有執行 SQL 工作的封裝，可以使用 OLE DB 連線管理員來連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
 若要在您建立新的封裝時自動建立及設定連線管理員，您可以使用 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 精靈也可以幫助您建立及設定使用連線管理員的來源和目的地。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](../../integration-services/create-packages-in-sql-server-data-tools.md)。  
  
 若要手動建立新的連線管理員，並將其加入至現有的封裝，請使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師之 [控制流程]、[資料流程] 和 [事件處理常式] 索引標籤上所出現的 [連線管理員] 區域。 從 [連線管理員] 區域，您可以使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師所提供的對話方塊，來選擇要建立的連線管理員類型，然後再設定連線管理員的屬性。 如需詳細資訊，請參閱本主題稍後的「使用連線管理員區域」一節。  
  
 將連接管理員加入封裝之後，您就可以在工作、「Foreach 迴圈」容器、來源、轉換和目的地中使用它。 如需詳細資訊，請參閱 [Integration Services 工作](../../integration-services/control-flow/integration-services-tasks.md)、[Foreach 迴圈容器](../../integration-services/control-flow/foreach-loop-container.md)和[資料流程](../../integration-services/data-flow/data-flow.md)。  
  
### <a name="using-the-connection-managers-area"></a>使用連接管理員區域  
 當 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師的 [控制流程]、[資料流程] 或 [事件處理常式] 索引標籤處於作用中時，您可以建立連線管理員。  
  
 下圖顯示 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師之 [控制流程] 索引標籤上的 [連線管理員] 區域。  
  
 ![具有套件之控制流程設計工具的螢幕擷取畫面](../../integration-services/connection-manager/media/samplecontrolflow.gif "具有套件之控制流程設計工具的螢幕擷取畫面")    
  
### <a name="32-bit-and-64-bit-providers-for-connection-managers"></a>連接管理員的 32 位元和 64 位元提供者  
 連接管理員使用的許多提供者都有 32 位元和 64 位元兩種版本。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 設計環境是 32 位元的環境；設計封裝時，您只會看到 32 位元的提供者。 因此，如果要將連接管理員設定成使用特定的 64 位元提供者，您必須同時安裝 32 位元版本的同一個提供者。  
  
 執行階段中會使用正確的版本，而且就算您在設計階段中指定了 32 位元版本的提供者也沒有關係。 即使封裝是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中執行，還是可以執行 64 位元版本的提供者。  
  
  兩個版本的提供者具有相同的識別碼。 若要指定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段是否使用可用的 64 位元版本提供者，請設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案的 Run64BitRuntime 屬性。 如果 Run64BitRuntime 屬性設定為 **true**，執行階段會尋找並使用 64 位元提供者；如果 Run64BitRuntime 是 **false**，執行階段便會尋找並使用 32 位元提供者。 如需可在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案上設定之屬性的詳細資訊，請參閱 [Integration Services (SSIS) 和 Studio 環境](https://msdn.microsoft.com/library/ms140028.aspx)。   

## <a name="add-a-connection-manager"></a>新增連線管理員
###  <a name="wizard"></a> 在建立套件時新增連線管理員  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈  
  
     除了建立及設定連接管理員之外，此精靈也會協助您建立及設定使用此連接管理員的來源和目的地。 如需詳細資訊，請參閱 [在 SQL Server 資料工具中建立封裝](../../integration-services/create-packages-in-sql-server-data-tools.md)。  
  
###  <a name="package"></a> 將連線管理員新增至現有的套件  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連線管理員] 區域可用。  
  
4.  以滑鼠右鍵按一下 [連線管理員] 區域的任意位置，然後執行下列其中之一：  
  
    -   按一下要加入封裝的連接管理員類型。  
  
         -或-  
  
    -   如果未列出要加入的類型，請按一下 [新增連接]，以開啟 [加入 SSIS 連線管理員] 對話方塊、選取連線管理員類型，然後按一下 [確定]。  
  
     已選取連接管理員類型的自訂對話方塊隨即開啟。 如需有關連接管理員類型和可用選項的詳細資訊，請參閱下列選項表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](../../integration-services/connection-manager/ado-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連線管理員](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)|[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[加入檔案連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 連線管理員 UI 參考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 連線管理員編輯器](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     [連線管理員] 區域會列出加入的連線管理員。  
  
5.  選擇性地以滑鼠右鍵按一下連線管理員，並按一下 [重新命名]，然後修改連線管理員的預設名稱。  
  
6.  若要儲存更新的封裝，請按一下 [檔案] 功能表上的 [儲存選取項目]。  
  
###  <a name="project"></a> 在專案層級新增連線管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，開啟 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，以滑鼠右鍵按一下 [連線管理員]，然後按一下 [新增連線管理員]。  
  
3.  在 [加入 SSIS 連線管理員] 對話方塊中，選取連線管理員的類型，然後按一下 [加入]。  
  
     已選取連接管理員類型的自訂對話方塊隨即開啟。 如需有關連接管理員類型和可用選項的詳細資訊，請參閱下列選項表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](../../integration-services/connection-manager/ado-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連線管理員](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)|[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[加入檔案連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 連線管理員 UI 參考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 連線管理員編輯器](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
     您加入的連線管理員將會顯示在方案總管的 [連線管理員] 節點底下。 針對專案中的所有封裝，它也會顯示在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中。 此索引標籤中連線管理員名稱的前置詞將是 **(專案)**，以區分此專案層級連線管理員以及封裝層級連線管理員。  
  
4.  或者，以滑鼠右鍵按一下方案總管視窗之 [連線管理員] 節點底下的連線管理員 (或) 在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，按一下 [重新命名]，然後修改連線管理員的預設名稱。  
  
    > [!NOTE]  
    >  在 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，您無法覆寫連線管理員名稱中的 **(專案)** 前置詞。 這是原廠設定。  

### <a name="add-ssis-connection-manager-dialog-box"></a>新增 SSIS 連線管理員對話方塊
使用 [加入 SSIS 連線管理員] 對話方塊來選取要加入封裝的連接類型。  
  
 若要深入了解連線管理員，請參閱 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)。  
  
#### <a name="options"></a>選項。  
 **連線管理員類型**  
 選取連接類型，然後按一下 [加入]，或按兩下連接類型，以使用每個連接類型的編輯器來指定連接屬性。  
  
 **[加入]**  
 使用每個連接類型的編輯器，來指定連接屬性。  
   
##  <a name="parameter"></a> 建立連線管理員屬性的參數  
  
1.  在 [連線管理員] 區域中，以滑鼠右鍵按一下您要建立其參數的連線管理員，然後按一下 [參數化]。  
  
2.  在 [參數化] 對話方塊中設定參數設定。 如需詳細資訊，請參閱[參數化對話方塊](https://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350)。  

## <a name="delete-a-connection-manager"></a>刪除連線管理員 
###  <a name="DeletePackageLevel"></a> 從套件中刪除連線管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連線管理員] 區域可用。  
  
4.  以滑鼠右鍵按一下您要刪除的連線管理員，然後按一下 [刪除]。  
  
     如果您要刪除封裝元素 (如執行 SQL 工作或 OLE DB 來源) 所使用的連線管理員，您將會遇到以下結果：  
  
    -   在封裝元素上出現一個錯誤圖示，表示使用了已刪除的連線管理員。  
  
    -   此封裝驗證失敗。  
  
    -   無法執行此封裝。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
###  <a name="DeleteProjectLevel"></a> 刪除共用的連線管理員 (專案層級的連線管理員)  
  
1.  若要刪除專案層級的連線管理員，以滑鼠右鍵按一下方案總管視窗之 [連線管理員] 節點底下的連線管理員，然後按一下 [刪除]。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 會顯示下列警告訊息：  
  
    > [!WARNING]  
    >  刪除專案連接管理員後，使用該連接管理員的封裝可能無法執行。 您無法恢復這個動作。 您要刪除連接管理員嗎?  
  
2.  按一下 [確定] 可刪除該連接管理員，或按一下 [取消] 可保留該連接管理員。  
  
    > [!NOTE]  
    >  您也可以從針對專案中任何封裝開啟之 [SSIS 設計師] 視窗的 [連線管理員] 索引標籤中，刪除專案層級的連線管理員。 為此，以滑鼠右鍵按一下索引標籤中的連線管理員，然後按一下 [刪除]。 
    
## <a name="set-the-properties-of-a-connection-manager"></a>設定連線管理員的屬性
所有連接管理員都可以使用 [屬性] 視窗進行設定。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 還提供自訂對話方塊，用以修改 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中不同類型的連線管理員。 因連接管理員類型的不同，對話方塊也有不同的選項集。  
  
### <a name="modify-a-connection-manager-using-the-properties-window"></a>使用 [屬性] 視窗修改連線管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 SSIS 設計師中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連接管理員] 區域可用。  
  
4.  以滑鼠右鍵按一下連接管理員，然後按一下 [屬性]。  
  
5.  在 [屬性] 視窗中編輯屬性值。 針對部分無法在連接管理員之標準編輯器中設定的屬性，[屬性] 視窗提供了對這些屬性的存取權。  
  
6.  按一下 [確定] 。  
  
7.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>使用連線管理員對話方塊修改連線管理員  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 中，按一下 [控制流程] 索引標籤、[資料流程] 索引標籤或 [事件處理常式] 索引標籤，以讓 [連接管理員] 區域可用。  
  
4.  在 [連接管理員] 區域中，按兩下連接管理員，以開啟 [連接管理員] 對話方塊。 如需有關特定連接管理員類型以及每種類型可用之選項的詳細資訊，請參閱下表。  
  
    |[ODBC 來源編輯器]|選項。|  
    |------------------------|-------------|  
    |[ADO 連線管理員](../../integration-services/connection-manager/ado-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)|[設定 ADO.NET 連線管理員](../../integration-services/connection-manager/configure-ado-net-connection-manager.md)|  
    |[Analysis Services 連線管理員](../../integration-services/connection-manager/analysis-services-connection-manager.md)|[加入 Analysis Services 連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Excel 連線管理員](../../integration-services/connection-manager/excel-connection-manager.md)|[Excel 連線管理員編輯器](../../integration-services/connection-manager/excel-connection-manager-editor.md)|  
    |[檔案連線管理員](../../integration-services/connection-manager/file-connection-manager.md)|[檔案連線管理員編輯器](../../integration-services/connection-manager/file-connection-manager-editor.md)|  
    |[多重檔案連線管理員](../../integration-services/connection-manager/multiple-files-connection-manager.md)|[加入檔案連線管理員對話方塊 UI 參考](../../integration-services/connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[一般檔案連線管理員](../../integration-services/connection-manager/flat-file-connection-manager.md)|[一般檔案連線管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[資料行] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;[進階] 頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)|  
    |[多重一般檔案連線管理員](../../integration-services/connection-manager/multiple-flat-files-connection-manager.md)|[多個一般檔案連接管理員編輯器 &#40;一般頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;資料行頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [多個一般檔案連接管理員編輯器 &#40;進階頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [多個一般檔案連線管理員編輯器 &#40;預覽頁面&#41;](../../integration-services/connection-manager/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[FTP 連線管理員](../../integration-services/connection-manager/ftp-connection-manager.md)|[FTP 連線管理員編輯器](../../integration-services/connection-manager/ftp-connection-manager-editor.md)|  
    |[HTTP 連線管理員](../../integration-services/connection-manager/http-connection-manager.md)|[HTTP 連線管理員編輯器 &#40;伺服器頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)<br /><br /> [HTTP 連接管理員編輯器 &#40;Proxy 頁面&#41;](../../integration-services/connection-manager/http-connection-manager-editor-proxy-page.md)|  
    |[MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)|[MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)|  
    |[ODBC 連線管理員](../../integration-services/connection-manager/odbc-connection-manager.md)|[ODBC 連線管理員 UI 參考](../../integration-services/connection-manager/odbc-connection-manager-ui-reference.md)|  
    |[OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)|[設定 OLE DB 連線管理員](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)|  
    |[SMO 連線管理員](../../integration-services/connection-manager/smo-connection-manager.md)|[SMO 連線管理員編輯器](../../integration-services/connection-manager/smo-connection-manager-editor.md)|  
    |[SMTP 連線管理員](../../integration-services/connection-manager/smtp-connection-manager.md)|[SMTP 連線管理員編輯器](../../integration-services/connection-manager/smtp-connection-manager-editor.md)|  
    |[SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|[SQL Server Compact Edition 連線管理員編輯器 &#40;連接頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [SQL Server Compact Edition 連線管理員編輯器 &#40;全部頁面&#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[WMI 連線管理員](../../integration-services/connection-manager/wmi-connection-manager.md)|[WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)|  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="related-content"></a>相關內容  
  
-   technet.microsoft.com 上的影片： [沿用 Microsoft Attunity Connector for Oracle 來增強封裝效能](https://technet.microsoft.com/sqlserver/gg598963.aspx)  
  
-   social.technet.microsoft.com 上的 Wiki 文章： [SSIS 連接性](https://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)   
  
-   blogs.msdn.com 上的部落格文章： [從 SSIS 連接至 MySQL](https://go.microsoft.com/fwlink/?LinkId=217669)。  
  
-   blogs.msdn.com 上的技術文章： [擷取及載入 SQL Server Integration Services 中的 SharePoint 資料](https://go.microsoft.com/fwlink/?LinkId=247826)。  
  
-   support.microsoft.com 上的技術文章：[在 SSIS 中使用 Oracle 連線管理員時收到 "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" 錯誤訊息](https://go.microsoft.com/fwlink/?LinkId=233696)。  
  
  
