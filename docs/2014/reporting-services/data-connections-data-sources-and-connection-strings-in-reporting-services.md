---
title: Reporting Services 中的資料連線、資料來源和連接字串 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], data sources
- reports [Reporting Services], data
- expressions [Reporting Services], data sources
- data sources [Reporting Services], connections
- connection strings [Reporting Services]
- shared data sources [Reporting Services]
- Reporting Services, data sources
- logins [Reporting Services]
ms.assetid: 4d8f0ae1-102b-4b3d-9155-fa584c962c9e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8147471dc662b651ac9c99cc9290a383cc235ee8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891567"
---
# <a name="data-connections-data-sources-and-connection-strings-in-reporting-services"></a>Data Connections, Data Sources, and Connection Strings in Reporting Services
  若要在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表中包括資料，您必須先建立「資料來源」 與「資料集」。 本主題說明資料來源的類型、如何建立資料來源，以及與資料來源認證相關的重要資訊。 資料來源包括資料來源類型、連接資訊，以及要使用的認證類型。 資料來源有兩種類型：內嵌和共用。 內嵌資料來源是定義在報表中，而且只能供該報表使用。 共用資料來源則與報表分開定義，而且可以供多個報表使用。 如需詳細資訊，請參閱[內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md) 和[內嵌和共用資料集 &#40;報表產生器及 SSRS&#41;](report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)。  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 原生模式 &#124; [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint 模式|  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  

  
##  <a name="bkmk_data_sources"></a> 內嵌與共用資料來源  
 內嵌與共用資料來源之間的差異在於建立、儲存和管理的方式。  
  
-   在報表設計師中，您可以將內嵌或共用資料來源建立成 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 專案的一部分。 您可以控制要在本機使用它們進行預覽，還是將它們當做專案的一部分部署至報表伺服器或 SharePoint 網站。 您可以使用已經安裝在電腦以及報表伺服器或 SharePoint 網站 (部署報表的所在位置) 上的自訂資料延伸模組。  
  
     系統管理員可以安裝與設定其他資料處理延伸模組以及 .NET Framework 資料提供者。 如需詳細資訊，請參閱[資料處理延伸模組與 .NET Framework Data Providers &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)。  
  
     開發人員可以使用 <xref:Microsoft.ReportingServices.DataProcessing> API 建立資料處理延伸模組，以支援其他類型的資料來源。  
  
-   在報表產生器中，您可以瀏覽至報表伺服器或 SharePoint 網站，然後選取共用資料來源或在報表中建立內嵌資料來源。 您無法在報表產生器中建立共用資料來源。 您無法在報表產生器中使用自訂資料延伸模組。  
  
##  <a name="bkmk_DataConnections"></a> 內建的資料延伸模組  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 中預設的資料延伸模組包括下列資料連接類型：  
  
-   Microsoft SQL Server  
  
-   Microsoft SQL Server Analysis Services  
  
-   Microsoft SharePoint 清單  
  
-   [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]  
  
-   Microsoft SQL Server Parallel Data Warehouse  
  
-   OLE DB  
  
-   Oracle  
  
-   SAP NetWeaver BI  
  
-   Hyperion Essbase  
  
-   Teradata  
  
-   XML  
  
-   ODBC  
  
-   適用于 Power View 的 Microsoft BI 語義模型:在已針對 PowerPivot 圖庫和[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]設定的 SharePoint 網站上, 可以使用此資料來源類型。 此資料來源類型僅用於 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] 簡報。 如需詳細資訊，請參閱 [建立 Power View 的完整 BI 語意表格式模型](https://technet.microsoft.com/video/building-the-perfect-bi-semantic-tabular-models-for-power-view.aspx)。  
  
 如需 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 支援之資料來源與版本的完整清單，請參閱 [Reporting Services 支援的資料來源 &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
##  <a name="bkmk_create_data_source"></a>建立資料來源  
 若要建立資料來源，您必須擁有下列資訊：  
  
-   **資料來源類型**連線類型, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]例如。 請從連接類型的下拉式清單中選擇此值。  
  
-   **連接資訊** 連接資訊包括資料來源的名稱與位置，以及每個資料提供者專屬的連接屬性。 *「連接字串」* (Connection String) 是連接資訊的文字表示。 例如，如果資料來源是 SQL Server 資料庫，您就可以指定資料庫的名稱。 若是內嵌的資料來源，您也可以撰寫以運算式為基礎的連接字串，在執行階段接受評估。 如需詳細資訊，請參閱本主題稍後的 [以運算式為基礎的連接字串](#bkmk_Expressions_in_connection_strings) 。  
  
-   **認證** 您可以提供存取資料所需的認證。 資料來源擁有者必須已經授與您適當的權限，您才能同時存取資料來源及資料來源上的特定資料。 例如，若要連接到網路伺服器上所安裝的 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 範例資料庫，您必須擁有連接伺服器的權限，以及存取資料庫的唯讀權限。  
  
    > [!NOTE]  
    >  根據設計，認證會與資料來源分開管理。 在本機系統上用於預覽報表的認證可能與檢視已發行之報表所需的認證不同。 將資料來源儲存至報表伺服器或 SharePoint 網站之後，您可能必須變更認證，才能從該位置工作。 如需詳細資訊，請參閱＜ [資料來源的認證](#bkmk_credentials)＞。  
  
> [!NOTE]  
>  當您建立內嵌的資料來源中報表[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，您必須在 [方案總管] 或 [報表資料] 窗格中，但不是在[伺服器總管] 中的報表設計師中建立資料來源。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 報表設計師不支援[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]建立在[伺服器總管] 中的資料來源。  
  
 [報表資料] 窗格會顯示內嵌資料來源以及已經加入至報表之共用資料來源的參考。 在報表產生器中，共用資料來源參考會指向報表伺服器或 SharePoint 網站上的共用資料來源。 在報表設計師中，共用資料來源參考會指向 [方案總管] 中 [共用資料來源] 資料夾底下的共用資料來源。  
  
##  <a name="bkmk_credentials"></a>資料來源的認證  
 根據設計，認證可以與連接資訊分開儲存和管理。 認證是用來建立資料來源、執行資料集查詢，以及預覽報表。  
  
> [!NOTE]  
>  我們建議您不要在資料來源的連接屬性中加入登入資訊，例如登入名稱和密碼。 請盡可能使用共用資料來源搭配預存認證。 在撰寫環境中，當您建立資料連接或執行資料集查詢時，請使用 **[資料來源]** 對話方塊的 [認證] 頁面來輸入認證。  
  
 您針對從電腦進行資料存取所輸入的認證會安全地儲存在本機專案組態檔中，而且是該電腦專用的。 如果您將專案檔案複製到其他電腦，則必須重新定義資料來源的認證。  
  
 當您將報表部署至報表伺服器或 SharePoint 網站時，其內嵌和共用資料來源就會分開管理。 從電腦存取資料所需的資料來源認證可能與報表伺服器存取資料所需的認證不同。  
  
 ![注意](media/rs-fyinote.png "注意")最好的作法是在發行報表之後, 確認資料來源連接是否繼續連接成功。 如果您需要變更認證，可以直接在報表伺服器上進行修改。  
  
 若要變更報表所使用的資料來源, 您可以在原生模式中修改報告屬性, 報表管理員或從 SharePoint 模式的文件庫。 如需詳細資訊，請參閱下列內容：  
  
-   [將認證儲存在 Reporting Services 資料來源中](report-data/store-credentials-in-a-reporting-services-data-source.md)[將認證儲存在 Reporting Services 資料來源中](report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
-   [指定報表資料來源的認證及連線資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
-   [為自訂資料處理延伸模組指定連線](report-data/specify-connections-for-custom-data-processing-extensions.md)  
  
-   [在報表產生器中指定認證](../../2014/reporting-services/specify-credentials-in-report-builder.md)  
  
-   [新增及驗證資料連線或資料來源&#40;報表產生器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
##  <a name="bkmk_connection_examples"></a> 一般連接字串範例  
 連接字串是資料提供者之連接屬性的文字表示。 下表列出各種資料連接類型之連接字串的範例。  
  
|**資料來源**|**範例**|**描述**|  
|---------------------|-----------------|---------------------|  
|本機伺服器上的 SQL Server 資料庫|`data source="(local)";initial catalog=AdventureWorks`|將資料來源類型設定為 `Microsoft SQL Server`。 如需詳細資訊，請參閱 [SQL Server 連接類型 &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)。|  
|本機伺服器上的 SQL Server 資料庫|`data source="(local)";initial catalog=AdventureWorks`|將資料來源類型設定為 `Microsoft SQL Server`。|  
|SQL Server 執行個體<br /><br /> database|`Data Source=localhost\MSSQL10_50.InstanceName; Initial Catalog=AdventureWorks`|將資料來源類型設定為 `Microsoft SQL Server`。|  
|SQL Server Express 資料庫|`Data Source=localhost\MSSQL10_50.SQLEXPRESS; Initial Catalog=AdventureWorks`|將資料來源類型設定為 `Microsoft SQL Server`。|  
|[!INCLUDE[ssSDS](../includes/sssds-md.md)]在雲端中|`Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True`|將資料來源類型設定為 `Windows Azure SQL Database`。 如需詳細資訊，請參閱 [SQL Azure 連接類型 &#40;SSRS&#41;](report-data/sql-azure-connection-type-ssrs.md)。|  
|SQL Server 平行資料倉儲|`HOST=<IP address>;database= AdventureWorks; port=<port>`|將資料來源類型設定為 `Microsoft SQL Server Parallel Data Warehouse`。 如需詳細資訊，請參閱 [SQL Server 平行資料倉儲連接類型 &#40;SSRS&#41;](report-data/sql-server-parallel-data-warehouse-connection-type-ssrs.md)。|  
|本機伺服器上的 Analysis Services 資料庫|`data source=localhost;initial catalog=Adventure Works DW`|將資料來源類型設定為 `Microsoft SQL Server Analysis Services`。 如需詳細資訊，請參閱 [MDX 的 Analysis Services 連線類型 &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-mdx-ssrs.md) 或 [DMX 的 Analysis Services 連線類型 &#40;SSRS&#41;](report-data/analysis-services-connection-type-for-dmx-ssrs.md)。|  
|具有 Sales 檢視方塊的 Analysis Services 表格式模型資料庫|`Data source=<servername>;initial catalog= Adventure Works DW;cube='Sales'`|將資料來源類型設定為 `Microsoft SQL Server Analysis Services`。 在 cube= 設定中指定檢視方塊名稱。 如需詳細資訊，請參閱 [檢視方塊 &#40;SSAS 表格式&#41;](https://docs.microsoft.com/analysis-services/tabular-models/perspectives-ssas-tabular)。|  
|在原生模式設定之報表伺服器上的報表模型資料來源|`Server=http://myreportservername/reportserver; datasource=/models/Adventure Works`|指定報表伺服器或文件庫 URL 以及報表伺服器資料或文件庫資料夾命名空間中已發行模型的路徑。
|在 SharePoint 整合模式設定之報表伺服器上的報表模型資料來源|`Server=http://server; datasource=http://server/site/documents/models/Adventure Works.smdl`|指定報表伺服器或文件庫 URL 以及報表伺服器資料或文件庫資料夾命名空間中已發行模型的路徑。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器|`provider=MSOLAP.2;data source=<remote server name>;initial catalog=FoodMart 2000`|將資料來源類型設定為 `OLE DB Provider for OLAP Services 8.0`。<br /><br /> 如果將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 屬性設定為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，則可以加快 `ConnectTo` 2000 `8.0` 資料來源的連接。 若要設定這個屬性，請使用 **[連接屬性]** 對話方塊的 **[進階屬性]** 索引標籤。|  
|Oracle 伺服器|`data source=myserver`|將資料來源類型設定為 `Oracle`。 Oracle 用戶端工具必須安裝在報表設計師電腦和報表伺服器上。 如需詳細資訊，請參閱 [Oracle 連接類型 &#40;SSRS&#41;](report-data/oracle-connection-type-ssrs.md)。|  
|SAP NetWeaver BI 資料來源|`DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla`|將資料來源類型設定為 `SAP NetWeaver BI`。 如需詳細資訊，請參閱 [SAP NetWeaver BI 連接類型 &#40;SSRS&#41;](report-data/sap-netweaver-bi-connection-type-ssrs.md)。|  
|Hyperion Essbase 資料來源|`Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample`|將資料來源類型設定為 `Hyperion Essbase`。 如需詳細資訊，請參閱 [Hyperion Essbase 連接類型 &#40;SSRS&#41;](report-data/hyperion-essbase-connection-type-ssrs.md)。|  
|Teradata 資料來源|`data source=`\<NNN>.\<NNN>.\<NNN>.\<NNN>`;`|將資料來源類型設定為 `Teradata`。 連接字串是四個欄位形式的網際網路通訊協定 (IP) 位址，其中每個欄位都可以是 1 到 3 位數。 如需詳細資訊，請參閱 [Teradata 連線類型 &#40;SSRS&#41;](report-data/teradata-connection-type-ssrs.md)。|  
|XML 資料來源, Web 服務|`data source=http://adventure-works.com/results.aspx`|將資料來源類型設定為 `XML`。 連接字串是支援 Web 服務定義語言 (WSDL) 之 Web 服務的 URL。 如需詳細資訊，請參閱 [XML 連線類型 &#40;SSRS&#41;](report-data/xml-connection-type-ssrs.md)。|  
|XML 資料來源、XML 文件|`http://localhost/XML/Customers.xml`|將資料來源類型設定為 `XML`。 連接字串是 XML 文件的 URL。|  
|XML 資料來源, 內嵌 XML 文件|*Empty*|將資料來源類型設定為 `XML`。 XML 資料內嵌在報表定義中。|  
  
如果無法使用 `localhost` 連接到報表伺服器，請檢查 TCP/IP 通訊協定的網路通訊協定是否已啟用。 如需詳細資訊，請參閱 [Configure Client Protocols](../database-engine/configure-windows/configure-client-protocols.md)。  
  
##  <a name="bkmk_special_password_characters"></a> 密碼中的特殊字元  
 如果您設定 ODBC 或 SQL 資料來源以提示密碼或將密碼包含在連接字串中，則當使用者輸入含有特殊字元 (例如：標點符號) 的密碼時，某些基礎資料來源驅動程式無法驗證這些特殊字元。 當您處理報表時，訊息「不是有效密碼」可能會指出此問題。 如果無法變更密碼，您可以洽詢資料庫管理員，將適當的認證儲存在伺服器上，做為系統 ODBC 資料來源名稱 (DSN) 的一部分。 如需詳細資訊，請參閱 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] SDK 文件集中的＜OdbcConnection.ConnectionString＞。  
  
##  <a name="bkmk_Expressions_in_connection_strings"></a> 以運算式為基礎的連接字串  
 以運算式為基礎的連接字串是在執行階段進行評估。 例如，您可以將資料來源指定為參數，包括連接字串中的參數參考，並允許使用者選擇報表的資料來源。 例如，假設有一家跨國企業，在許多國家 (地區) 有資料伺服器。 執行銷售報表的使用者可以在執行報表之前，使用以運算式為基礎的連接字串，來選取特定國家 (地區) 的資料來源。  
  
 下列範例說明在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 連接字串中，使用資料來源運算式。 本範例假設您已經建立一個名為 `ServerName`的報表參數：  
  
```  
="data source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks"  
```  
  
 資料來源運算式是在執行階段，或者在預覽報表時處理。 運算式必須以 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]撰寫。 定義資料來源運算式時，請使用下列指導方針：  
  
-   使用靜態連接字串設計報表。 靜態連接字串是指未透過運算式設定的連接字串 (例如，您遵循建立報表特定或共用資料來源的步驟執行時，所定義的就是靜態連接字串)。 使用靜態連接字串可以讓您連接到報表設計師中的資料來源，以便取得建立報表所需的查詢結果。  
  
-   定義資料來源連接時，請勿使用共用資料來源。 您不能在共用資料來源中使用資料來源運算式。 您必須為報表定義內嵌的資料來源。  
  
-   分開指定認證與連接字串。 您可以使用預存認證、提示認證或整合式安全性。  
  
-   加入報表參數，以指定資料來源。 針對參數值，您可以提供靜態可用的值清單 (在此情況下，可用的值應為可以搭配報表使用的資料來源)，或者定義在執行階段擷取資料來源清單的查詢。  
  
-   請確定資料來源清單共用相同的資料庫結構描述。 所有的報表設計都是從結構描述資訊開始。 如果用於定義報表的結構描述，和報表在執行階段使用的實際結構描述不符，報表可能不會執行。  
  
-   發行報表之前，請以運算式取代靜態連接字串。 等到設計好報表之後，再以運算式取代靜態連接字串。 一旦使用運算式，就不能在報表設計師中執行查詢。 此外，[報表資料] 窗格中的欄位清單與 [參數] 清單也不會自動更新。  
  
## <a name="see-also"></a>另請參閱  
 [內嵌和共用資料連接或資料來源 &#40;報表產生器及 SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [管理報表資料來源](report-data/manage-report-data-sources.md)   
 [資料來源屬性對話方塊、認證](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)   
 [共用資料來源屬性對話方塊、認證](../../2014/reporting-services/shared-data-source-properties-dialog-box-credentials.md)   
 [建立、修改和刪除共用資料來源 &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [設定部署屬性 &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md)   
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [新增及驗證資料連線或資料來源&#40;報表產生器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
