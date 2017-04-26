---
title: "SQL Server 2016 技術文件 | Microsoft Docs"
ms.date: 03/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
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
caps.latest.revision: 106
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 034e10f491c3c327d6a7b2a044f57121636c3c06
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-technical-documentation"></a>SQL Server 技術文件
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

 可協助您安裝、設定和使用 SQL Server 的文件。 內容包括完整範例、程式碼範例和視訊。 如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 語言的主題，請參閱 [語言參考](../t-sql/language-reference.md)。

**SQL Server vNext**

如需最新版本資訊，請參閱 [SQL Server vNext 版本資訊](../sql-server/sql-server-vnext-release-notes.md)

如需新功能的最新資訊，請參閱 [SQL Server vNext 的新功能](../sql-server/what-s-new-in-sql-server-vnext.md)
 
**SQL Server 2016：**
 
 [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)

[SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)
    
 **試用 SQL Server！**    
    
 - [**從評估中心下載 SQL Server 2016**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)    
    
- **[啟動已安裝 SQL Server 2016 的虛擬機器](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)**    
    
-  **[下載最新版的 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**   
    
  
    
## <a name="sql-server-technologies"></a>SQL Server 技術    
    
|||    
|-|-|    
|![SQL 資料庫引擎](../sql-server/media/sql-database-engine.png "SQL 資料庫引擎")|**[Database Engine](../database-engine/configure-windows/sql-server-database-engine.md)**<br /><br /> Database Engine 是用於儲存、處理和保護資料的核心服務。 它提供受控制的存取和快速交易處理，可滿足您企業內部最嚴苛的資料取用應用程式需求。 Database Engine 還提供豐富的支援以維持高可用性。|    
|![R Server](../sql-server/media/r-server.png "R Server")|**[R Services](../advanced-analytics/r-services/r-services.md)**<br /><br /> Microsoft R Services 提供多種方法來將受歡迎的 R 語言併入企業工作流程中。<br /><br /> [!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] 會整合 R 語言和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，以便藉由呼叫 [!INCLUDE[tsql](../includes/tsql-md.md)] 預存程序輕鬆建立、重新定型以及為模型評分。<br /><br /> Microsoft R Server 在企業中提供 R 的多平台、可擴充支援，並且支援 Hadoop 和 Teradata 等資料來源。|    
|![Data Quality Services](../sql-server/media/data-quality-services.png "Data Quality Services")|**[Data Quality Services](../data-quality-services/data-quality-services.md)**<br /><br /> SQL Server Data Quality Services (DQS) 提供您知識驅動的資料清理方案。 DQS 可讓您建立知識庫，然後使用該知識庫透過電腦輔助及互動式方法，對您的資料執行資料更正及刪除重複資料。 您可以使用雲端式參考資料服務，也可以建立資料管理方案，將 DQS 與 SQL Server Integration Services 和 Master Data Services 進行整合。|    
|![Integration Services](../sql-server/media/integration-services.png "Integration Services")|**[Integration Services](../integration-services/sql-server-integration-services.md)**<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一個平台，用於建立高效能資料整合方案，包括提供資料倉儲之擷取、轉換和載入 (ETL) 處理的封裝。|    
|![Master Data Services](../sql-server/media/master-data-services.png)|**[Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md)**<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 建立在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 上的方案可協助確保報表和分析乃依據正確的資訊。 使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]可建立主要資料的中央儲存機制，並且在資料隨時間改變時，維持可稽核且安全的記錄。|    
|![Analysis Services](../sql-server/media/analysis-services.png "Analysis Services")|**[Analysis Services](../analysis-services/analysis-services.md)**<br /><br /> [!INCLUDE[ssASnoversion_md](../includes/ssasnoversion-md.md)] 是一套適用於個人、團隊和企業商業智慧的分析資料平台與工具組。 伺服器和用戶端設計工具支援傳統的 OLAP 方案、新的表格式模型方案，以及使用 [!INCLUDE[ssGemini](../includes/ssgemini-md.md)]、Excel 和 SharePoint Server 環境的自助式分析與共同作業。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 也包含資料採礦，讓您能夠發現隱藏在大量資料內部的模式和關聯性。|    
|![複寫服務](../sql-server/media/replication-services.png "複寫服務")|**[複寫](../relational-databases/replication/sql-server-replication.md)**<br /><br /> 複寫是一組技術，用於將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理以維護一致性。 使用複寫，您可以透過區域網路、廣域網路、撥號連接、無線連接及網際網路，將資料散發到不同的位置以及遠端或行動使用者。|    
|![Reporting Services](../sql-server/media/reporting-services.png "Reporting Services")|**[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)**<br /><br /> Reporting Services 提供了啟用 Web 的企業級報表功能，讓您可以建立從各種資料來源取得內容的報表、以各種格式發行報表，以及集中管理安全性和訂閱。|    
     
   
 ## <a name="more-information"></a>詳細資訊   
+ [SQL Server 組態管理員](../relational-databases/sql-server-configuration-manager.md)
+ [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx) 連結和資訊，以取得所有支援的版本 
+ [安裝 SQL Server Database Engine](../database-engine/install-windows/install-sql-server-database-engine.md) 
+ [安裝 SQL Server 管理工具與 SSMS](https://msdn.microsoft.com/library/bb500441.aspx) 
+ [Visual Studio 2015 中的 SQL Server Data Tools](https://msdn.microsoft.com/mt186501.aspx)
+ [影片、範例和社群資源](https://msdn.microsoft.com/library/dn237258.aspx)
+ [SQL Server 2016 簡介](https://www.microsoft.com/en-us/server-cloud/products/sql-server/default.aspx?WT.srch=1&WT.mc_id=SEM_%5B_uniqid%5D&utm_source=Bing&utm_medium=CPC&utm_term=SQL%20Server%202016&utm_campaign=Data_Management)  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect-md](../includes/feedback-stackoverflow-msdn-connect-md.md)]


