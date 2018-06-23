---
title: Integration Services (SSIS) 連線 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 90
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: aa0a870cd1a5e48849b81d392f3d34bdeb7d308e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031681"
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
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會使用連接管理員做為連接的邏輯表示法。 在設計階段，您可以設定連接管理員的屬性，以描述 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 在封裝執行時建立的實體連接。 例如，連接管理員包含`ConnectionString`您設定在設計階段; 在執行階段的屬性，建立實體連接是使用中連接字串屬性的值。  
  
 封裝可使用連接管理員類型的多個執行個體，並且您可以在每個執行個體上設定屬性。 在執行階段，連接管理員類型的每個執行個體都會建立具有不同屬性的連接。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會提供不同類型的連接管理員，可讓封裝連接到各種資料來源和伺服器：  
  
-   當您安裝 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]時，安裝程式會安裝內建的連接管理員。  
  
-   有些連接管理員可從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 網站下載。  
  
-   如果現有的連接管理員不符合您的需求，您可以建立自己的自訂連接管理員。  
  
### <a name="built-in-connection-managers"></a>內建的連接管理員  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的連接管理員類型。  
  
|類型|描述|主題|  
|----------|-----------------|-----------|  
|ADO|連接到 ActiveX Data Objects (ADO) 物件。|[ADO 連線管理員](ado-connection-manager.md)|  
|ADO.NET|使用 .NET 提供者連接到資料來源。|[ADO.NET 連線管理員](ado-net-connection-manager.md)|  
|CACHE|從資料流程或快取檔案 (.caw) 中讀取資料，而且可以將資料儲存至快取檔案。|[快取連線管理員](cache-connection-manager.md)|  
|DQS|連接至 Data Quality Services 伺服器及伺服器上的 Data Quality Services 資料庫。|[DQS 清理連線管理員](dqs-cleansing-connection-manager.md)|  
|EXCEL|連接到 Excel 活頁簿檔案。|[Excel 連線管理員](excel-connection-manager.md)|  
|FILE|連接到檔案或資料夾。|[檔案連線管理員](file-connection-manager.md)|  
|FLATFILE|連接到單一一般檔案中的資料。|[一般檔案連線管理員](flat-file-connection-manager.md)|  
|FTP|連接到 FTP 伺服器。|[FTP 連線管理員](ftp-connection-manager.md)|  
|HTTP|連接到 Web 伺服器。|[HTTP 連線管理員](http-connection-manager.md)|  
|MSMQ|連接到訊息佇列。|[MSMQ 連線管理員](msmq-connection-manager.md)|  
|MSOLAP100|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的執行個體。|[Analysis Services 連線管理員](analysis-services-connection-manager.md)|  
|MULTIFILE|連接到多個檔案和資料夾。|[多重檔案連線管理員](multiple-files-connection-manager.md)|  
|MULTIFLATFILE|連接到多個資料檔案和資料夾。|[多重一般檔案連線管理員](multiple-flat-files-connection-manager.md)|  
|OLEDB|使用 OLE DB 提供者連接到資料來源。|[OLE DB 連線管理員](ole-db-connection-manager.md)|  
|ODBC|使用 ODBC 連接到資料來源。|[ODBC 連線管理員](odbc-connection-manager.md)|  
|SMOServer|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 伺服器。|[SMO 連線管理員](smo-connection-manager.md)|  
|SMTP|連接到 SMTP 郵件伺服器。|[SMTP 連線管理員](smtp-connection-manager.md)|  
|SQLMOBILE|連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 壓縮資料庫。|[SQL Server Compact Edition 連線管理員](sql-server-compact-edition-connection-manager.md)|  
|WMI|連接到伺服器，並指定該伺服器上 Windows Management Instrumentation (WMI) 管理的範圍。|[WMI 連線管理員](wmi-connection-manager.md)|  
  
### <a name="connection-managers-available-for-download"></a>可下載的連接管理員  
 下表列出您可以從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 網站下載的其他連接管理員類型。  
  
> [!IMPORTANT]  
>  下表所列出的連線管理員只可搭配 [!INCLUDE[ssEnterpriseEd11](../../includes/ssenterpriseed11-md.md)] 和 [!INCLUDE[ssDeveloperEd11](../../includes/ssdevelopered11-md.md)]使用。  
  
|類型|描述|主題|  
|----------|-----------------|-----------|  
|ORACLE|連接到 Oracle\<版本資訊 > 伺服器。|Oracle 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Oracle by Attunity 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面上的 [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526)。|  
|SAPBI|連接到 SAP NetWeaver BI 7 系統。|SAP BI 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for SAP BI 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面的＜ [Microsoft SQL Server 2008 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=262016)＞。|  
|TERADATA|連接到 Teradata\<版本資訊 > 伺服器。|Teradata 連接管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 的連接管理員元件。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector for Teradata by Attunity 也包含來源和目的地。 如需詳細資訊，請參閱下載頁面上的 [Microsoft Connectors for Oracle and Teradata by Attunity](http://go.microsoft.com/fwlink/?LinkId=251526)。|  
  
### <a name="custom-connection-managers"></a>自訂連接管理員  
 您也可以撰寫自訂連接管理員。 如需詳細資訊，請參閱＜ [Developing a Custom Connection Manager](../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
 如需如何加入或刪除封裝中之連線管理員的詳細資訊，請參閱[加入、刪除或共用封裝中的連線管理員](../add-delete-or-share-a-connection-manager-in-a-package.md)。  
  
 如需如何在封裝中設定連線管理員屬性的詳細資訊，請參閱[設定連線管理員的屬性](../set-the-properties-of-a-connection-manager.md)。  
  
## <a name="related-content"></a>相關內容  
  
-   technet.microsoft.com 上的影片： [沿用 Microsoft Attunity Connector for Oracle 來增強封裝效能](http://technet.microsoft.com/sqlserver/gg598963.aspx)  
  
-   social.technet.microsoft.com 上的 Wiki 文章： [SSIS 連接性](http://social.technet.microsoft.com/wiki/contents/articles/sql-server-integration-services-ssis.aspx#Connectivity)   
  
-   blogs.msdn.com 上的部落格文章： [從 SSIS 連接至 MySQL](http://go.microsoft.com/fwlink/?LinkId=217669)。  
  
-   blogs.msdn.com 上的技術文章： [擷取及載入 SQL Server Integration Services 中的 SharePoint 資料](http://go.microsoft.com/fwlink/?LinkId=247826)。  
  
-   support.microsoft.com 上的技術文章： [在 SSIS 中使用 Oracle 連線管理員時收到 "DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER" 錯誤訊息](http://go.microsoft.com/fwlink/?LinkId=233696)。  
  
  