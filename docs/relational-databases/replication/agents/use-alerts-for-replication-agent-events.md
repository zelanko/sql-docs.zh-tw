---
title: "使用複寫代理程式事件的警示 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "檢視警示"
  - "佇列讀取器代理程式, 警示"
  - "警示 [SQL Server 複寫]"
  - "預先定義的複寫警示 [SQL Server 複寫]"
  - "記錄讀取器代理程式, 警示"
  - "散發代理程式, 警示"
  - "合併代理程式, 警示"
  - "代理程式 [SQL Server 複寫], 警示"
  - "顯示警示"
  - "快照集代理程式, 警示"
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 使用複寫代理程式事件的警示
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式提供監視事件，如複寫代理程式事件的方法使用警示。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式會監視 Windows 應用程式記錄檔與警示相關聯的事件。 如果發生這類事件，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 會藉由執行已經定義的工作，及 (或) 向指定操作員傳送電子郵件或呼叫器訊息，進行自動回應。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 您可以設定執行工作和 （或） 通知操作員的複寫代理程式包含一組預先定義的警示。 如需定義要執行之工作的詳細資訊，請參閱本主題的「自動化回應警示」一節。  
  
 當電腦設定為「散發者」時，會安裝下列警示：  
  
|訊息 ID|預先定義的警示|觸發警示的條件|在 msdb..sysreplicationalerts 中輸入額外的資訊|  
|----------------|----------------------|-----------------------------------------|-----------------------------------------------------------------|  
|14150|**複寫: 代理程式成功**|代理程式成功關閉。|是|  
|14151|**複寫: 代理程式失敗**|代理程式關閉時發生錯誤。|是|  
|14152|**複寫: 代理程式重試**|代理程式於重試動作不成功之後關閉 (代理程式遇到錯誤，例如伺服器無法使用、鎖死、連線失敗、或逾時失敗)。|是|  
|14157|**複寫: 已卸除逾期的訂閱**|已卸除逾期的訂閱。|否|  
|20572|**複寫: 驗證失敗後重新初始化訂閱**|回應作業「重新初始化資料驗證失敗的訂閱」成功重新初始化訂閱。|否|  
|20574|**複寫: 訂閱者資料驗證失敗**|散發或合併代理程式的資料驗證失敗。|是|  
|20575|**複寫: 訂閱者已經通過資料驗證**|散發或合併代理程式通過資料驗證。|是|  
|20578|**複寫: 代理程式自訂關閉**|||  
|22815|**點對點衝突偵測警示**|散發代理程式在嘗試將變更套用到對等節點上時偵測到衝突。|是|  
  
 除了這些警示外，複寫監視器還提供與狀態和效能相關的警告與警示集合。 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警示基礎結構，為其他複寫事件定義警示。 如需詳細資訊，請參閱 [建立使用者定義事件](../../../ssms/agent/create-a-user-defined-event.md)。  
  
 **若要設定預先定義的複寫警示**  
  
-   [!包含 [ssManStudioFull] (.../ Token/ssManStudioFull_md.md)]: [Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## 直接檢視應用程式記錄檔  
 若要檢視 Windows 應用程式記錄檔，請使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 事件檢視器。 應用程式記錄檔包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤訊息，以及電腦上其他許多活動的訊息。 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤記錄檔不同，每次啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時不會建立新的應用程式記錄檔 (每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工作階段都會將新的事件寫入現有的應用程式記錄檔)，但您可以指定記錄事件的保留期限。 檢視 Windows 應用程式記錄檔時，您可以篩選特定事件的記錄檔。 如需詳細資訊，請參閱 Windows 文件集。  
  
## 自動化回應警示  
 複寫為資料驗證失敗的訂閱提供回應作業，還提供架構，可建立對警示的其他自動回應。 回應作業命名為 **資料驗證失敗的訂閱重新初始化** 並儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理程式 **工作** 資料夾中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]。 啟用此回應作業的相關資訊，請參閱 [設定預先定義的複寫警示 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)。 如果交易式發行集中的發行項驗證失敗，回應作業只會重新初始化失敗的發行項。 如果合併式發行集中的發行項驗證失敗，回應作業將重新初始化發行集中的所有發行項。  
  
### 自動回應的架構  
 通常在觸發警示時，協助您了解造成警示原因和採取適當動作的唯一資訊，都包含在警示訊息中。 剖析此資訊可能較費時，並且很容易出錯。 複寫更輕鬆自動化回應警示中的其他資訊提供 **sysreplicationalerts** 系統資料表中，輕鬆地使用自訂程式的形式已剖析所提供的資訊。  
  
 比方說，如果在資料 **Sales.SalesOrderHeader** 「 訂閱者的資料表無法通過驗證， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可以觸發 20574 訊息，通知您發生失敗。 您收到的訊息將會是: 「 訂閱者 'A'、 訂閱的發行集 'MyPublication' 中的發行項 'SalesOrderHeader' 資料驗證失敗。 」  
  
 如果您根據此訊息建立回應，必須手動從訊息中剖析「訂閱者」名稱、發行項名稱、發行集名稱及錯誤。 不過，因為散發代理程式 」 和 「 合併代理程式寫入至相同的資訊，所以 **sysreplicationalerts** （連同例如代理程式類型、 警示、 發行集資料庫、 訂閱者資料庫的時間和發行集類型的詳細資料） 回應作業可以直接查詢資料表中的相關資訊。 雖然實際的資料列無法與警示的特定執行個體相關聯，則表示資料表具有 **狀態** 資料行，可用來追蹤服務的項目。 在記錄保留期限內將保留此資料表中的項目。  
  
 例如，若要在服務警示訊息 20574 的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中建立回應作業，可能會使用下列邏輯：  
  
```  
declare @publisher sysname, @publisher_db sysname, @publication sysname, @publication_type int, @article sysname, @subscriber sysname, @subscriber_db sysname, @alert_id int  
declare hc cursor local for select publisher, publisher_db, publication, publication_type, article, subscriber,   
  subscriber_db, alert_id from   
  msdb..sysreplicationalerts where  
  alert_error_code = 20574 and status = 0  
  for read only  
open hc  
fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
while (@@fetch_status <> -1)  
begin  
/* Do custom work  */  
/* Update status to 1, which means the alert has been serviced. This prevents subsequent runs of this job from doing this again */  
update msdb..sysreplicationalerts set status = 1 where alert_id = @alert_id  
 fetch hc into  @publisher, @publisher_db, @publication, @publication_type, @article, @subscriber, @subscriber_db, @alert_id  
end  
close hc  
deallocate hc  
```  
  
## 另請參閱  
 [複寫代理程式管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [複寫管理的最佳做法](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)   
 [監視和 #40。複寫 & #41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  