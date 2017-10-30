---
title: "匯入和匯出資料的 SQL Server 匯入和匯出精靈 |Microsoft 文件"
ms.custom: 
ms.date: 10/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 6cd388215de02072522011b149a9cecc3239b64c
ms.contentlocale: zh-tw
ms.lasthandoff: 10/18/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>使用 SQL Server 匯入和匯出精靈來匯入或匯出資料

 > 如需舊版的 SQL Server 相關的內容，請參閱[執行 SQL Server 匯入和匯出精靈](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx)。

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈是將資料從來源複製到目的地的簡單方式。 本概觀說明資料來源精靈可作為來源和目的地，以及您執行精靈所需的權限。

## <a name="get-the-wizard"></a>取得精靈
如果您想要執行精靈，但電腦上尚未安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則可以安裝 SQL Server Data Tools (SSDT) 來安裝 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]。 如需詳細資訊，請參閱 [下載 SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)。

## <a name="what-happens-when-i-run-the-wizard"></a>在執行精靈時，會發生什麼事？
-    **請參閱步驟清單。** 如需精靈中的步驟的說明，請參閱[的 SQL Server 匯入和匯出精靈 」 中的步驟](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)。 也是在精靈的每一頁的文件的個別頁面。  
    \- 或 [選擇目的地] \-
-   **請參閱範例。** 快速瀏覽數個您在一般的工作階段中看到的畫面，看看這則簡易範例在單一頁面-[開始匯入和匯出精靈 」 的這個簡單的範例使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)。  

##  <a name="wizardSources"></a>哪些來源和目的地可以使用？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]匯入和匯出精靈可以將資料複製與下表所列的資料來源。 若要連接的部分這些資料來源，您可能要下載並安裝其他檔案。
 
| 資料來源 | 必須下載其他檔案嗎？ |
|-------------|-----------------------------------------|
|**企業資料庫**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 Oracle、 DB2 和其他項目。|SQL Server 或 SQL Server Data Tools (SSDT) 中安裝檔案，您需要連接到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 但是，SSDT 不會安裝您要連接到其他企業資料庫，如 Oracle 或 IBM DB2 的所有檔案。<br/><br/>若要連接到企業的資料庫，您通常必須擁有兩件事：<br/><br/>1.**用戶端軟體**。 企業資料庫系統如已安裝用戶端軟體，即已具備建立連接所需項目。 如未安裝用戶端軟體，請詢問資料庫管理員如何安裝已授權的複本。<br/><br/>2.**驅動程式或提供者**。 Microsoft 會安裝驅動程式和服務提供者連接到 Oracle。 若要連接至 IBM DB2，取得 Microsoft® OLEDB Provider for DB2 v5.0 Microsoft SQL Server 從[Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676)。<br/><br/>如需詳細資訊，請參閱[連接到 SQL Server 資料來源](connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)或[連接到 Oracle 資料來源](connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)。|
|**文字檔**（一般檔案）|不需要額外的檔案。<br/><br/>如需詳細資訊，請參閱[連接到一般檔案資料來源](connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)。|
|**Microsoft Excel 和 Microsoft Access 檔案**|Microsoft Office 不會安裝連接至 Excel 和 Access 檔案以作為資料來源所需的全部檔案。 取得下列下載- [Microsoft Access 資料庫引擎 2016年可轉散發套件](https://www.microsoft.com/download/details.aspx?id=54920)。<br/><br/>如需詳細資訊，請參閱[連接到 Excel 資料來源](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)或[Access 資料來源的連接](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)。|
|**Azure 資料來源**<br/>目前僅 Azure Blob 儲存體。|SQL Server Data Tools，請勿安裝您要連接到 Azure Blob 儲存體做為資料來源的檔案。 取得以下下載： [Azure 的 Microsoft SQL Server 2016 Integration Services 功能套件](https://www.microsoft.com/download/details.aspx?id=49492)。<br/><br/>如需詳細資訊，請參閱[連接到 Azure Blob 儲存體](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)。|
|**開放原始碼資料庫**<br/>PostgreSQL、 MySql 和其他項目。|若要連接到這些資料來源，您必須下載其他檔案。<br/><br/>-若為**PostgreSQL**，請參閱[PostgreSQL 資料來源的連接](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)。<br/>-若為**MySql**，請參閱[連接到 MySQL 資料來源](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)。|
|**任何其他資料來源驅動程式或提供者可供使用**|您通常必須下載其他檔案才能連接至下列類型的資料來源。<br/><br/>- 有可用 **ODBC 驅動程式** 的任何來源。 如需詳細資訊，請參閱[連接到 ODBC 資料來源](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)。<br/>- 有可用 **.Net Framework 資料提供者** 的任何來源。<br/>- 有可用 **OLE DB 提供者** 的任何來源。<br/><br/>提供其他資料來源的來源和目的地功能的協力廠商元件是有時候行銷附加產品為 SQL Server Integration Services (SSIS)。|

## <a name="how-do-i-connect-to-my-data"></a>如何連接到我的資料？
如需如何連接至常用的資料來源資訊，請參閱下列頁面：
-   [連線到 SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [連接到一般檔案 （文字檔）](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 Azure Blob 儲存體](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [使用 ODBC 連接](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [連接到 MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


如需如何連接到未在此處列出的資料來源資訊，請參閱[連接字串參考](https://www.connectionstrings.com/)。 此第三方網站包含範例連接字串和資料提供者的詳細資訊以及它們需要的連接資訊。

## <a name="what-permissions-do-i-need"></a>我需要哪些權限？  
 若要順利完成 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈]，您至少必須具備下列權限。 如果您已經在使用您的資料來源和目的地，可能就已經有需要的權限。
  
|您需要有權限才能執行這些作業|如果您要連線至 SQL Server，您會需要這些特定的權限 |  
|-------------------------|----------------------------------------------------|  
|連接到來源及目的地資料庫或檔案共用。|伺服器與資料庫登入權限。|  
|匯出或讀取來源資料庫或檔案中的資料。|來源資料表和檢視的 SELECT 權限。|  
|將資料匯入或寫入目的地資料庫或檔案。|目的地資料表的 INSERT 權限。|  
|如果可行，建立目的地資料庫或檔案。|CREATE DATABASE 或 CREATE TABLE 權限。|  
|若適用，儲存精靈建立的 SSIS 封裝。|如果您想要將封裝儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須要有將封裝儲存到 **msdb** 資料庫的足夠權限。|  
  
## <a name="get-help-while-the-wizard-is-running"></a>在精靈執行時取得說明
> [!TIP]
> 在精靈的任何頁面或對話方塊中點選 F1 鍵，以查看目前頁面的文件。   
  
##  <a name="wizardSSIS"></a> 精靈使用 SQL Server Integration Services (SSIS)  
 精靈使用 SQL Server Integration Services (SSIS) 複製資料。 SSIS 是擷取、轉換及載入資料 (ETL) 的工具。 精靈的頁面會使用一些 SSIS 語言。
  
 在 SSIS 中，基本的單位就是 **封裝**。 當您在精靈的頁面間移動並指定選項時，精靈會在記憶體中建立 SSIS 封裝。    
  
如果安裝了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 或更新版本，您也可以在精靈結尾處選擇儲存 SSIS 套件。 然後使用 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 加入工作、轉換和事件驅動邏輯，重新使用及擴充封裝。 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 是建立基本 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，將資料從來源複製到目的地的最簡單方式。

如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)。

## <a name="whats-next"></a>下一步  
 啟動精靈。 如需詳細資訊，請參閱 [啟動 SQL Server 匯入和匯出精靈](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)。  

## <a name="see-also"></a>另請參閱
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[SQL Server 匯入及匯出精靈的資料類型對應](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



