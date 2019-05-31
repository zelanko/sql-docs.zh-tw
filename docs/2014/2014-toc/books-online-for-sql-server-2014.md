---
title: 適用於 SQL Server 2014 線上叢書 》 |Microsoft Docs
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.technology: release-landing
ms.reviewer: ''
ms.topic: 'index-page '
f1_keywords:
- sql12.portal.f1
helpviewer_keywords:
- documentation [SQL Server], home page
- Help [SQL Server]
- SQL Server, documentation
- home page [SQL Server]
- Help [SQL Server], documentation home page
- Books Online [SQL Server], home page
- portal page [SQL Server]
ms.assetid: 674933a8-e423-4d44-a39b-2a997e2c2333
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 33cc877dfb2b1789aa775981e8377cf66b4ee950
ms.sourcegitcommit: 249c0925f81b7edfff888ea386c0deaa658d56ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/30/2019
ms.locfileid: "66413211"
---
# <a name="books-online-for-sql-server-2014"></a>SQL Server 2014 的線上叢書

  歡迎使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)]® 的《[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]® 線上叢書》。 《線上叢書》包含工作描述和參考文件集，描述如何使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行資料管理及商業智慧工作。  

SQL Server 2016 和更新版本中，記載[此處](https://docs.microsoft.com/sql/sql-server/index)。 SQL Server 2012 和較舊版本，都記載[此處](#previous-versions-gm2014)。 <!-- ?view= defaults to the latest GA version, to resolve the https '/index' address ambiguity. So '2014' will always be too old to be the default. -->

 **現在就試試看：**  
 ![Azure 虛擬機器小型](../sql-server/media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) 擁有 Azure 帳戶嗎？  接著前往 **[此處](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** 到已安裝 SQL Server 2014 Service Pack 1 (SP1) 的虛擬機器的加速。 如需有關 SQL Server 2014 (SP1) 的詳細資訊，請參閱 < [SQL Server 2014 Service Pack 1 版本資訊](https://support.microsoft.com/en-us/kb/3058865)。 
  
## <a name="sql-server-technologies"></a>SQL Server 技術  

 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 包含數種資料管理和分析技術。 按下表中的連結，以尋找每項技術的功能、工作及參考文件集。  
  
|||  
|-|-|  
|![Database Engine 圖示](media/database-engine.gif "Database Engine 圖示")|[資料庫引擎](../database-engine/sql-server-database-engine-overview.md)<br /><br /> Database Engine 是用於儲存、處理和保護資料的核心服務。 它提供受控制的存取和快速交易處理，可滿足您企業內部最嚴苛的資料取用應用程式需求。 Database Engine 還提供豐富的支援以維持高可用性。|  
|![BOL 首頁主題的 DQS 標誌](media/dqs-logo.jpg "BOL 首頁主題的 DQS 標誌")|[Data Quality Services](../data-quality-services/data-quality-services.md)<br /><br /> SQL Server Data Quality Services (DQS) 提供您知識驅動的資料清理方案。 DQS 可讓您建立知識庫，然後使用該知識庫透過電腦輔助及互動式方法，對您的資料執行資料更正及刪除重複資料。 您可以使用雲端式參考資料服務，也可以建立資料管理方案，將 DQS 與 SQL Server Integration Services 和 Master Data Services 進行整合。|  
|![Analysis Services 圖示](media/analysisserver.gif "Analysis Services 圖示")|[Analysis Services (英文)](../analysis-services/analysis-services.md)<br /><br /> [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 是一套適用於個人、團隊和企業商業智慧的分析資料平台與工具組。 伺服器和用戶端設計工具支援傳統的 OLAP 方案、新的表格式模型方案，以及使用 PowerPivot、Excel 和 SharePoint Server 環境的自助式分析與共同作業。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 也包含資料採礦，讓您能夠發現隱藏在大量資料內部的模式和關聯性。|  
|![Integration Services 圖示](media/dts.gif "Integration Services 圖示")|[Integration Services](../integration-services/sql-server-integration-services.md)<br /><br /> [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一個平台，用於建立高效能資料整合方案，包括提供資料倉儲之擷取、轉換和載入 (ETL) 處理的封裝。|  
|![mds_cm_icon](media/mds-cm-icon.gif "mds_cm_icon")|[Master Data Services](../master-data-services/master-data-services.md)<br /><br /> [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 建立在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 上的方案可協助確保報表和分析乃依據正確的資訊。 使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]可建立主要資料的中央儲存機制，並且在資料隨時間改變時，維持可稽核且安全的記錄。|  
|![複寫圖示](media/replication.gif "複寫圖示")|[複寫](../relational-databases/replication/sql-server-replication.md)<br /><br /> 複寫是一組技術，用於將資料和資料庫物件從某個資料庫複製和散發到另一個資料庫，然後在兩個資料庫之間進行同步處理以維護一致性。 使用複寫，您可以透過區域網路、廣域網路、撥號連接、無線連接及網際網路，將資料散發到不同的位置以及遠端或行動使用者。|  
|![Reporting Services 圖示](media/reportingservices.gif "Reporting Services 圖示")|[Reporting Services](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)<br /><br /> Reporting Services 提供了啟用 Web 的企業級報表功能，讓您可以建立從各種資料來源取得內容的報表、以各種格式發行報表，以及集中管理安全性和訂閱。|  
  
## <a name="sql-server-information-on-the-web"></a>網站上的 SQL Server 資訊  

 [!INCLUDE[msCoName](../includes/msconame-md.md)] 在幾個網站中發行有關 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的其他資訊。  
  
 **SQL Server 網站**  
  
-   [Microsoft.com 上的 SQL Server](https://go.microsoft.com/fwlink/?linkid=8504)  
  
-   [SQL Server 資源中心](https://www.microsoft.com/sql-server/sql-server-2017-resources)  
  
-   [SQL Server TechCenter](https://go.microsoft.com/fwlink/?linkid=28107)  
  
-   [SQL Server 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=42457)  
  
-   [資料平台開發人員中心](https://go.microsoft.com/fwlink/?LinkId=17386)  
  
-   [XML 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=42458)  

## <a name="previous-versions-gm2014"></a> SQL Server 2005、 2008、 2012、 2016年 +

[!INCLUDE[???](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>另請參閱  

 [SQL Server 組態管理員說明](../tools/configuration-manager/sql-server-configuration-manager-help.md)  
  
  
