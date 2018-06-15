---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
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
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2cf23ffc6cceaf92f80eb75dbe9da1179e9e4a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064165"
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  根據工作階段識別碼或工作單位 (UOW) 來結束使用者處理序。 如果指定的工作階段識別碼或 UOW 有許多工作要復原，KILL 陳述式可能需要花一些時間來完成，特別是當它牽涉到復原較長的交易時。  
  
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
 *session ID*  
 這是要結束之處理序的工作階段識別碼。 *session ID* 是在建立連線時，指派給每個使用者連線的唯一整數 (**int**)。 在連接持續時間，工作階段識別碼值會繫結連接。 當連接結束時，會釋出這個整數值，它可以重新指派給新的連接。  
下列查詢可協助識別您想要終止的 `session_id`：  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 識別分散式交易的工作單位識別碼 (UOW)。 *UOW* 是可以從 sys.dm_tran_locks 動態管理檢視的 request_owner_guid 資料行取得的 GUID。 您也可以從錯誤記錄檔或透過 MS DTC 監視器來取得 *UOW*。 如需有關監視分散式交易的詳細資訊，請參閱 MS DTC 文件集。  
  
 使用 KILL *UOW* 來終止孤立的分散式交易。 這些交易並未與任何真正的工作階段識別碼關聯，相反地，它們是人工地關聯於 session ID = '-2'。 透過查詢 sys.dm_tran_locks、sys.dm_exec_sessions 或 sys.dm_exec_requests 動態管理檢視中的 session ID 資料行，此工作階段識別碼使得識別被遺棄的交易變得更容易。  
  
 WITH STATUSONLY  
 針對因先前 KILL 陳述式而導致復原的指定 *session ID* 或 *UOW*，產生一份進度報告。 KILL WITH STATUSONLY 並不會終止或復原 *session ID* 或 *UOW*，此命令只會顯示目前的復原進度。  
  
## <a name="remarks"></a>Remarks  
 KILL 通常用來結束利用鎖定來封鎖其他重要處理序的處理序，或所執行的查詢在使用必要系統資源的處理序。 系統處理序和執行擴充預存程序的處理序無法結束。  
  
 請謹慎使用 KILL，特別是當重要處理序正在執行時。 您無法終止自己的處理序。 其他不應終止的處理序如下：  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
利用 @@SPID 來顯示目前工作階段的工作階段識別碼值。  
  
 若要取得使用中工作階段識別碼值的報告，您可以查詢 sys.dm_tran_locks、sys.dm_exec_sessions 以及 sys.dm_exec_requests 動態管理檢視中的 session_id 資料行。 您也可以檢視由 sp_who 系統預存程序傳回的 SPID 資料行。 如果正在進行特定 SPID 的復原，sp_who 結果集中適用於該 SPID 的 cmd 資料行就會指出 KILLED/ROLLBACK。  
  
 當特定連接對資料庫資源有鎖定並封鎖另一個連接的進度時，封鎖連接的工作階段識別碼會出現在 `blocking_session_id` 的 `sys.dm_exec_requests` 資料行或是由 `blk` 傳回的 `sp_who` 資料行中。  
  
 KILL 命令可用來解決不確定的分散式交易。 這些交易是未解決的分散式交易，之所以會發生是因為資料庫伺服器或 MS DTC 協調器發生了非計畫的重新啟動。 如需未決交易的詳細資訊，請參閱[使用標示的交易以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)中的＜兩階段交易認可＞一節。  
  
## <a name="using-with-statusonly"></a>使用 WITH STATUSONLY  
 只有因先前的 KILL *session ID*|*UOW* 陳述式而導致目前正在復原工作階段識別碼或 UOW 時，KILL WITH STATUSONLY 才會產生報告。 進度報告會指出已完成的回復量 (百分比) 及估計的剩下時間長度 (以秒為單位)，格式如下：  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 如果在執行 KILL *session ID*|*UOW* WITH STATUSONLY 陳述式時工作階段識別碼或 UOW 的復原已經完成，或者沒有復原中的工作階段識別碼或 UOW，KILL *session ID*|*UOW* WITH STATUSONLY 便會傳回下列錯誤：  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 您可以重複使用不含 WITH STATUSONLY 選項的相同 KILL *session ID*|*UOW* 陳述式來取得相同的狀態報告，但建議您不要這樣做。 如果復原已完成，且在執行新的 KILL 陳述式之前，已將工作階段識別碼重新指派給新的工作，則重複使用 KILL *session ID* 陳述式可能會終止新的處理序。 指定 WITH STATUSONLY 會防止發生這個情況。  
  
## <a name="permissions"></a>Permissions  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：** 需要 ALTER ANY CONNECTION 權限。 ALTER ANY CONNECTION 隨附在系統管理員 (sysadmin) 或處理序管理員 (processadmin) 固定伺服器角色的成員資格中。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]：** 需要 KILL DATABASE CONNECTION 權限。 伺服器層級主體登入具備 KILL DATABASE CONNECTION。  
  
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
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. 使用 KILL 來終止孤立的分散式交易  
 下列範例示範如何終止 *UOW* 為 `D5499C66-E398-45CA-BF7E-DC9C194B48CF` 的孤立分散式交易 (工作階段識別碼 = -2)。  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>另請參閱  
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
