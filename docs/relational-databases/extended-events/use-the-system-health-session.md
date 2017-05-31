---
title: "使用 system_health 工作階段 | Microsoft 文件"
ms.custom: 
ms.date: 06/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c64a0a128576a4bbf38f10b70514dbc4def84d11
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="use-the-systemhealth-session"></a>使用 system_health 工作階段
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  system_health 工作階段是預設隨附於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的擴充事件工作階段。 當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 啟動時，這個工作階段就會自動啟動，並且在不造成任何明顯效能影響的情況下執行。 此工作階段會收集系統資料，讓您能夠用來協助疑難排解 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的效能問題。 因此，我們建議您不要停止或刪除此工作階段。  
  
 此工作階段所收集的資訊包括：  
  
-   任何遇到嚴重性 >=20 錯誤之工作階段的 sql_text 和 session_id。  
  
-   任何遇到記憶體相關錯誤之工作階段的 sql_text 和 session_id。 這些錯誤包括 17803、701、802、8645、8651、8657 和 8902。  
  
-   任何沒有產量之排程器問題的記錄 (這些問題會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中顯示成錯誤 17883)。  
  
-   偵測到的任何死結。  
  
-   任何已經等候閂鎖 (或其他相關資源) > 15 秒之工作階段的 callstack、sql_text 和 session_id。  
  
-   任何已經等候鎖定 > 30 秒之工作階段的 callstack、sql_text 和 session_id。  
  
-   任何已經等候先佔式等候一段長時間之工作階段的 callstack、sql_text 和 session_id。 此持續時間會因等候類型而異。 先佔式等候是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等候外部 API 呼叫的位置。  
  
-   CLR 配置和虛擬配置失敗的呼叫堆疊與 session_id。  
  
-   記憶體 Broker、排程器監視器、記憶體節點 OOM、安全性和連接性的 ring_buffer 事件。  
  
-   來自 sp_server_diagnostics 的系統元件結果。  
  
-   scheduler_monitor_system_health_ring_buffer_recorded 所收集的執行個體健全狀況。  
  
-   CLR 配置失敗。  
  
-   使用 connectivity_ring_buffer_recorded 的連接錯誤。  
  
-   使用 security_error_ring_buffer_recorded 的安全性錯誤。  
  
## <a name="viewing-the-session-data"></a>檢視工作階段資料  
 工作階段會使用信號緩衝區目標來儲存資料。 若要檢視工作階段資料，請使用下列查詢：  
  
```  
SELECT CAST(xet.target_data as xml) FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe  
ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
若要檢視事件檔案中的工作階段資料，請使用 Management Studio 中提供的「擴充事件」使用者介面。 如需詳細資訊，請參閱 [進階檢視 SQL Server 中擴充事件的目標資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。
  
## <a name="restoring-the-systemhealth-session"></a>還原 system_health 工作階段  
 如果您刪除了 system_health 工作階段，可以在 [查詢編輯器] 中執行 **u_tables.sql** 檔案，藉以還原此工作階段。 這個檔案位於下列資料夾，其中 C: 代表您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式檔案的磁碟機：  
  
 C:\Program Files\Microsoft SQL Server\MSSQL13.\<執行個體識別碼>\MSSQL\Install  
  
 請注意，當您還原此工作階段之後，必須使用 ALTER EVENT SESSION 陳述式或 [物件總管] 中的 **[擴充事件]** 節點來啟動此工作階段。 否則，此工作階段會在您下一次重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務時自動啟動。  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件工具](../../relational-databases/extended-events/extended-events-tools.md)  
  
  

