---
title: 使用複寫代理程式事件的警示 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing alerts
- Queue Reader Agent, alerts
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
- Log Reader Agent, alerts
- Distribution Agent, alerts
- Merge Agent, alerts
- agents [SQL Server replication], alerts
- displaying alerts
- Snapshot Agent, alerts
ms.assetid: 8c42e523-7020-471d-8977-a0bd044b9471
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3a670a78f6e906221638fb67c1cf5be8398b415b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68210739"
---
# <a name="use-alerts-for-replication-agent-events"></a>使用複寫代理程式事件的警示
  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 提供使用警示來監視事件 (如複寫代理程式事件) 的方法。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 會監視 Windows 應用程式記錄檔中與警示相關的事件。 如果發生這類事件， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent 會藉由執行已經定義的工作，及 (或) 向指定操作員傳送電子郵件或呼叫器訊息，進行自動回應。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 包含一組預先定義的複寫代理程式警示，您可以設定這類警示來執行工作和 (或) 通知操作員。 如需定義要執行之工作的詳細資訊，請參閱本主題的「自動化回應警示」一節。  
  
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
  
 除了這些警示外，複寫監視器還提供與狀態和效能相關的警告與警示集合。 如需詳細資訊，請參閱在複寫監視器警示基礎結構[中設定臨界值和警告](../monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 如需詳細資訊，請參閱[建立使用者定義的事件](../../../ssms/agent/create-a-user-defined-event.md)。  
  
 **若要設定預先定義的複寫警示**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[設定預先定義的複寫警示 &#40;SQL Server Management Studio&#41;](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md)  
  
## <a name="viewing-the-application-log-directly"></a>直接檢視應用程式記錄檔  
 若要檢視 Windows 應用程式記錄檔，請使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 事件檢視器。 應用程式記錄檔包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤訊息，以及電腦上其他許多活動的訊息。 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 錯誤記錄檔不同，每次啟動 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 時不會建立新的應用程式記錄檔 (每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 工作階段都會將新的事件寫入現有的應用程式記錄檔)，但您可以指定記錄事件的保留期限。 檢視 Windows 應用程式記錄檔時，您可以篩選特定事件的記錄檔。 如需詳細資訊，請參閱 Windows 文件集。  
  
## <a name="automating-a-response-to-an-alert"></a>自動化回應警示  
 複寫為資料驗證失敗的訂閱提供回應作業，還提供架構，可建立對警示的其他自動回應。 回應作業命名為 **[重新初始化資料驗證失敗的訂閱]** ，並儲存在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之 **Agent 的** [作業] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]資料夾中。 如需啟用此回應作業的詳細資訊，請參閱[設定預先定義的複寫警示 &#40;SQL Server Management Studio&#41;](../administration/configure-predefined-replication-alerts-sql-server-management-studio.md)。 如果交易式發行集中的發行項驗證失敗，回應作業只會重新初始化失敗的發行項。 如果合併式發行集中的發行項驗證失敗，回應作業將重新初始化發行集中的所有發行項。  
  
### <a name="framework-for-automating-responses"></a>自動回應的架構  
 通常在觸發警示時，協助您了解造成警示原因和採取適當動作的唯一資訊，都包含在警示訊息中。 剖析此資訊可能較費時，並且很容易出錯。 複寫透過提供 **sysreplicationalerts** 系統資料表中警示的其他資訊，簡化了自動回應；提供的資訊已剖析成易於自訂程式使用的形式。  
  
 例如，如果「訂閱者 A」 **Sales.SalesOrderHeader** 資料表中的資料驗證失敗， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 便會觸發 20574 訊息，通知您發生失敗。 您收到的訊息將會是：「訂閱者 'A' 訂閱的發行項 'SalesOrderHeader' (在發行集 'MyPublication' 中) 未通過資料驗證」。  
  
 如果您根據此訊息建立回應，必須手動從訊息中剖析「訂閱者」名稱、發行項名稱、發行集名稱及錯誤。 但由於「散發代理程式」和「合併代理程式」會將相同資訊寫入 **sysreplicationalerts** (包括代理程式類型、警示時間、發行集資料庫、「訂閱者」資料庫以及發行集類型等詳細資料)，回應作業可從資料表中直接查詢相關資訊。 儘管實際資料列無法與警示的特定執行個體相關聯，但資料表含 **status** 資料行，該資料可用於追蹤已服務的項目。 在記錄保留期限內將保留此資料表中的項目。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [複寫代理程式管理](replication-agent-administration.md)   
 [Best Practices for Replication Administration](../administration/best-practices-for-replication-administration.md)   
 [監視 &#40;複寫&#41;](../monitoring-replication.md)  
  
  
