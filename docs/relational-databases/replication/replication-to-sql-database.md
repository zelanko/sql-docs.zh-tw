---
title: 複寫至 SQL 資料庫 | Microsoft 文件
ms.custom: ''
ms.date: 04/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Database replication
- replication, SQL Database
ms.assetid: e8484da7-495f-4dac-b38e-bcdc4691f9fa
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e3099ebb18883a99b5815b3db3e40f178b22234
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="replication-to-sql-database"></a>複寫至 SQL 資料庫
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫可設定成 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。  
 
 ### <a name="supported-configurations"></a>**支援的組態：**  
 -  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以是在內部部署執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或在雲端 Azure 虛擬機器中執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 如需詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。  
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者的發送訂閱者。  
 -  散發資料庫和複寫代理程式不能放在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
 - 支援快照集和單向異動複寫。 不支援點對點異動複寫和合併式複寫。  
 
 ## <a name="versions"></a>版本  
 - 發行者和散發者至少必須為下列其中一個版本︰  
   
 -   [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]  
 
 -   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP1 CU3  
   
 -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] RTM CU10  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 CU8  
   
 -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 預期為 SP3  
   
 - 嘗試使用舊版設定複寫可能會導致錯誤號碼 MSSQL_REPL20084 (處理程序無法連接到訂閱者。) 和 MSSQL_REPL40532 (無法開啟登入所要求的伺服器 \<名稱>。 登入失敗。)。  
 
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 訂閱者至少必須是 V12，可位於任何區域。  
   
 - 若要使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 的所有功能，您必須使用最新版的 [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 和 [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx)。  
   
 ## <a name="remarks"></a>Remarks  
 - 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或對發行者執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，可以設定複寫。 您無法使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 入口網站設定複寫。  
   
 - 複寫只能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入連接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
   
 - 複寫的資料表必須有主索引鍵。  
   
 - 您必須擁有現有的 Azure 訂用帳戶和現有的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。  
   
 - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的單一發行集可以同時支援 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Azure 虛擬機器中的內部部署和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) 訂閱者。  
   
 - 複寫管理、監視和疑難排解都必須從內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行。  
   
 - 只支援發送訂閱至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 。  
   
 - SQL Database 的 `@subscriber_type = 0` 只支援 **@subscriber_type = 0** 。  
   
 - [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 不支援雙向、即時、可更新或點對點複寫。      
   
 ## <a name="replication-architecture"></a>複寫架構  
 ![複寫至 SQL 資料庫](../../relational-databases/replication/media/replication-to-sql-database.png "複寫至 SQL 資料庫")  
   
 ## <a name="scenarios"></a>案例  
   
 ### <a name="typical-replication-scenario"></a>一般複寫案例  
   
 1.  在內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中建立異動複寫發行集。  
   
 2.  在內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上使用[新增訂閱精靈]  或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式來建立發送訂閱至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
   
 3.  初始資料集通常為由快照集代理程式建立，並由「散發代理程式」散發和套用的快照集。 初始資料集也可透過備份或其他方式 (如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。  
   
 #### <a name="data-migration-scenario"></a>資料移轉案例  
   
 1.  使用異動複寫，將資料從內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫複寫到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
   
 2.  重新導向用戶端或中介層應用程式來更新 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 複本。  
   
 3.  停止更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的資料表，並移除發行集。  
   
 ## <a name="limitations"></a>限制  
  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 訂閱不支援下列選項︰  
   
 -   複製檔案群組關聯  
   
 -   複製資料表資料分割配置  
   
 -   複製索引資料分割配置  
   
 -   複製使用者定義的統計資料  
   
 -   複製預設繫結  
   
 -   複製規則繫結  
   
 -   複製全文檢索索引  
   
 -   複製 XML XSD  
   
 -   複製 XML 索引  
   
 -   複製權限  
   
 -   複製空間索引  
   
 -   複製篩選的索引  
   
 -   複製資料壓縮屬性  
   
 -   複製疏鬆資料行屬性  
   
 -   將檔案資料流轉換為 MAX 資料類型  
   
 -   將 hierarchyId 轉換為 MAX 資料類型  
   
 -   將空間轉換為 MAX 資料類型  
   
 -   複製擴充屬性  
   
 -   複製權限  
   
### <a name="limitations-to-be-determined"></a>要決定的限制 
 
 -   複製定序  
   
 -   [SP 的序列式交易執行]  
   
 ## <a name="examples"></a>範例  
  建立發行集和發送訂閱。 如需詳細資訊，請參閱：  
   
 -   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
   
 -   藉由使用 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 邏輯伺服器名稱作為訂閱者 (例如 **N'azuresqldbdns.database.windows.net'**) 並使用 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 名稱作為目的地資料庫 (例如 **AdventureWorks**)，以[建立發送訂閱](../../relational-databases/replication/create-a-push-subscription.md)。  
   
 ## <a name="see-also"></a>另請參閱  
 - [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 - [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 - [複寫類型](../../relational-databases/replication/types-of-replication.md)   
 - [監視 &#40;複寫&#41;](../../relational-databases/replication/monitor/monitoring-replication.md)   
 - [初始化訂閱](../../relational-databases/replication/initialize-a-subscription.md)  
