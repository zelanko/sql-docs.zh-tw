---
title: "KILL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs: TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
caps.latest.revision: "61"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ff321a1ceec820049fc8c757d97336d0c25f1ce3
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  根據工作階段識別碼或工作單位 (UOW) 來結束使用者處理序。 如果指定的工作階段識別碼或 UOW 有許多工作来恢復，KILL 陳述式可能需要一些時間才能完成，特別是當它牽涉到回復較長的交易。  
  
 KILL 可用於結束正常的連接，這樣就可在內部結束與指定之工作階段識別碼關聯的交易。 當 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 在使用中時，此陳述式也可用以結束被遺棄和不確定的分散式交易。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>引數  
 *工作階段識別碼*  
 這是要結束之處理序的工作階段識別碼。 *工作階段識別碼*的唯一整數 (**int**) 時，指派給每個使用者連接會連接。 在連接持續時間，工作階段識別碼值會繫結連接。 當連接結束時，會釋出這個整數值，它可以重新指派給新的連接。  
下列查詢可協助您識別`session_id`您想要終止：  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**適用於**: ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 識別分散式交易的工作單位識別碼 (UOW)。 *UOW*是可能從 sys.dm_tran_locks 動態管理檢視的 request_owner_guid 資料行取得的 GUID。 *UOW*也可透過從錯誤記錄檔或透過 MS DTC 監視器。 如需有關監視分散式交易的詳細資訊，請參閱 MS DTC 文件集。  
  
 使用 KILL *UOW*以結束被遺棄的分散式的交易。 這些交易並未與任何真正的工作階段識別碼關聯，相反地，它們是人工地關聯於 session ID = '-2'。 透過查詢 sys.dm_tran_locks、sys.dm_exec_sessions 或 sys.dm_exec_requests 動態管理檢視中的 session ID 資料行，此工作階段識別碼使得識別被遺棄的交易變得更容易。  
  
 WITH STATUSONLY  
 會產生進度報告的指定*工作階段識別碼*或*UOW* ，正在復原回先前的 KILL 陳述式。 KILL WITH STATUSONLY 並不終止或回復*工作階段識別碼*或*UOW*; 此命令只會顯示目前的回復進度。  
  
## <a name="remarks"></a>備註  
 KILL 通常用來結束利用鎖定來封鎖其他重要處理序的處理序，或所執行的查詢在使用必要系統資源的處理序。 系統處理序和執行擴充預存程序的處理序無法結束。  
  
 尤其執行重要處理序時，請小心，使用 KILL。 您無法終止自己的處理序。 其他不應終止的處理序如下：  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
使用 @@SPID顯示目前工作階段的工作階段識別碼值。  
  
 若要取得使用中工作階段識別碼值的報告，您可以查詢 sys.dm_tran_locks、sys.dm_exec_sessions 以及 sys.dm_exec_requests 動態管理檢視中的 session_id 資料行。 您也可以檢視由 sp_who 系統預存程序傳回的 SPID 資料行。 如果的回復正在進行特定 SPID 中，sp_who 結果的 cmd 資料行會設定 SPID 指出 KILLED/ROLLBACK。  
  
 當特定連接對資料庫資源有鎖定並封鎖另一個連接的進度時，封鎖連接的工作階段識別碼會出現在 `blocking_session_id` 的 `sys.dm_exec_requests` 資料行或是由 `blk` 傳回的 `sp_who` 資料行中。  
  
 KILL 命令可用來解決不確定的分散式交易。 這些交易是未解決的分散式交易，之所以會發生是因為資料庫伺服器或 MS DTC 協調器發生了非計畫的重新啟動。 如需 「 可疑 」 交易的詳細資訊，請參閱中的 「 兩階段認可 」 一節[使用標示的異動以一致復原相關資料庫 &#40;完整復原模式 &#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>使用 WITH STATUSONLY  
 KILL WITH STATUSONLY 會產生報告，只有當工作階段識別碼或 UOW 目前正在回復因先前的 KILL*工作階段識別碼*|*UOW*陳述式。 進度報告會指出已完成的回復量 (百分比) 及估計的剩下時間長度 (以秒為單位)，格式如下：  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 如果工作階段識別碼或 UOW 的回復已經完成時終止*工作階段識別碼*|*UOW* WITH STATUSONLY 陳述式時，或如果沒有工作階段識別碼或 UOW 正在回復，KILL *工作階段識別碼*|*UOW* WITH STATUSONLY 會傳回下列錯誤：  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 您可以取得相同的狀態報告重複相同的 KILL*工作階段識別碼*|*UOW*陳述式，而不使用 WITH STATUSONLY 選項; 不過，我們不建議這樣。 重複 KILL*工作階段識別碼*陳述式可能會終止新處理序，如果復原已完成，且工作階段識別碼已重新指派至新的工作之前執行新的 KILL 陳述式。 指定 WITH STATUSONLY 會防止發生這個情況。  
  
## <a name="permissions"></a>Permissions  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:**需要 ALTER ANY CONNECTION 權限。 ALTER ANY CONNECTION 隨附在系統管理員 (sysadmin) 或處理序管理員 (processadmin) 固定伺服器角色的成員資格中。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:**需要 KILL DATABASE CONNECTION 權限。 伺服器層級主體登入已終止資料庫連接。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. 使用 KILL 來結束工作階段  
 下列範例顯示如何結束工作階段識別碼 `53`。  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>B. 使用 KILL 工作階段識別碼 WITH STATUSONLY 來取得進度報告  
 下列範例會產生特定工作階段識別碼的回復處理序狀態。  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. 使用 KILL 來結束被遺棄的分散式的交易  
 下列範例顯示如何結束被遺棄的分散式的交易 (工作階段識別碼 =-2) 與*UOW*的`D5499C66-E398-45CA-BF7E-DC9C194B48CF`。  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>另請參閱  
 [KILL STATS JOB &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
