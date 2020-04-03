---
title: 使用 system_health 工作階段
description: system_health 擴充事件工作階段隨附於 SQL Server。 此工作階段會收集系統資料，以針對資料庫引擎的效能進行疑難排解。
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- extended events [SQL Server], system health session
- extended events [SQL Server], system_health session
- system_health session [SQL Server extended events]
- system health session [SQL Server extended events]
ms.assetid: 1e1fad43-d747-4775-ac0d-c50648e56d78
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ffa5587415d9f4bc689a37a5ba49be87eaf14716
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79487586"
---
# <a name="use-the-system_health-session"></a>使用 system_health 工作階段

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

system_health 工作階段是預設隨附於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的擴充事件工作階段。 當 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 啟動時，這個工作階段就會自動啟動，並且在不造成任何明顯效能影響的情況下執行。 此工作階段會收集系統資料，讓您能夠用來協助疑難排解 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的效能問題。 

> [!IMPORTANT]
> 我們建議您不要停止、改變或刪除 system_health 工作階段。 未來的產品更新，都可能會覆寫對 system_health 工作階段設定所做的任何變更。
  
此工作階段所收集的資訊包括：  
  
-   對於遇到嚴重性 >=20 錯誤的任何工作階段，其中的 *sql_text* 和 *session_id*。  
  
-   對於遇到記憶體相關錯誤的任何工作階段，其中的 *sql_text* 和 *session_id*。 這些錯誤包括 17803、701、802、8645、8651、8657 和 8902。  
  
-   任何沒有產量之排程器問題的記錄 這些問題會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中顯示成錯誤 17883。  
  
-   偵測到的任何死結，包括死結圖形。  
  
-   對於已經等候閂鎖 (或其他相關資源) > 15 秒的任何工作階段，其中的 *callstack*、*sql_text* 和 *session_id*。  
  
-   對於已經等候鎖定 > 30 秒的任何工作階段，其中的 *callstack*、*sql_text* 和 *session_id*。  
  
-   對於已經等候先佔式等候一段長時間的任何工作階段，其中的 *callstack*、*sql_text* 和 *session_id*。 此持續時間會因等候類型而異。 先佔式等候是指 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 等候外部 API 呼叫的位置。  
  
-   CLR 配置和虛擬配置失敗的 *callstack* 和 *session_id*。  
  
-   記憶體 Broker、排程器監視器、記憶體節點 OOM、安全性和連線的環形緩衝區事件。  
  
-   來自 `sp_server_diagnostics` 的系統元件結果。  
  
-   *scheduler_monitor_system_health_ring_buffer_recorded* 所收集的執行個體健康狀態。  
  
-   CLR 配置失敗。  
  
-   使用 *connectivity_ring_buffer_recorded* 的連線錯誤。  
  
-   使用 *security_error_ring_buffer_recorded* 的安全性錯誤。  

> [!NOTE]
> 如需死結的詳細資訊，請參閱[交易鎖定與資料列版本設定指南中的死結](../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md#deadlocks)。   
> 如需 SQL 錯誤訊息的詳細資訊，請參閱[錯誤](../../relational-databases/errors-events/database-engine-events-and-errors.md)。

## <a name="viewing-the-session-data"></a>檢視工作階段資料  
工作階段會使用環形緩衝區目標和事件檔案目標來儲存資料。 事件檔案目標已設定 5 MB 的大小上限，以及 4 個檔案的檔案保留原則。 

若要使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中可用之擴充事件使用者介面來檢視環形緩衝區目標中的工作階段資料，請參閱[進階檢視 SQL Server 中擴充事件的目標資料 - 監看即時資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md#b3-watch-live-data)。

若要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來檢視環形緩衝區目標中的工作階段資料，請使用下列查詢：  
  
```sql  
SELECT CAST(xet.target_data as xml) 
FROM sys.dm_xe_session_targets xet  
JOIN sys.dm_xe_sessions xe ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'system_health'  
```  
  
若要檢視事件檔案中的工作階段資料，請使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中提供的「擴充事件」使用者介面。 如需詳細資訊，請參閱 [進階檢視 SQL Server 中擴充事件的目標資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。
  
## <a name="restoring-the-system_health-session"></a>還原 system_health 工作階段  
如果您刪除了 system_health 工作階段，可以在 [查詢編輯器] 中執行 **u_tables.sql** 檔案，藉以還原此工作階段。 這個檔案位於下列資料夾，其中 **C:** 代表您安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式檔案的磁碟機，而 **MSSQL1x** 表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的主要版本：  
  
 `C:\Program Files\Microsoft SQL Server\MSSQL1x.\<*instanceid*>\MSSQL\Install`  
  
請注意，當您還原此工作階段之後，必須使用 `ALTER EVENT SESSION` 陳述式或 [物件總管] 中的 [擴充事件]  節點來啟動此工作階段。 否則，此工作階段會在您下一次重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務時自動啟動。  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)    
 [擴充事件工具](../../relational-databases/extended-events/extended-events-tools.md)    
 [資料庫引擎錯誤](../../relational-databases/errors-events/database-engine-events-and-errors.md)    
 [訊息 (適用於錯誤) 目錄檢視 - sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) 
