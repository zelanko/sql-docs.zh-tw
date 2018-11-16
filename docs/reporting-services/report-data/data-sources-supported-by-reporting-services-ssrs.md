---
title: Reporting Services (SSRS) 支援的資料來源 | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- SQL Server data processing extension [Reporting Services]
- XML data processing extension [Reporting Services]
- reports [Reporting Services], data
- data processing extensions [Reporting Services], data sources
- Oracle [Reporting Services]
- OLE DB data processing extension
- data sources [Reporting Services], about data sources
- ODBC data processing extension
- Reporting Services, data sources
ms.assetid: 9d11d055-a3be-45aa-99a7-46447a94ed42
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a08ece8729125bf1cc60bb96385d58ba5c3a6ee
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813861"
---
# <a name="data-sources-supported-by-reporting-services-ssrs"></a>Reporting Services (SSRS) 支援的資料來源
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會透過使用資料處理延伸模組的模組化與可延伸資料層，擷取資料來源中的報表資料。 若要擷取資料來源中的報表資料，您必須選取資料處理延伸模組，其同時支援資料來源的類型 (也就是在資料來源上執行的軟體版本) 與資料來源平台 (32 位元或 64 位元 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)])。  
  
 當您部署 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]時，會同時在報表撰寫用戶端與報表伺服器上，自動安裝並註冊一組資料處理延伸模組，以提供各種資料來源類型的存取權。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會安裝下列資料來源類型：  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] for MDX、DMX、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]及表格式模型  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
  
-   Oracle  
  
-   SAP BW 
  
-   [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 清單  
  
-   Teradata  
  
-   OLE DB  
  
-   ODBC  
  
-   XML  
  
 此外，自訂資料處理延伸模組與標準的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者可由系統管理員安裝並註冊。 若要處理與檢視報表，資料處理延伸模組和資料提供者必須在報表伺服器上安裝並註冊；若要預覽報表，資料處理延伸模組和資料提供者則必須在報表撰寫用戶端上安裝並註冊。 資料處理延伸模組和資料提供者必須在所安裝的平台上原生編譯。 若您使用 SOAP Web 服務以程式設計的方式部署資料來源，則必須定義資料來源延伸模組。 使用 **RSReportDesigner.config** 檔的資料延伸模組值。 根據預設，這個檔案位於下列資料夾中︰  
  
```  
<drive letter>\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies  
```  
  
 例如， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料延伸模組是 OLEDB-MD。  
  
 許多協力廠商的標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者可從 [Microsoft 下載中心](https://go.microsoft.com/fwlink/?linkid=51456) 以及協力廠商網站下載。 您也可以搜尋 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 公用論壇中，有關協力廠商資料提供者的資訊。  
  
> [!NOTE]  
>  標準的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者不一定支援由 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組所提供的所有功能。 此外，有些 OLE DB 資料提供者和 ODBC 驅動程式可用來撰寫與預覽報表，但其設計不是用來支援在報表伺服器上發行的報表。 例如，報表伺服器不支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Jet。 如需詳細資訊，請參閱[資料處理延伸模組與 .NET Framework Data Providers &#40;SSRS&#41;](../../reporting-services/report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)。  
  
 如需有關自訂資料處理延伸模組的詳細資訊，請參閱＜ [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)＞。 如需標準 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的詳細資訊，請參閱 <xref:System.Data> 命名空間。   
  
## <a name="platform-support-for-report-data-sources"></a>報表資料來源的平台支援  
 您可以在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 部署中使用的資料來源會隨著 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 版本與平台而有所不同。 如需功能的詳細資訊，請參閱 [SQL Server 2016 版本支援的 Reporting Services 功能](../../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。 此主題稍後的資料表會依版本及平台，提供關於支援之資料來源的詳細資訊。  
  
 關於 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料來源的平台考量，則會分別針對報表撰寫用戶端與報表伺服器。  
  
### <a name="on-the-report-authoring-client"></a>在報表撰寫用戶端上  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 是 32 位元應用程式。 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 以 Itanium 為基礎的平台不支援。 若要在 x64 平台上，編輯和預覽報表設計師中的報表，您必須將 32 位元的資料提供者安裝在 (x86) 的平台目錄中。  
  
### <a name="on-the-report-server"></a>在報表伺服器上  
 當您將報表部署至 64 位元的報表伺服器時，報表伺服器上必須已經安裝以 64 位元原生編譯的資料提供者。 不支援在 64 位元介面中包裝 32 位元的資料提供者。 如需詳細資訊，請查詢資料提供者的文件。  
  
## <a name="supported-data-sources"></a>支援的資料來源  
 下表列出您可以用來擷取報表資料集與報表模型之資料的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 資料處理延伸模組和資料提供者。 如需有關延伸模組或資料提供者的詳細資訊，請按一下第二欄中的連結。 相關的資料表資料行描述如下：  
  
-   報表資料來源：所存取之資料類型；例如，關聯式資料庫、多維度資料庫、一般檔案或 XML。 此欄為「 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可以用於報表的資料類型為何？」這個問題的答案。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料來源類型：當您在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中定義資料來源時，您可以在下拉式清單中看到的其中一種資料來源類型。 此清單會從已安裝並註冊的 DPE 和資料提供者擴展。 此欄為「當我建立報表資料來源時，可以從下拉式清單中選取哪種資料來源類型？」這個問題的答案。  
  
-   資料處理延伸模組/資料提供者的名稱：對應選取之 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料來源類型的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組或其他資料提供者。 此欄為「當我選取資料來源類型時，要使用哪個對應的資料處理延伸模組或資料提供者？」這個問題的答案。  
  
-   基礎資料提供者版本 (選擇性)：某些資料來源類型支援一種以上的資料提供者。 這些可能是相同提供者的不同版本，或是依協力廠商針對資料提供者類型的不同實作。 提供者名稱通常會在已設定資料來源之後，出現在連接字串中。 此欄為「選取資料來源類型後，我可以在 **[連接屬性]** 對話方塊中選取哪個資料提供者？」這個問題的答案。  
  
-   資料來源 \<平台>：目標資料來源的資料處理延伸模組或資料提供者所支援的資料來源平台。 此欄為「這個資料處理延伸模組或資料提供者，可以從此類型平台的資料來源擷取資料嗎？」這個問題的答案。  
  
-   資料來源的版本：DPE 或資料提供者支援的目標資料來源版本。 此欄為「這個資料處理延伸模組或資料提供者，可以從此版本的資料來源擷取資料嗎？」這個問題的答案。  
  
-   RS \<平台>：報表伺服器與報表撰寫用戶端的平台，您可以在該處安裝自訂的 DPE 或資料提供者。 任何 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安裝所包含的內建 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]資料處理延伸模組。 自訂的資料處理延伸模組或 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者必須原始就針對特定平台編譯。 此欄為「這個資料處理延伸模組或資料提供者，可以安裝在此類型的平台上嗎？」這個問題的答案。  
  
###  <a name="DataSourcesTable"></a> 資料來源的類型  
  
|來源<br /><br /> 報表資料|Reporting Services 資料來源類型|資料處理延伸模組/資料提供者的名稱|基礎資料提供者版本<br /><br /> (選擇性)|data<br /><br /> 來源<br /><br /> x86 平台|資料<br /><br /> 來源<br /><br /> x64 平台|資料來源的版本|RS<br /><br /> x86 平台|RS<br /><br /> x64 平台|  
|-------------------------------|-----------------------------------------|------------------------------------------------------|-------------------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|-------------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫|[Microsoft SQL Server](#MicrosoftSQLServer)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.SqlClient|Y|Y|SQL Server 2008 及更新版本。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫|OLEDB|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.OledbClient|Y|Y|SQL Server 2008 及更新版本。|Y|Y|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫|[ODBC](#ODBC)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.OdbcClient|Y|Y|SQL Server 2008 及更新版本。|Y|Y|  
|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|[Microsoft Azure SQL Database](#Azure)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.SqlClient|不適用|N/A|[!INCLUDE[ssSDS](../../includes/sssds-md.md)]|Y|Y|
|SQL 資料倉儲|[Microsoft Azure SQL Database](#Azure)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.SqlClient|不適用|不適用|SQL 資料倉儲|Y|Y| 
|[!INCLUDE[ssDW](../../includes/ssdw-md.md)] 應用裝置|[Microsoft Parallel Data Warehouse](#PWD)|已被取代的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|不適用|不適用|不適用|[!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|N|N|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度資料庫|[Microsoft SQL Server Analysis Services](#AnalysisServices)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|使用 ADOMD.NET|Y|Y|SQL Server 2008 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 及更新版本|Y|Y|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度資料庫|OLEDB|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充 System.Data.OledbClient<br /><br /> 10.0 版|Y|Y|SQL Server 2008 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Y|Y|   
|SharePoint 清單|[Microsoft SharePoint 清單](#SharePointList)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|從 Lists.asmx 或 SharePoint 物件模型 API 介面取得資料。<br /><br /> 請參閱 [注意事項](#SharePointList)。|N|Y|SharePoint 2013 產品及更新版本|Y|Y|   
|XML|[XML](#XML)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|XML 資料來源沒有平台相依性。|不適用|不適用|[!INCLUDE[vstecwebservices](../../includes/vstecwebservices-md.md)] 或文件|Y|Y|  
|報表伺服器模型|報表模型|已發行之 SMDL 檔案的已被取代 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|模型的資料來源使用內建的資料處理延伸模組。<br /><br /> 以 Oracle 為基礎的模型需要 Oracle 用戶端元件。<br /><br /> 以 Teradata 為基礎的模型需要來自 Teradata 的 .NET Data Provider for Teradata。<br /><br /> 請參閱平台支援的 Teradata 文件集。|不適用|不適用|模型可以從以下版本建立：[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本。<br /><br /> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<br /><br /> Oracle 9.2.0.3 或更新版本<br /><br /> Teradata V14、v13、v12 和 v6.2|N|N|  
|SAP 多維度資料庫|SAP BW|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|請參閱平台支援的 SAP 文件集。|不適用|不適用|SAP BW 7.0-7.5|Y|不適用|  
|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)]|[Hyperion Essbase](#Hyperion)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|請參閱平台支援的 Hyperion 文件集。|Y|不適用|[!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 9.3.1|Y|不適用|  
|Oracle 關聯式資料庫|[Oracle](#OracleClient)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|需要 Oracle 用戶端元件 12c 或更高版本。|Y|不適用|Oracle 11g、11g R2、12c|Y|Y|  
|Teradata 關聯式資料庫|[Teradata](#Teradata)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|擴充來自 Teradata 的 .NET Data Provider for Teradata。<br /><br /> 需要來自 Teradata 的 .NET Data Provider for Teradata。<br /><br /> 請參閱平台支援的 Teradata 文件集。|Y|不適用|Teradata v15<br /><br />Teradata v14<br /><br /> Teradata v13|Y|N|  
|DB2 關聯式資料庫|自訂的已註冊資料延伸模組名稱||2004 Host Integration (HI) Server<br /><br /> 請參閱 [HI Server 文件](https://msdn.microsoft.com/library/gg241192\(v=bts.10\).aspx)(英文)。|Y|不適用|N/A|Y|N|  
|一般 OLE DB 資料來源|OLEDB|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|支援 OLE DB 的任何資料來源。<br /><br /> 請參閱平台支援的資料來源文件。|Y|不適用|支援 OLE DB 的任何資料來源。 請參閱 [注意事項](#OLEDBStandard)。|Y|不適用|  
|一般 ODBC 資料來源|[ODBC](#ODBCGeneric)|內建的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組|支援 ODBC 的任何資料來源。<br /><br /> 請參閱平台支援的資料來源文件。|Y|不適用|支援 ODBC 的任何資料來源。 請參閱 [注意事項](#ODBCGeneric)。|Y|Y|  
  
 如需使用外部資料來源的資訊，請參閱[從外部資料來源加入資料 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)。  
  
 許多標準的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者都可以從協力廠商取得。 如需詳細資訊，請搜尋協力廠商的網站或論壇。  
  
 若要安裝並註冊自訂的資料處理延伸模組或標準的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者，您必須參考資料提供者的參考文件。 如需詳細資訊，請參閱[註冊標準的 .NET Framework Data Provider &#40;SSRS&#41;](../../reporting-services/report-data/register-a-standard-net-framework-data-provider-ssrs.md)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
## <a name="reporting-services-data-processing-extensions"></a>Reporting Services 資料處理延伸模組  
 下列資料處理延伸模組會隨 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]自動安裝。 如需詳細資訊或要確認安裝，請參閱 [RSReportDesigner 組態檔](../../reporting-services/report-server/rsreportdesigner-configuration-file.md) 和 [RsReportServer.config 組態檔](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)。  
  
> [!NOTE]  
>  目前並不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料處理延伸模組。  
  
 如需報表產生器支援之資料處理延伸模組的詳細資訊，請參閱 msdn.microsoft.com 上 [報表產生器文件](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) 中的 [報表產生器中的資料連接、資料來源及連接字串](https://go.microsoft.com/fwlink/?LinkId=154494) 。  
  
###  <a name="MicrosoftSQLServer"></a> Microsoft SQL Server 資料處理延伸模組  
 資料來源類型 **Microsoft SQL Server** 會包裝與擴充 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此資料處理延伸模組是原生針對 x86 與 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]平台編譯，並在這些平台上執行。  
  
 在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]中，與此資料延伸模組相關聯的查詢設計工具是 Visual Database Tools 設計工具。 如果您在圖形化模式下使用查詢設計工具，則會分析查詢，而且可能會重寫查詢。 當您想要控制用於查詢的確切 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法時，請使用以文字為基礎的查詢設計工具。 如需詳細資訊，請參閱 [圖形化查詢設計工具使用者介面](../../reporting-services/report-data/graphical-query-designer-user-interface.md)。  
  
 如需詳細資訊，請參閱 [SQL Server 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)。  
  
 在報表產生器中，與此資料延伸模組相關聯的查詢設計工具是關聯式查詢設計工具。 
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="Azure"></a> Microsoft Azure SQL Database 處理延伸模組  
 資料來源類型 **Microsoft Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]** 會包裝與擴充 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]中，與此資料延伸模組相關聯的圖形化查詢設計工具是關聯式查詢設計工具，不是與 **Microsoft SQL Server** 資料來源類型搭配使用的 Visual Database Tools 設計工具。  
  
 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]會自動區分 **Microsoft Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)]** 和 **Microsoft SQL Server** 資料來源類型，並開啟與資料來源類型相關聯的圖形化查詢設計工具。  
  
 如果您在圖形化模式下使用查詢設計工具，則會分析查詢，而且可能會重寫查詢。 以文字為基礎的查詢設計工具也可用來編寫查詢。 當您想要控制用於查詢的確切 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法時，請使用以文字為基礎的查詢設計工具。   
  
 從 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]、SQL 資料倉儲和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擷取資料的做法非常類似，但有幾項需求只適用於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。 如需詳細資訊，請參閱 [SQL Azure 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sql-azure-connection-type-ssrs.md)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="PWD"></a> Microsoft SQL Server 平行資料倉儲資料處理延伸模組  
此資料來源已被取代。 請使用 SQL Server 資料來源類型來連接到 Microsoft 分析平台 (APS)。
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="AnalysisServices"></a> Microsoft SQL Server Analysis Services 資料處理延伸模組  
 當您選取資料來源類型 **Microsoft SQL Server Analysis Services**時，您選取的是可擴展 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 此資料處理延伸模組是原生針對 x86 與 x64 平台編譯，並在這些平台上執行。  
  
 此資料提供者使用 ADOMD.NET 物件模型來建立使用 XML for Analysis (XMLA) 1.1 版的查詢。 這些結果會當做扁平化資料列集傳回。 如需詳細資訊，請參閱 [MDX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)、[DMX 的 Analysis Services 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)、[Analysis Services MDX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-mdx-query-designer-user-interface.md)和 [Analysis Services DMX 查詢設計工具使用者介面](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)。  
  
 連接至 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源時， [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料處理延伸模組支援多重值的參數，而且會將資料格與成員屬性對應至 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]所支援的擴充屬性。 如需詳細資訊，請參閱 [Analysis Services 資料庫的擴充欄位屬性 &#40;SSRS&#41;](../../reporting-services/report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)。  
  
 您也可以從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料來源建立模型。  
  
###  <a name="OLEDBAll"></a> OLE DB Data Processing Extension  
 OLE DB 資料處理延伸模組需要根據您要在報表中使用的資料來源版本，選擇其他資料提供者層。 如果您不選取特定的資料提供者，則會提供預設值。 透過從 [資料來源] 或 [共用資料來源] 對話方塊的 [編輯] 按鈕存取的 [連接屬性] 對話方塊，選擇特定的資料提供者。  
  
 如需 OLE DB 相關聯之查詢設計工具的詳細資訊，請參閱 [圖形化查詢設計工具使用者介面](../../reporting-services/report-data/graphical-query-designer-user-interface.md)。 如需有關 OLE DB 提供者之特定支援的詳細資訊，請參閱 [知識庫中的](https://support.microsoft.com/default.aspx/kb/811241) Visual Studio .NET 設計工具支援 OLE DB 提供者特定資訊 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
####  <a name="OLEDBSQL"></a> OLE DB for SQL Server  
 當您選取資料來源類型 **OLE DB**時，您選取的是可擴展 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for OLE DB 的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料處理延伸模組。 此資料處理延伸模組是原生針對 x86 與 x64 平台編譯，並在這些平台上執行。  
  
 如需詳細資訊，請參閱 [OLE DB 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
#### <a name="ole-db-for-olap-70"></a>OLE DB for OLAP 7.0  
 不支援 OLE DB Provider for OLAP Services 7.0。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
####  <a name="OracleOLEDB"></a> OLE DB for Oracle  
 資料處理延伸模組 OLE DB for Oracle 不支援下列 Oracle 資料類型：BLOB、CLOB、NCLOB、BFILE、UROWID。  
  
 支援與位置有關的未指名參數。 此延伸模組不支援具名參數。 若要使用具名參數，請使用 [Oracle](#OracleClient) 資料處理延伸模組。  
  
 如需有關將 Oracle 設定為資料來源的詳細資訊，請參閱＜ [如何使用 Reporting Services 設定及存取 Oracle 資料來源](https://support.microsoft.com/kb/834305)＞(機器翻譯)。 如需其他權限設定的詳細資訊，請參閱 [知識庫中的](https://support.microsoft.com/kb/870668) 如何新增 NETWORK SERVICE 安全性主體的權限 [!INCLUDE[msCoName](../../includes/msconame-md.md)] (機器翻譯)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
####  <a name="OLEDBStandard"></a> OLE DB 標準的 .NET Framework 資料提供者  
 若要從支援 OLE DB [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的資料來源擷取資料，使用 **OLE DB** 資料來源類型，並選取預設的資料提供者，或從 **[連接字串]** 對話方塊中已安裝的資料提供者選取。  
  
> [!NOTE]  
>  雖然資料提供者可能支援在您的報表撰寫用戶端上預覽報表，但是並非所有 OLE DB 資料提供者的設計都支援在報表伺服器上發行的報表。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="ODBC"></a> ODBC Data Processing Extension  
 當您選取資料來源類型 **ODBC**時，您選取的是可擴展 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Data Provider for ODBC 的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料處理延伸模組。 此資料處理延伸模組是原生針對 x86 與 [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] 平台編譯，並在這些平台上執行。 使用此延伸模組連接至具有 ODBC 提供者的任何資料來源，並從中擷取資料。  
  
> [!NOTE]  
>  雖然資料提供者可能支援在您的報表撰寫用戶端上預覽報表，但是並非所有 ODBC 資料提供者的設計都支援在報表伺服器上發行的報表。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
####  <a name="ODBCGeneric"></a> ODBC 標準的 .NET Framework 資料提供者  
 若要從支援 ODBC [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 資料提供者的資料來源擷取資料，使用 **ODBC** 資料來源類型，並選取預設的資料提供者，或從 **[連接字串]** 對話方塊中已安裝的資料提供者選取。  
  
> [!NOTE]  
>  雖然資料提供者可能支援在您的報表撰寫用戶端上預覽報表，但是並非所有 ODBC 資料提供者的設計都支援在報表伺服器上發行的報表。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="OracleClient"></a> Oracle 資料處理延伸模組  
 當您選取資料來源類型 **Oracle** 時，您會選取直接使用 Oracle 資料提供者且不再經過 System.Data.OracleClien 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組。 若要從 Oracle 資料庫擷取報表資料，您的管理員必須安裝 Oracle 用戶端工具。 用戶端應用程式版本必須為 11g 或更新版本。 這些工具必須安裝在報表撰寫用戶端上，才可以預覽報表，以及在報表伺服器上檢視已發行的報表。  
 
若要安裝 Oracle 用戶端工具，您可以執行下列步驟。
 
1.  前往 [Oracle 的下載網站](https://www.oracle.com/us/products/tools/index-090165.html)
2.  下載 ODAC 12c Release 4 (12.1.0.2.4) for Windows (伺服器為 64bit，工具為 32bit)
3.  安裝 Data Provider for .NET 4
  
 此延伸模組支援具名參數。 若使用 Oracle 11g 或更新版本，則支援多重值的參數。 對於與位置有關的未指名參數，請搭配資料提供者 [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for Oracle 使用 OLE DB 資料處理延伸模組。 如需有關將 Oracle 設定為資料來源的詳細資訊，請參閱＜ [如何使用 Reporting Services 設定及存取 Oracle 資料來源](https://support.microsoft.com/kb/834305)＞(機器翻譯)。 如需其他權限設定的詳細資訊，請參閱 [知識庫中的](https://support.microsoft.com/kb/870668) 如何新增 NETWORK SERVICE 安全性主體的權限 [!INCLUDE[msCoName](../../includes/msconame-md.md)] (機器翻譯)。  
  
 您可以從具有多個輸入參數的預存程序擷取資料，但是預存程序必須只傳回一個輸出資料指標。 如需詳細資訊，請參閱＜ [使用 DataReader 擷取資料](https://go.microsoft.com/fwlink/?LinkId=81758)＞中的 Oracle 章節。  
  
 如需詳細資訊，請參閱 [Oracle 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)。 如需相關聯之查詢設計工具的詳細資訊，請參閱 [圖形化查詢設計工具使用者介面](../../reporting-services/report-data/graphical-query-designer-user-interface.md)。  
  
 您也可以根據 Oracle 資料庫建立模型。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="Teradata"></a> Teradata 資料處理延伸模組  
 當您選取資料來源類型 **Teradata**時，您選取的是可擴展 .NET Framework Data Provider for Teradata 的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 資料處理延伸模組。 若要從 Teradata 資料庫擷取報表資料，系統管理員必須在報表撰寫用戶端上安裝 .NET Framework Data Provider for Teradata，才能在用戶端上編輯和預覽報表，並在報表伺服器上檢視已發行的報表。  
  
 對於報表伺服器專案而言，沒有可用於此延伸模組的圖形化查詢設計工具。 您必須使用以文字為基礎的查詢設計工具來建立查詢。  
  
 下表顯示哪個版本的 .NET Data Provider for Teradata 支援定義在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]之報表定義中的資料來源：  
  
|[!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] 版本|Teradata 資料庫版本|.NET Framework Data Provider for Teradata 版本|  
|-----------------------------------|-------------------------------|-------------------------------------------------------|    
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|6.20|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|12.00|12.00.01|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|13.00|13.0.0.1|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|14.00|14.00.01| 
|SQL Server 2016|13.00|13.0.0.1|  
|SQL Server 2016|14.00|14.00.01|
|SQL Server 2016|15.00|15.00.01| 
  
 此延伸模組支援多重值參數。 您可以在 TEXT 查詢模式下使用 EXECUTE 命令指定查詢中的巨集。  
  
 如需詳細資訊，請參閱 [Teradata 連線類型 &#40;SSRS&#41;](../../reporting-services/report-data/teradata-connection-type-ssrs.md)。  
  
 您也可以根據 Teradata 資料庫建立模型。 如需詳細資訊，請參閱 Teradata 網站上的以下白皮書： [Microsoft SQL Server 2012 Reporting Services 和 Teradata Corporation](https://www.teradata.com/white-papers/Microsoft-SQL-Server-2012-Reporting-Services-and-Teradata-Corporation/?type=WP)(英文)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="SharePointList"></a> SharePoint 清單資料延伸模組  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 清單資料延伸，以便讓您使用 SharePoint 清單做為報表中的資料來源。 您可以從以下所列擷取清單資料：  
  
-   SharePoint Server 2016  

-   [!INCLUDE[SPS2013](../../includes/sps2013-md.md)]  
  
 SharePoint 清單資料提供者有三種實作方式。  
  
1.  從在 [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)]中的報表產生器或報表設計師等報表撰寫環境，或以原生模式設定的報表伺服器，清單資料是來自 SharePoint 網站的 Lists.asmx Web 服務。  
  
2.  在以 SharePoint 整合模式設定的報表伺服器上，清單資料來自對應的 Lists.asmx Web 服務或以程式設計方式呼叫 SharePoint API。 在這種模式中，您可以從 SharePoint 伺服器陣列擷取清單資料。  
  
3.  對於 [!INCLUDE[SPS2013](../../includes/sps2013-md.md)] 和 SharePoint Server 2016，適用於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SharePoint 技術的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 增益集可讓您從 SharePoint 網站的 Lists.asmx Web 服務擷取清單資料，或從屬於 SharePoint 伺服器陣列的 SharePoint 網站擷取清單資料。 這種情況也稱為 *「本機模式」* (Local Mode)，因為不需要報表伺服器。  
  
 您可以指定的認證是依照用戶端應用程式所使用的實作而定。 如需詳細資訊，請參閱 [SharePoint 清單連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/sharepoint-list-connection-type-ssrs.md)。  
  
###  <a name="XML"></a> XML 資料處理延伸模組  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包括 XML 資料處理延伸模組，因此您可以在報表中使用 XML 資料。 可以從 XML 文件、Web 服務或是可透過 URL 存取的網路架構應用程式來擷取這些資料。 如需詳細資訊，請參閱 [XML 連線類型 &#40;SSRS&#41;](../../reporting-services/report-data/xml-connection-type-ssrs.md)。 如需相關聯之查詢設計工具的詳細資訊，請參閱 [圖形化查詢設計工具使用者介面](../../reporting-services/report-data/graphical-query-designer-user-interface.md)中的＜以文字為基礎的查詢設計工具＞一節。 如需範例，請參閱 [Reporting Services：使用 XML 與 Web 服務資料來源](https://go.microsoft.com/fwlink/?LinkId=81654)。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="SAPBW"></a> SAP BW 資料處理延伸模組  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含資料處理延伸模組，可讓您在報表中使用來自 SAP BW 資料來源的資料。
  
 [返回資料來源資料表](#DataSourcesTable)  
  
###  <a name="Hyperion"></a> Hyperion Essbase Business Intelligence 資料處理延伸模組  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 包含資料處理延伸模組，可讓您從報表中的 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] 資料來源使用資料。  
  
 如需詳細資訊，請參閱 [Hyperion Essbase 連接類型 &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md)。 如需有關關聯之查詢設計工具的詳細資訊，請參閱＜ [Hyperion Essbase Query Designer User Interface](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md)＞。  
  
 如需有關 [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]的詳細資訊，請參閱＜ [使用 SQL Server 2005 Reporting Services 搭配 Hyperion Essbase](https://go.microsoft.com/fwlink/?LinkId=81970)＞。  
  
 [返回資料來源資料表](#DataSourcesTable)  
  
## <a name="see-also"></a>另請參閱  
 [資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [報表資料集 &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 更多問題嗎？ [試試 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  
