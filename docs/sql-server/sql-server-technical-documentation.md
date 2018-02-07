---
title: "SQL Server 文件集 | Microsoft Docs"
ms.date: 10/30/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
caps.latest.revision: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5e6b2ffe7735bf8c7cb2fe7e9f76b7d4b675ceef
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="sql-server-documentation"></a>SQL Server 文件集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server 是 Microsoft 資料平台的核心。 SQL Server 是操作資料庫管理系統 (ODBMS) 的業界領導者。 本文件可協助您安裝、設定及使用 SQL Server。 內容包括端對端範例、程式碼範例和視訊。 如需 SQL Server 語言主題，請參閱[語言參考](../t-sql/language-reference.md)。

|新功能  | 版本資訊  |
|---------|---------|
|[SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)     | [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)        |
|[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)     | [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)        |
|[SQL Server 2014 的新功能](https://msdn.microsoft.com/library/bb500435(v=sql.120).aspx)     | [SQL Server 2014 Release Notes](../sql-server/sql-server-2014-release-notes.md)        |
   
**試用 SQL Server！**

|||
|-|-|
|[![從 Evaluation Center 下載](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) [下載 SQL Server 2017](http://go.microsoft.com/fwlink/?LinkID=829477) | [![從 Evaluation Center 下載](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) [下載 SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) |
|[![建立虛擬機器](../includes/media/azure-vm.png)](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) [取得 SQL Server 虛擬機器](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) | [![從 Evaluation Center 下載](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) [下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) |
| [![從 Evaluation Center 下載](../includes/media/download2.png)](../ssdt/download-sql-server-data-tools-ssdt.md) [下載 SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | |

    
## <a name="sql-server-technologies"></a>SQL Server 技術    
    
|||    
|-|-|    
|![SQL 資料庫引擎](../sql-server/media/sql-database-engine.png "SQL 資料庫引擎")|**[Database Engine](../database-engine/sql-server-database-engine-overview.md)**<br /><br /> Database Engine 是用於儲存、處理和保護資料的核心服務。 它提供受控制的存取和快速交易處理，可滿足您企業內部最嚴苛的資料取用應用程式需求。 Database Engine 還提供豐富的支援以維持高可用性。|
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一個平台，用於建立高效能資料整合方案，包括提供資料倉儲之擷取、轉換和載入 (ETL) 處理的封裝。|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] 是一套適用於個人、團隊和企業商業智慧的分析資料平台與工具組。 伺服器和用戶端設計工具支援傳統的 OLAP 方案、新的表格式模型方案，以及使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]、Excel 和 SharePoint Server 環境的自助式分析與共同作業。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 也包含資料採礦，讓您能夠發現隱藏在大量資料內部的模式和關聯性。|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services 提供啟用 Web 的企業級報告功能。  您可以建立從各種資料來源取得內容的報表、以各種格式發行報表，以及集中管理安全性和訂閱。|
|![R Server](../sql-server/media/r-server.png "R Server")|**[機器學習服務](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft Machine Learning 服務支援將機器學習 (使用受歡迎的 R 和 Python 語言) 整合到企業的工作流程。<br /><br /> Machine Learning 服務 (資料庫內) 將 R 和 Python 與 SQL Server 整合，藉由呼叫預存程序，以輕鬆建立、重新定型模型，以及為模型評分。  Microsoft Machine Learning 伺服器提供企業規模的 R 和 Python 支援，而不需要 SQL Server。|
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) 提供您知識驅動的資料清理方案。 DQS 可讓您建立知識庫，然後使用該知識庫透過電腦輔助及互動式方法，對您的資料執行資料更正及刪除重複資料。 您可以使用雲端式參考資料服務，也可以建立資料管理方案，將 DQS 與 SQL Server Integration Services 和 Master Data Services 進行整合。|
|![複寫服務](../sql-server/media/replication-services.png "複寫服務")|**[複寫](../relational-databases/replication/sql-server-replication.md)**<br /><br /> 複寫是一組技術，用於將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理以維護一致性。 使用複寫，您可以透過區域網路、廣域網路、撥號連接、無線連接及網際網路，將資料散發到不同的位置以及遠端或行動使用者。|
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 建立在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 上的方案可協助確保報表和分析乃依據正確的資訊。 使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]可建立主要資料的中央儲存機制，並且在資料隨時間改變時，維持可稽核且安全的記錄。|

## <a name="migrate-and-move-data"></a>移轉並移動資料
- [使用 SQL Server 匯入和匯出精靈來匯入和匯出資料](../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)
- [Microsoft Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)
- [將 SQL Server Database 移轉至 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

## <a name="earlier-sql-server-versions"></a>較早的 SQL Server 版本
- [SQL Server 更新中心 - 所有已支援版本的連結和資訊](https://msdn.microsoft.com/library/ff803383.aspx)
- [SQL Server 2014 文件](https://msdn.microsoft.com/library/ms130214(v=sql.120).aspx)
- [SQL Server 2012 文件](https://technet.microsoft.com/library/bb418433(v=sql.10).aspx)  
- [SQL Server 2008 R2 文件](https://msdn.microsoft.com/library/hh278298(v=sql.10).aspx)  
- [SQL Server 2008 文件](https://msdn.microsoft.com/library/hh994727(v=sql.10).aspx) 
- [SQL Server 2005 封存文件](https://msdn.microsoft.com/library/hh278313(v=sql.10).aspx)    

## <a name="samples"></a>範例  
- [Wide World Importers 範例資料庫](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx)  
- [SQL Server 2016 的 AdventureWorks 範例資料庫與指令碼](https://www.microsoft.com/download/details.aspx?id=49502) 
- [GitHub 上的 SQL Server 範例](https://github.com/Microsoft/sql-server-samples) 
   
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
