---
title: SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
ms.assetid: 8d1dc600-aabb-416f-b3af-fbc9fccfd0ec
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 80b6776f555fd5bdaa8ed4c4977dc5193a27eba2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37975193"
---
# <a name="sql-server-agent"></a>SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 是 Microsoft Windows 服務，它會執行排程的管理工作 (在 *中稱為* 「作業」 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)](Job))。  
  
**本主題內容**  
  
-   [SQL Server Agent 的優點](#Benefits)  
  
-   [SQL Server Agent 的元件](#Components)  
  
-   [SQL Server Agent 管理的安全性](#Security)  
  
## <a name="Benefits"></a>SQL Server Agent 的優點  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 來儲存作業資訊。 作業包含了一個或多個作業步驟。 每一個步驟包含它自己的工作 (例如備份資料庫)。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 可以按照排程、為了回應特定事件或視需要來執行作業。 例如，假設您要在每個工作日結束後備份公司的所有伺服器，您可以讓這項工作自動執行。 將備份排程在星期一至星期五 22:00 之後執行，如果備份發生問題，SQL Server Agent 可以記錄事件並通知您。  
  
> [!NOTE]  
> 根據預設，除非使用者明確地選擇要自動啟動服務，否則在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 時， [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] Agent 服務是停用的。  
  
## <a name="Components"></a>SQL Server Agent 元件  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 使用下列元件來定義要執行的工作，何時執行工作以及報告工作成功或失敗的方式。  
  
### <a name="jobs"></a>中稱為  
*「作業」* 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 執行的一系列指定動作。 請使用作業來定義管理工作，這個管理工作可以執行一或多次，而且可以監視它是成功或者失敗。 作業可以在本機伺服器或多個遠端伺服器上執行。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 容錯移轉叢集執行個體的容錯移轉事件期間執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業，並不會在容錯移轉至另一個容錯移轉叢集節點後繼續。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 於 Hyper-V 暫停期間執行的 Agent 作業，如果該此暫停會造成容錯移轉至另一個節點，那麼這些作業並不會繼續。 已開始的工作卻因為容錯移轉事件而無法完成，會記錄為已啟動，但是不會顯其他表示完成或失敗的記錄項目。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業看起來永遠不會結束。  
  
執行作業有數種方式：  
  
-   依照一個或多個排程。  
  
-   回應一個或多個警示。  
  
-   執行 sp_start_job 預存程序。  
  
作業中的每個動作都是 *「作業步驟」*(Job Step)。 例如，作業步驟可能是由執行 [!INCLUDE[tsql](../../includes/tsql_md.md)] 陳述式、執行 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝或對 Analysis Services 伺服器發出命令等動作構成。 作業步驟會視為作業的一部份來管理。  
  
每個作業步驟都是在特定的安全性內容中執行。 對於使用 [!INCLUDE[tsql](../../includes/tsql_md.md)]的作業步驟，請使用 EXECUTE AS 陳述式來設定作業步驟的安全性內容。 對其他作業步驟類型，可以使用 Proxy 帳戶來設定作業步驟的安全性內容。  
  
### <a name="schedules"></a>[排程]  
您可以使用 *「排程」* (Schedule) 來指定作業的執行時間。 相同的排程上可執行多個作業，而且多個排程可以套用到相同的作業。 排程可以為作業執行時間定義下列條件：  
  
-   每當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 啟動時。  
  
-   每當電腦的 CPU 使用率達到您定義為閒置的等級時。  
  
-   某個特定的日期和時間。  
  
-   執行循環排程時。  
  
如需詳細資訊，請參閱 [建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
### <a name="alerts"></a>警示  
*「警示」* 是針對特定事件的自動回應。 例如，事件可能是啟動某項作業，或是系統資源即將接近特定臨界值。 您要定義在什麼條件下會產生警示。  
  
警示可回應下列條件之一：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 事件  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 效能條件  
  
-   在執行 SQL Server Agent 之電腦上的 Microsoft Windows Management Instrumentation (WMI) 事件  
  
警示可執行下列動作：  
  
-   通知一或多個操作員  
  
-   執行作業  
  
如需詳細資訊，請參閱 [警示](../../ssms/agent/alerts.md)。  
  
### <a name="operators"></a>操作員  
*「操作員」* (Operator) 會定義負責維護一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體之人員的連絡資訊。 某些企業將操作員責任指派給一個人。 在具有多個伺服器的企業中，很多人可以共同擔任操作員的任務。 操作員不包含安全性資訊，而且不會定義安全性主體。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 可以透過下列一或多種方式，通知操作員發生警示：  
  
-   電子郵件  
  
-   呼叫器 (透過電子郵件)  
  
-   **net send**  
  
> [!NOTE]  
> 若要使用 **net send**來傳送通知，則必須在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 所在的電腦上啟動 Windows Messenger 服務。  
  
> [!IMPORTANT]  
> [呼叫器] 和 [Net Send] 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 未來版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 移除。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
若要使用電子郵件或呼叫器來傳送通知給操作員，則必須設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 以使用 Database Mail。 如需詳細資訊，請參閱 [Database Mail](http://msdn.microsoft.com/9e4563dd-4799-4b32-a78a-048ea44a44c1)。  
  
您可以將操作員定義成一群人員的別名。 用這種方法，可以同時告知具有該別名的所有成員。 如需詳細資訊，請參閱 [運算子](../../ssms/agent/operators.md)。  
  
## <a name="Security"></a>SQL Server Agent 管理的安全性  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會在 **msdb**資料庫中使用 **SQLAgentUserRole**、 **SQLAgentReaderRole** 與 **SQLAgentOperatorRole** 固定資料庫角色控制非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sysadmin **(系統管理員) 固定伺服器角色成員對** Agent 的存取。 除了這些固定資料庫角色之外，子系統與 Proxy 可協助資料庫管理員確保每一個作業步驟都以執行工作所需的最小權限來執行。  
  
### <a name="roles"></a>角色  
**msdb**中 **SQLAgentUserRole**、 **SQLAgentReaderRole** 與 **SQLAgentOperatorRole**固定資料庫角色的成員，以及 **系統管理員 (sysadmin)** 固定伺服器角色的成員，都具有存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 的權限。 不屬於以上任一角色的成員，都無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 所使用角色的詳細資訊，請參閱 [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)。  
  
### <a name="subsystems"></a>子系統  
子系統是預先定義的物件，代表作業步驟可用的功能。 每個 Proxy 都具有一或多個子系統的存取權。 子系統可提供安全性，因為它們會將 Proxy 可用的功能存取加以分隔。 每種作業步驟都可在 Proxy 的內容中執行，除了 [!INCLUDE[tsql](../../includes/tsql_md.md)] 作業步驟以外； [!INCLUDE[tsql](../../includes/tsql_md.md)] 作業步驟使用 EXECUTE AS 命令來設定作業擁有者的安全性內容。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 定義了下表所列的子系統：  
  
|子系統名稱|Description|  
|--------------|-----------|  
|Microsoft ActiveX Script|執行 ActiveX Scripting 作業步驟。<br /><br />**警告** [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 之後的版本會將 ActiveX Scripting 子系統從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。|  
|作業系統 (**CmdExec**)|執行可執行的程式。|  
|PowerShell|執行 PowerShell 指令碼作業步驟。|  
|複寫散發者|執行可啟動複寫「散發代理程式」的作業步驟。|  
|複寫合併|執行可啟動複寫「合併代理程式」的作業步驟。|  
|複寫佇列讀取器|執行可啟動複寫「佇列讀取器代理程式」的作業步驟。|  
|複寫快照|執行可啟動複寫「快照代理程式」的作業步驟。|  
|複寫交易記錄讀取器|執行可啟動複寫「記錄讀取器代理程式」的作業步驟。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 命令|執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 命令。|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 查詢|執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] 查詢。|  
|[!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝執行|執行 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝。|  
  
> [!NOTE]  
> 由於 [!INCLUDE[tsql](../../includes/tsql_md.md)] 作業步驟不使用 Proxy，因此沒有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 作業步驟適用的 [!INCLUDE[tsql](../../includes/tsql_md.md)] Agent 子系統。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會強制執行子系統限制，即使 Proxy 的安全性主體通常具有可執行作業步驟中工作的權限，亦是如此。 例如，屬於系統管理員 (sysadmin) 固定伺服器角色成員之使用者的 Proxy，若沒有 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 子系統的存取權，即無法執行 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 作業步驟，即使使用者可執行 [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝亦然。  
  
### <a name="proxies"></a>Proxy  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 使用 Proxy 來管理安全性內容。 一個 Proxy 可用於多個作業步驟。 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以建立 Proxy。  
  
每個 Proxy 都對應於一個安全性認證。 每一個 Proxy 可以與一組子系統和一組登入產生關聯。 Proxy 僅適用於使用該 Proxy 相關聯子系統的作業步驟。 若要建立使用特定 Proxy 的作業步驟，則作業擁有者必須使用與該 Proxy 相關的登入，或為可無限制存取 Proxy 的角色成員。 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以自由存取所有 Proxy； **SQLAgentUserRole**、 **SQLAgentReaderRole**或 **SQLAgentOperatorRole** 的成員，則只能使用他們已被授與特定存取權的 Proxy。 屬於這些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 固定資料庫角色成員的每一個使用者，必須被授與特定 Proxy 的存取權，才能建立使用這些 Proxy 的作業步驟。  
  
## <a name="related-tasks"></a>相關工作  
您可以使用下列步驟設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent，以便自動化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 管理：  
  
1.  確認哪些管理工作或伺服器事件會定期發生，以及是否可以程式設計的方式管理這些工作或事件。 如果工作包含一連串可預期的步驟，且在特定時間或為了回應特定事件而發生，則此工作就很適合自動執行。  
  
2.  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、 [!INCLUDE[tsql](../../includes/tsql_md.md)] 指令碼或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 管理物件 (SMO)，定義一組作業、排程、警示及運算子。 如需詳細資訊，請參閱 [建立作業](../../ssms/agent/create-jobs.md)。  
  
3.  執行您已定義的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業。  
  
> [!NOTE]  
> 針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的預設執行個體而言， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 服務的名稱為 SQLSERVERAGENT。 對於具名執行個體來說， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務的名稱為 SQLAgent$*instancename*。  
  
如果您執行多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]執行個體，您可以利用多伺服器管理來自動化所有執行個體間通用的工作。 如需詳細資訊，請參閱 [將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)。  
  
若要開始使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent，請使用下列工作：  
  
|Description|主題|  
|-----------|-----|  
|描述如何設定 SQL Server Agent。|[設定 SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)|  
|描述如何啟動、停止和暫停 SQL Server Agent 服務。|[啟動、停止或暫停 SQL Server Agent 服務](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)|  
|描述指定 SQL Server Agent 服務之帳戶的考量。|[選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)|  
|描述如何使用 SQL Server Agent 錯誤記錄檔。|[SQL Server Agent 錯誤記錄檔](../../ssms/agent/sql-server-agent-error-log.md)|  
|描述如何使用效能物件。|[使用效能物件](../../ssms/agent/use-performance-objects.md)|  
|描述維護計畫精靈，它是一個公用程式，可協助您用來建立作業、警示和操作員來自動化管理 SQL Server 的執行個體。|[使用維護計畫精靈](http://msdn.microsoft.com/db65c726-9892-480c-873b-3af29afcee44)|  
|描述如何使用 SQL Server Agent 自動化管理工作。|[自動化管理工作 &#40;SQL Server Agent&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)|  
  
## <a name="see-also"></a>另請參閱  
[介面區組態](http://msdn.microsoft.com/f741169c-1453-4ad2-830b-bf2be27d712f)  
  
