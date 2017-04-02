---
title: "使用 SQL Server 匯入和匯出精靈來匯入或匯出資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "匯出資料"
  - "對應檔案 [Integration Services]"
  - "SQL Server 匯入和匯出精靈"
  - "SSIS 封裝, 建立"
  - "封裝 [Integration Services], 複製"
  - "Integration Services 封裝, 建立"
  - "封裝 [Integration Services], 建立"
  - "SQL Server Integration Services 封裝，建立"
  - "匯入和匯出精靈"
  - "複製資料 [Integration Services]"
  - "匯入資料, SSIS 封裝"
  - "來源 [Integration Services], 複製資料"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# 使用 SQL Server 匯入和匯出精靈來匯入或匯出資料
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈是將資料從來源複製到目的地的簡單方式。 您不需要安裝 SQL Server，就能執行精靈。 此概觀描述您可以使用精靈來從中匯入或對其匯出的資料來源，以及執行精靈所需要的權限。

本主題僅提供精靈的**概觀**。
-   如果您準備好要執行精靈，且只是想要知道其啟動方式，請參閱[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。
-   如果您要尋找精靈中的步驟相關資訊，請在內容導覽功能表中選取需要的頁面。 精靈每個頁面都有各自的文件。 或在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。

**取得精靈。** 如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱[下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

> [!TIP] 如果您必須複製多個資料庫，或資料表和檢視以外的資料庫物件，請使用 [複製資料庫精靈]，而非 [匯入和匯出精靈]。 如需詳細資訊，請參閱[使用複製資料庫精靈](../../relational-databases/databases/use-the-copy-database-wizard.md)。

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>常用案例範例 - 將資料匯出到 Excel (影片)  
精靈的常見用法是將資料匯出至 Excel。 在以下四分鐘的 YouTube 影片中，會以清楚且簡單的指示來示範精靈並說明如何執行作業：[Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (使用 SQL Server 匯入和匯出精靈匯出至 Excel)。

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> 可以使用哪些資料來源與目的地？  
 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 可以在下列資料來源中來回複製資料。 若要使用這些資料來源的一部分，您可能必須要下載並安裝其他檔案。

| 資料來源 | 必須下載其他檔案嗎？ |
|-------------|-----------------------------------------|
|**企業資料庫**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle 及其他。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會安裝您要連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Oracle 所需的檔案，但不會安裝連接到 IBM DB2 或 Informix 等其他企業資料庫需要的檔案。<br/>- 企業資料庫系統如已安裝用戶端軟體，即已具備建立連接所需項目。<br/>- 如未安裝用戶端軟體，請詢問資料庫管理員如何安裝已授權的複本。|
|**開放原始碼資料庫**<br/>MySql、PostgreSQL、SQLite 及其他。|您必須下載其他檔案才能連接至這些資料來源。<br/><br/>- 針對 **MySQL** 請參閱 [MySQL Connectors](http://dev.mysql.com/downloads/connector/)。<br/>- 針對 **PostgreSQL** 請參閱 [psqlODBC - PostgreSQL ODBC driver](https://odbc.postgresql.org/) 和協力廠商產品，例如 [Npgsql - .NET Data Provider for PostgreSQL](http://www.npgsql.org/) 。<br/>- 若為 **SQLite**，請在數個線上開放原始碼提供者和驅動程式之間選取。|
|**文字檔** (一般檔案)。|不需要額外的檔案。|
|**Microsoft Excel 和 Microsoft Access 檔案**|Microsoft Office 不會安裝連接至 Excel 和 Access 檔案以作為資料來源所需的全部檔案。 取得以下下載項目：[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)。|
|**Azure 資料來源**<br/>目前僅 Azure Blob 儲存體。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會安裝連接至 Azure Blob 儲存體作為資料來源所需的檔案。 取得以下下載：[Azure 的 Microsoft SQL Server 2016 Integration Services 功能套件](https://www.microsoft.com/download/details.aspx?id=49492)。|
|**有可用連接器的任何其他資料來源**。|您通常必須下載其他檔案才能連接至下列類型的資料來源。<br/><br/>- 有可用 **ODBC 驅動程式**的任何來源。 建立 ODBC (開放式資料庫連接) 連接：在精靈的 [選擇資料來源] 或 [選擇目的地] 的頁面中選取 [.Net Framework Provider for Odbc (ODBC .Net Framework 提供者)]，然後提供參考 ODBC 驅動程式的連接字串或現有的 DSN (資料來源名稱)。<br/>- 有可用 **OLE DB 提供者**的任何來源。<br/>- 有可用 **.Net Framework 資料提供者**的任何來源。<br/>- 有**協力廠商元件**提供來源和目的地功能的其他資料來源。 這些協力廠商產品通常是當作 SQL Server Integration Services (SSIS) 的附加產品來行銷。|
  
> [!TIP] 如果您的資料來源需要連接字串，您可以在下列協力廠商網站上找到範例 - [The Connection Strings Reference](https://www.connectionstrings.com/) (連接字串參考)。  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>執行精靈需要的權限  
 若要順利完成 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]，您至少必須具備下列權限。 如果您已經在使用您的資料來源和目的地，可能就已經有需要的權限。
  
|您需要有權限才能執行這些作業|如果您連線到 SQL Server，則需要這些權限 |  
|-------------------------|----------------------------------------------------|  
|連接到來源及目的地資料庫或檔案共用。|伺服器與資料庫登入權限。|  
|匯出或讀取來源資料庫或檔案中的資料。|來源資料表和檢視的 SELECT 權限。|  
|將資料匯入或寫入目的地資料庫或檔案。|目的地資料表的 INSERT 權限。|  
|如果可行，建立目的地資料庫或檔案。|CREATE DATABASE 或 CREATE TABLE 權限。|  
|若適用，儲存精靈建立的 SSIS 封裝。|如果您想要將封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須要有將封裝儲存到 **msdb** 資料庫的足夠權限。|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> 精靈使用 SQL Server Integration Services (SSIS)  
 精靈使用 SQL Server Integration Services (SSIS) 複製資料。 SSIS 是擷取、轉換及載入資料 (ETL) 的工具。 精靈的頁面會使用一些 SSIS 語言。
  
 在 SSIS 中，基本的單位就是**封裝**。 當您在精靈的頁面間移動並指定選項時，精靈會在記憶體中建立 SSIS 封裝。    
  
如果安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 或更新版本，您也可以在精靈結尾處選擇儲存 SSIS 套件。 然後使用 [[!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 加入工作、轉換和事件驅動邏輯，重新使用及擴充封裝。 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 是建立基本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，將資料從來源複製到目的地的最簡單方式。

如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。

## <a name="get-help-while-the-wizard-is-running"></a>在精靈執行時取得說明
> [!TIP] 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。   
  
## <a name="whats-next"></a>下一步  
 啟動精靈。 如需詳細資訊，請參閱[啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。  
  
## <a name="see-also"></a>另請參閱
[SQL Server 匯入及匯出精靈的資料類型對應](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
