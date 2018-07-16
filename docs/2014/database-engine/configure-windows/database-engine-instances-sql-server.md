---
title: 資料庫引擎執行個體 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 243524a0f073ab1950398eff715bd1f1420144a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291344"
---
# <a name="database-engine-instances-sql-server"></a>Database Engine 執行個體 (SQL Server)
  執行個體[!INCLUDE[ssDE](../../includes/ssde-md.md)]是一份`sqlservr.exe`當做作業系統服務執行的可執行檔。 每個執行個體都會管理數個系統資料庫以及一個或多個使用者資料庫。 每部電腦都可以執行多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體。 應用程式會連接至執行個體，以在執行個體所管理的資料庫中執行工作。  
  
## <a name="instances"></a>執行個體  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體是做為服務來操作，而該服務可處理所有應用程式要求，以使用執行個體所管理之任何資料庫中的資料。 這是來自應用程式之連接要求 (登入) 的目標。 如果應用程式和執行個體位在不同的電腦上，則此連接會透過網路連接來執行。 如果應用程式和執行個體位在相同的電腦上，則 SQL Server 連接可以網路連接或記憶體中的連接形式來執行。 連接完成時，應用程式會透過與執行個體的連接來傳送 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 此執行個體會根據資料庫中的資料和物件將 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式解析為作業，而且如果已將必要的權限授與登入認證，則會執行工作。 任何擷取的資料以及任何訊息 (例如錯誤) 都會傳回給應用程式。  
  
 您可以在某部電腦上執行多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。 其中一個執行個體可以是預設執行個體。 預設執行個體沒有名稱。 如果連接要求只指定電腦的名稱，就會連接到預設執行個體。 具名執行個體是您在安裝執行個體時，指定執行個體名稱的執行個體。 連接要求必須指定電腦名稱和執行個體名稱，才能連接至該執行個體。 您不需要安裝預設執行個體，而在某部電腦上執行的所有執行個體都可以是具名執行個體。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何設定執行個體的屬性。 設定預設值 (例如檔案位置和日期格式)，或是執行個體使用作業系統資源 (例如記憶體或執行緒) 的方式。|[設定 Database Engine 執行個體 &#40;SQL Server&#41;](database-engine-instances-sql-server.md)|  
|描述如何管理 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的定序。 定序定義用來代表字元的位元模式，以及相關聯的行為 (例如排序) 和比較作業中的區分大小寫或區分腔調音。|[定序與 Unicode 支援](../../relational-databases/collations/collation-and-unicode-support.md)|  
|描述如何設定連結的伺服器定義，而這些連結的伺服器允許 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在執行個體中執行，以使用個別 OLE DB 資料來源中所儲存的資料。|[連結的伺服器 &#40;Database Engine&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|描述如何建立登入觸發程序，其指定登入嘗試已驗證之後，開始使用執行個體中的資源之前，所要採取的動作。 登入觸發程序可支援以下動作，如記錄連接活動，或根據 Windows 和 SQL Server 所執行認證驗證以外之邏輯的限制登入。|[登入觸發程序](../../relational-databases/triggers/logon-triggers.md)|  
|描述如何管理與 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體相關聯的服務。 此包含啟動和停止服務，或是設定啟動選項等動作。|[管理 Database Engine Services](manage-the-database-engine-services.md)|  
|描述如何執行伺服器網路組態工作，例如：啟用通訊協定、修改通訊協定所使用的通訊埠或管道、設定加密、設定 SQL Server Browser 服務、在網路上公開或隱藏 SQL Server Database Engine，以及註冊伺服器主體名稱。|[伺服器網路組態](server-network-configuration.md)|  
|描述如何執行用戶端網路組態工作，例如：設定用戶端通訊協定，以及建立或刪除伺服器別名。|[用戶端網路組態](client-network-configuration.md)|  
|描述可用來設計、偵錯以及執行指令碼 (例如 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指令碼) 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 編輯器。 同時描述如何撰寫 Windows PowerShell 指令碼以使用 SQL Server 元件。|[Database Engine 指令碼](../../relational-databases/scripting/database-engine-scripting.md)|  
|描述如何使用維護計畫來指定執行個體之一般管理工作的工作流程。 工作流程包含備份資料庫以及更新統計資料這類工作，以提升效能。|[維護計畫](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|描述如何使用資源管理員透過指定應用程式要求可用的 CPU 和記憶體數量限制，來管理資源耗用和工作負載。|[資源管理員](../../relational-databases/resource-governor/resource-governor.md)|  
|描述資料庫應用程式如何使用 Database Mail，從 [!INCLUDE[ssDE](../../includes/ssde-md.md)]傳送電子郵件訊息。|[Database Mail](../../relational-databases/database-mail/database-mail.md)|  
|描述如何使用擴充事件來擷取效能資料可用來建立效能比較基準或診斷效能問題。 擴充事件是一種輕量型的高擴充性系統，可供蒐集效能資料使用。|[擴充事件](../../relational-databases/extended-events/extended-events.md)|  
|描述如何使用 SQL 追蹤建立用於 [!INCLUDE[ssDE](../../includes/ssde-md.md)]中擷取以及記錄事件的自訂系統。|[SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)|  
|描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 擷取進入 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體之應用程式要求的追蹤。 稍後可以針對活動 (例如效能測試或問題診斷) 重新執行這些追蹤。|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|描述異動資料擷取 (CDC) 和變更追蹤功能，以及描述如何使用這些功能來追蹤資料庫資料變更。|[追蹤資料變更 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|描述如何使用 [記錄檔檢視器] 來尋找和檢視各種記錄檔中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤和訊息，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作業記錄、SQL Server 記錄檔和 Windows 事件記錄檔。|[記錄檔檢視器](../../relational-databases/logs/log-file-viewer.md)|  
|描述如何使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Tuning Advisor 來分析資料庫，以及提供解決潛在效能問題的建議。|[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|描述實際執行資料庫管理員在未接受標準連接時，如何對執行個體進行診斷連接。|[資料庫管理員的診斷連接](diagnostic-connection-for-database-administrators.md)|  
|描述如何使用已被取代的遠端伺服器功能來啟用不同 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體間的存取。 此功能的慣用機制是連結的伺服器。|[遠端伺服器](remote-servers.md)|  
|描述傳訊和佇列應用程式之 Service Broker 的功能，並提供 Service Broker 文件集的指標。|[Service Broker](sql-server-service-broker.md)|  
|描述如何使用緩衝集區擴充將非動態隨機存取儲存裝置 (固態磁碟機) 完全整合到 Database Engine 緩衝集區，以大幅提升 I/O 輸送量。|[緩衝集區擴充檔](buffer-pool-extension.md)|  
  
## <a name="see-also"></a>另請參閱  
 [sqlservr 應用程式](../../tools/sqlservr-application.md)   
 [資料庫功能](../../relational-databases/database-features.md)   
 [資料庫引擎跨執行個體功能](../database-engine-cross-instance-features.md)  
  
  
