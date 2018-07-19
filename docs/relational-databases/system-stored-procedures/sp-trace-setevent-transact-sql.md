---
title: sp_trace_setevent & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_trace_setevent_TSQL
- sp_trace_setevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setevent
ms.assetid: 7662d1d9-6d0f-443a-b011-c901a8b77a44
caps.latest.revision: 49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 352d406b2c8735cb09787e9cd1554a4df7dd1bc0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38005770"
---
# <a name="sptracesetevent-transact-sql"></a>sp_trace_setevent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在追蹤中加入或移除事件或事件資料行。 **sp_trace_setevent**可能只能在已停止的現有追蹤上執行 (*狀態*是**0**)。 如果會傳回錯誤，此預存程序執行的追蹤中不存在，或其*狀態*不是**0**。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 請改用擴充事件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_trace_setevent [ @traceid = ] trace_id   
          , [ @eventid = ] event_id  
          , [ @columnid = ] column_id  
          , [ @on = ] on  
```  
  
## <a name="arguments"></a>引數  
 [ **@traceid=** ] *trace_id*  
 這是要修改的追蹤識別碼。 *trace_id*已**int**，沒有預設值。 使用者會利用這*trace_id*值來識別、 修改和控制追蹤。  
  
 [ **@eventid=** ] *event_id*  
 這是要開啟的事件識別碼。 *event_id*已**int**，沒有預設值。  
  
 這份資料表會列出能夠在追蹤中新增或移除的事件。  
  
|事件編號|事件名稱|描述|  
|------------------|----------------|-----------------|  
|0-9|已保留|已保留|  
|10|RPC:Completed|發生在遠端程序呼叫 (RPC) 已完成之時。|  
|11|RPC:Starting|發生在 RPC 已啟動之時。|  
|12|SQL:BatchCompleted|發生在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次已完成之時。|  
|13|SQL:BatchStarting|發生在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次已啟動之時。|  
|14|稽核登入|發生在使用者成功登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之時。|  
|15|稽核登出|發生在使用者登出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之時。|  
|16|Attention|發生在出現注意事項事件 (如用戶端中斷要求或中斷用戶端連接)。|  
|17|ExistingConnection|在啟動追蹤之前，偵測連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之使用者的所有活動。|  
|18|Audit Server Starts and Stops|發生在修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務狀態之時。|  
|19|DTCTransaction|追蹤兩個或多個資料庫之間的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分散式交易協調器 (MS DTC) 協調交易。|  
|20|Audit Login Failed|指出用戶端嘗試登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 失敗。|  
|21|EventLog|指出事件已記錄在 Windows 應用程式記錄檔中。|  
|22|ErrorLog|指出錯誤事件已記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔中。|  
|23|Lock:Released|指出已釋放資源 (如頁面) 的鎖定。|  
|24|Lock:Acquired|指出已取得資源 (如資料頁) 的鎖定。|  
|25|Lock:Deadlock|指出兩項同時發生的交易因試圖取得另一方交易所擁有之資源的不相容鎖定，彼此成為死結。|  
|26|Lock:Cancel|指出已取消資源鎖定之取得 (例如，由於死結之故)。|  
|27|Lock:Timeout|指出對於所需資源 (如頁面) 的鎖定要求，因其他交易持有資源的封鎖鎖定而逾時。 逾時由 @@LOCK_TIMEOUT函式，並可使用 SET LOCK_TIMEOUT 陳述式來設定。|  
|28|Degree of Parallelism Event (7.0 Insert)|發生在執行 SELECT、INSERT 或 UPDATE 陳述式之前。|  
|29-31|已保留|改用事件 28。|  
|32|已保留|已保留|  
|33|例外狀況|指出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發生例外狀況。|  
|34|SP:CacheMiss|指出在程序快取中找不到預存程序。|  
|35|SP:CacheInsert|指出項目已插入程序快取中。|  
|36|SP:CacheRemove|指出已從程序快取中移除項目。|  
|37|SP:Recompile|指出已重新編譯預存程序。|  
|38|SP:CacheHit|指出在程序快取中找到預存程序。|  
|39|已被取代|已被取代|  
|40|SQL:StmtStarting|發生在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式已啟動之時。|  
|41|SQL:StmtCompleted|發生在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式已完成之時。|  
|42|SP:Starting|指出已啟動預存程序。|  
|43|SP:Completed|指出已完成預存程序。|  
|44|SP:StmtStarting|指出已經開始執行預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|  
|45|SP:StmtCompleted|指出已經完成執行預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|  
|46|Object:Created|指出已建立物件，例如，CREATE INDEX、CREATE TABLE 和 CREATE DATABASE 等陳述式。|  
|47|Object:Deleted|指出已刪除物件，例如，DROP INDEX 和 DROP TABLE 陳述式。|  
|48|已保留||  
|49|已保留||  
|50|SQL Transaction|追蹤 [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN、COMMIT、SAVE 和 ROLLBACK TRANSACTION 等陳述式。|  
|51|Scan:Started|指出已啟動資料表或索引掃描。|  
|52|Scan:Stopped|指出已停止資料表或索引掃描。|  
|53|CursorOpen|指出 ODBC、OLE DB 或 DB-Library 已開啟 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的資料指標。|  
|54|TransactionLog|追蹤交易寫入交易記錄中。|  
|55|Hash Warning|指出未處理緩衝區資料分割的雜湊作業 (如雜湊聯結、雜湊彙總、雜湊聯集和雜湊相異)，已還原成替代計畫。 這可能是因為遞迴深度、資料偏斜、追蹤旗標或位元計數而發生。|  
|56-57|已保留||  
|58|Auto Stats|指出已自動更新索引統計資料。|  
|59|Lock:Deadlock Chain|針對每個會導向死結的事件而產生。|  
|60|Lock:Escalation|指出較細部鎖定已經轉換成較廣泛鎖定 (例如，頁面鎖定已擴大或轉換成 TABLE 或 HoBT 鎖定)。|  
|61|OLE DB Errors|指出發生 OLE DB 錯誤。|  
|62-66|已保留||  
|67|Execution Warnings|指出在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式或預存程序期間所發生的任何警告。|  
|68|Showplan Text (Unencoded)|顯示所執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式之計畫樹狀結構。|  
|69|Sort Warnings|指出不適合在記憶體中的排序作業。 不包括包含建立索引的排序作業；只包括在查詢中的排序作業 (例如，在 SELECT 陳述式中所用的 ORDER BY 子句)。|  
|70|CursorPrepare|指出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的資料指標已備妥，可供 ODBC、OLE DB 或 DB-Library 使用。|  
|71|Prepare SQL|ODBC、OLE DB 或 DB-Library 已備妥一或多個待用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|  
|72|Exec Prepared SQL|ODBC、OLE DB 或 DB-Library 已執行一或多個備妥的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|  
|73|Unprepare SQL|ODBC、OLE DB 或 DB-Library 已取消準備 (刪除) 一或多個備妥的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。|  
|74|CursorExecute|執行 ODBC、OLE DB 或 DB-Library 先前已備妥的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式資料指標。|  
|75|CursorRecompile|已直接重新編譯或因結構描述變更而重新編譯 ODBC 或 DB-Library 所開啟的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式資料指標。<br /><br /> 針對 ANSI 和非 ANSI 資料指標而觸發。|  
|76|CursorImplicitConversion|由 [!INCLUDE[tsql](../../includes/tsql-md.md)] 轉換成其他類型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式資料指標。<br /><br /> 針對 ANSI 和非 ANSI 資料指標而觸發。|  
|77|CursorUnprepare|ODBC、OLE DB 或 DB-Library 取消準備 (刪除) 已備妥的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式資料指標。|  
|78|CursorClose|關閉 ODBC、OLE DB 或 DB-Library 先前已開啟的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式資料指標。|  
|79|Missing Column Statistics|無法取得最佳化工具可能用到的資料行統計資料。|  
|80|Missing Join Predicate|正在執行沒有聯結述詞的查詢。 這可能造成長時間執行的查詢。|  
|81|Server Memory Change|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體用量已增加或減少 1 MB 或最大伺服器記憶體的 5%，兩者中取較大者。|  
|82-91|User Configurable (0 -9)|使用者所定義的事件資料。|  
|92|Data File Auto Grow|指出伺服器已自動擴充資料檔。|  
|93|Log File Auto Grow|指出伺服器已自動擴充記錄檔。|  
|94|Data File Auto Shrink|指出伺服器已自動壓縮資料檔。|  
|95|Log File Auto Shrink|指出伺服器已自動壓縮記錄檔。|  
|96|Showplan Text|顯示查詢最佳化工具的 SQL 陳述式查詢計畫樹狀目錄。 請注意， **TextData**資料行不包含此事件的顯示計畫。|  
|97|Showplan All|顯示含有所執行的 SQL 陳述式之完整編譯階段詳細資料的查詢計畫。 請注意， **TextData**資料行不包含此事件的顯示計畫。|  
|98|Showplan Statistics Profile|顯示含有所執行的 SQL 陳述式之完整執行階段詳細資料的查詢計畫。 請注意， **TextData**資料行不包含此事件的顯示計畫。|  
|99|已保留||  
|100|RPC Output Parameter|產生每個 RPC 的參數輸出值。|  
|101|已保留||  
|102|Audit Database Scope GDR|發生在每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的任何使用者對僅限資料庫的動作 (例如授與資料庫的權限) 發出陳述式權限的 GRANT、DENY、REVOKE 之時。|  
|103|Audit Object GDR Event|發生在每次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的任何使用者發出物件權限的 GRANT、DENY、REVOKE 之時。|  
|104|Audit AddLogin Event|發生時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]加入或移除登入的**sp_addlogin**並**sp_droplogin**。|  
|105|Audit Login GDR Event|發生於加入或移除; Windows 登入權限針對**sp_grantlogin**， **sp_revokelogin**，並**sp_denylogin**。|  
|106|Audit Login Change Property Event|發生於修改登入，密碼以外的屬性;針對**sp_defaultdb**並**sp_defaultlanguage**。|  
|107|Audit Login Change Password Event|發生在變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入密碼之時。<br /><br /> 並未記錄密碼。|  
|108|Audit Add Login to Server Role Event|發生於加入或移除從固定的伺服器角色; 登入針對**sp_addsrvrolemember**，並**sp_dropsrvrolemember**。|  
|109|Audit Add DB User Event|發生於加入或移除的資料庫使用者身分登入 (Windows 或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) 到資料庫，如**sp_grantdbaccess**， **sp_revokedbaccess**， **sp_adduser**，並**sp_dropuser**。|  
|110|Audit Add Member to DB Role Event|登入新增或移除了資料庫使用者 （固定或使用者定義） 至資料庫時，就會發生針對**sp_addrolemember**， **sp_droprolemember**，並**sp_changegroup**。|  
|111|Audit Add Role Event|登入新增或移除了資料庫使用者至資料庫時，就會發生針對**sp_addrole**並**sp_droprole**。|  
|112|Audit App Role Change Password Event|發生在變更應用程式角色的密碼之時。|  
|113|Audit Statement Permission Event|發生在使用陳述式權限 (如 CREATE TABLE) 之時。|  
|114|Audit Schema Object Access Event|發生在使用物件權限 (如 SELECT) 成功或失敗之時。|  
|115|Audit Backup/Restore Event|發生在發出 BACKUP 或 RESTORE 命令之時。|  
|116|Audit DBCC Event|發生在發出 DBCC 命令之時。|  
|117|Audit Change Audit Event|發生在修改稽核追蹤之時。|  
|118|Audit Object Derived Permission Event|發生在發出 CREATE、ALTER 和 DROP 物件命令之時。|  
|119|OLEDB Call Event|發生在發出分散式查詢和遠端預存程序的 OLE DB 提供者呼叫之時。|  
|120|OLEDB QueryInterface Event|發生於 OLE DB **QueryInterface**呼叫的分散式的查詢和遠端預存程序。|  
|121|OLEDB DataRead Event|發生在向 OLE DB 提供者發出資料要求呼叫之時。|  
|122|Showplan XML|發生在執行 SQL 陳述式之時。 請併入這個事件來識別顯示計畫操作員。 每個事件都會儲存在格式正確的 XML 文件中。 請注意，**二進位**這個事件的資料行包含編碼的顯示計畫。 請使用 SQL Server Profiler 開啟追蹤並檢視執行程序表。|  
|123|SQL:FullTextQuery|發生在執行全文檢索查詢之時。|  
|124|Broker:Conversation|報告 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 交談進度。|  
|125|Deprecation Announcement|發生在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將移除所用的功能之時。|  
|126|Deprecation Final Support|發生在未來 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的主要版本將移除所用的功能之時。|  
|127|Exchange Spill Event|發生於平行查詢計畫中的通訊緩衝區已暫時寫入**tempdb**資料庫。|  
|128|Audit Database Management Event|發生在建立、改變或卸除資料庫之時。|  
|129|Audit Database Object Management Event|發生在執行資料庫物件 (如結構描述) 的 CREATE、ALTER 或 DROP 陳述式之時。|  
|130|Audit Database Principal Management Event|發生在從資料庫中建立、改變或卸除主體 (如使用者) 之時。|  
|131|Audit Schema Object Management Event|發生在建立、改變或卸除伺服器物件之時。|  
|132|Audit Server Principal Impersonation Event|發生在伺服器範圍內有模擬情況 (如 EXECUTE AS LOGIN) 之時。|  
|133|Audit Database Principal Impersonation Event|發生在資料庫範圍內有模擬情況 (如 EXECUTE AS USER 或 SETUSER) 之時。|  
|134|Audit Server Object Take Ownership Event|發生在伺服器範圍內的物件擁有者有了改變之時。|  
|135|Audit Database Object Take Ownership Event|發生在資料庫範圍內的物件擁有者有了改變之時。|  
|136|Broker:Conversation Group|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 建立新的交談群組或卸除現有的交談群組之時。|  
|137|Blocked Process Report|發生在封鎖處理序超出指定時間量之時。 不包括系統處理序或在不可偵測死結的資源上等候的處理序。 使用**sp_configure**設定產生報告的臨界值和頻率。|  
|138|Broker:Connection|報告 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 所管理的傳輸連接狀態。|  
|139|Broker:Forwarded Message Sent|當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 轉送訊息時發生。|  
|140|Broker:Forwarded Message Dropped|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 卸除即將轉送的訊息之時。|  
|141|Broker:Message Classify|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 決定訊息路由之時。|  
|142|Broker:Transmission|指出 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 傳輸層發生錯誤。 錯誤號碼和狀態值會指出錯誤來源。|  
|143|Broker:Queue Disabled|指出偵測到有害訊息，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 佇列有五個連續的交易回復。 事件包含有害訊息所在之佇列的資料庫識別碼和佇列識別碼。|  
|144-145|已保留||  
|146|Showplan XML Statistics Profile|發生在執行 SQL 陳述式之時。 它會識別顯示計畫操作員，且會顯示完整的編譯階段資料。 請注意，**二進位**這個事件的資料行包含編碼的顯示計畫。 請使用 SQL Server Profiler 開啟追蹤並檢視執行程序表。|  
|148|Deadlock Graph|發生在因獲得鎖定的嘗試是死結的一部分，且已被選為死結的犧牲者，因而取消嘗試之時。 提供死結的 XML 描述。|  
|149|Broker:Remote Message Acknowledgement|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 傳送或接收訊息收條之時。|  
|150|Trace File Close|發生在追蹤檔換用期間關閉追蹤檔之時。|  
|151|已保留||  
|152|Audit Change Database Owner|發生在利用 ALTER AUTHORIZATION 來變更資料庫擁有者，且檢查執行這項動作的權限之時。|  
|153|Audit Schema Object Take Ownership Event|發生在利用 ALTER AUTHORIZATION 來將擁有者指派給物件，且檢查執行這項動作的權限之時。|  
|154|已保留||  
|155|FT:Crawl Started|發生在開始全文檢索搜耙 (擴展) 之時。 用來檢查工作者工作是否已取出搜耙要求。|  
|156|FT:Crawl Stopped|發生在全文檢索搜耙 (擴展) 停止之時。 停止發生在搜耙已順利完成或發生嚴重錯誤之時。|  
|157|FT:Crawl Aborted|發生在全文檢索搜耙期間發生例外狀況之時。 通常會造成停止全文檢索搜耙。|  
|158|Audit Broker Conversation|報告 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話安全性的相關稽核訊息。|  
|159|Audit Broker Login|報告 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 傳輸安全性的相關稽核訊息。|  
|160|Broker:Message Undeliverable|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 無法保留已收到且應該已傳遞給服務的訊息之時。|  
|161|Broker:Corrupted Message|發生在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 收到損毀的訊息之時。|  
|162|User Error Message|顯示在發生錯誤或例外狀況時，使用者所見到的錯誤訊息。|  
|163|Broker:Activation|發生在佇列監視器開始啟用預存程序、傳送 QUEUE_ACTIVATION 通知之時，或佇列監視器所開始的啟用預存程序結束之時。|  
|164|Object:Altered|發生在改變資料庫物件之時。|  
|165|Performance statistics|發生在已初次快取編譯的查詢計畫之時，以及從計畫快取中重新編譯或移除已編譯的查詢計畫之時。|  
|166|SQL:StmtRecompile|發生在陳述式層級重新編譯之時。|  
|167|Database Mirroring State Change|發生在鏡像資料庫狀態改變之時。|  
|168|Showplan XML For Query Compile|發生在編譯 SQL 陳述式之時。 它會顯示完整的編譯階段資料。 請注意，**二進位**這個事件的資料行包含編碼的顯示計畫。 請使用 SQL Server Profiler 開啟追蹤並檢視執行程序表。|  
|169|Showplan All For Query Compile|發生在編譯 SQL 陳述式之時。 它會顯示完整的編譯階段資料。 用來識別顯示計畫操作員。|  
|170|Audit Server Scope GDR Event|指出在伺服器範圍中，發生授與、拒絕或撤銷權限的事件，如建立一項登入。|  
|171|Audit Server Object GDR Event|指出發生結構描述物件 (如資料表或函數) 的授與、拒絕或撤銷事件。|  
|172|Audit Database Object GDR Event|指出發生資料庫物件 (如組件和結構描述) 的授與、拒絕或撤銷事件。|  
|173|Audit Server Operation Event|發生在使用安全性稽核作業 (如改變設定、資源、外部存取或權限) 之時。|  
|175|Audit Server Alter Trace Event|發生在陳述式檢查 ALTER TRACE 權限之時。|  
|176|Audit Server Object Management Event|發生在建立、改變或卸除伺服器物件之時。|  
|177|Audit Server Principal Management Event|發生在建立、改變或卸除伺服器主體之時。|  
|178|Audit Database Operation Event|發生在執行資料庫作業 (如檢查點或訂閱查詢通知) 之時。|  
|180|Audit Database Object Access Event|發生在存取資料庫物件 (如結構描述) 之時。|  
|181|TM: Begin Tran starting|發生在 BEGIN TRANSACTION 要求啟動之時。|  
|182|TM: Begin Tran completed|發生在 BEGIN TRANSACTION 要求完成之時。|  
|183|TM: Promote Tran starting|發生在 PROMOTE TRANSACTION 要求啟動之時。|  
|184|TM: Promote Tran completed|發生在 PROMOTE TRANSACTION 要求完成之時。|  
|185|TM: Commit Tran starting|發生在 COMMIT TRANSACTION 要求啟動之時。|  
|186|TM: Commit Tran completed|發生在 COMMIT TRANSACTION 要求完成之時。|  
|187|TM: Rollback Tran starting|發生在 ROLLBACK TRANSACTION 要求啟動之時。|  
|188|TM: Rollback Tran completed|發生在 ROLLBACK TRANSACTION 要求完成之時。|  
|189|Lock: Timeout (timeout > 0)|發生在資源 (如頁面) 鎖定要求逾時之時。|  
|190|Progress Report: Online Index Operation|在建置處理序執行時，報告線上索引建置作業的進度。|  
|191|TM: Save Tran starting|發生在 SAVE TRANSACTION 要求啟動之時。|  
|192|TM: Save Tran completed|發生在 SAVE TRANSACTION 要求完成之時。|  
|193|Background Job Error|發生在背景作業異常結束之時。|  
|194|OLEDB Provider Information|發生在執行分散式查詢及收集提供者連接的對應資訊之時。|  
|195|Mount Tape|發生在收到磁帶掛載要求之時。|  
|196|Assembly Load|發生在要求載入 CLR 組件之時。|  
|197|已保留||  
|198|XQuery Static Type|發生在執行 XQuery 運算式之時。 這個事件類別提供 XQuery 運算式的靜態類型。|  
|199|QN: subscription|發生在無法訂閱查詢登錄之時。 **TextData**資料行包含事件的相關資訊。|  
|200|QN: parameter table|使用中之訂閱的相關資訊儲存在內部參數資料表中。 當建立或刪除參數資料表時，便會發生這個事件。 這些資料表通常是在重新啟動資料庫時建立或刪除。 **TextData**資料行包含事件的相關資訊。|  
|201|QN: template|查詢範本代表一個訂閱查詢類別。 相同類別中的查詢，除了參數值之外，通常都是相同的。 當新的訂閱要求是在已存在的類別 (Match)、新的類別 (Create) 或卸除的類別 (Drop) 中，就會發生這個事件類別，表示清除不含使用中訂閱之查詢類別的範本。 **TextData**資料行包含事件的相關資訊。|  
|202|QN: dynamics|追蹤查詢通知的內部活動。 **TextData**資料行包含事件的相關資訊。|  
|212|點陣圖警告|指出查詢中已經停用點陣圖篩選。|  
|213|Database Suspect Data Page|指出頁面何時加入至**suspect_pages**資料表中**msdb**。|  
|214|CPU threshold exceeded|指出資源管理員偵測到查詢已超過 CPU 臨界值 (REQUEST_MAX_CPU_TIME_SEC)。|  
|215|指出 LOGON 觸發程序或資源管理員分類函數開始執行。|指出 LOGON 觸發程序或資源管理員分類函數開始執行。|  
|216|PreConnect:Completed|指出 LOGON 觸發程序或資源管理員分類函數已完成執行。|  
|217|Plan Guide Successful|指出 SQL Server 已成功為包含計畫指南的查詢或批次產生執行計畫。|  
|218|Plan Guide Unsuccessful|指出 SQL Server 無法為包含計畫指南的查詢或批次產生執行計畫。 SQL Server 嘗試在未套用計畫指南的情況下，為這個查詢或批次產生執行計畫。 無效的計畫指南可能是造成這個問題的原因。 您可以使用 sys.fn_validate_plan_guide 系統函數驗證此計畫指南。|  
|235|Audit Fulltext||  
  
 [ **@columnid=** ] *column_id*  
 這是要加入之事件資料行的識別碼。 *column_id*已**int**，沒有預設值。  
  
 下表列出能夠新增的事件資料行。  
  
|資料行編號|資料行名稱|描述|  
|-------------------|-----------------|-----------------|  
|1|**TextData**|這是一個文字值，會隨著追蹤所擷取的事件類別而不同。|  
|2|**BinaryData**|這是一個二進位值，會隨著追蹤所擷取的事件類別而不同。|  
|3|**DatabaseID**|使用指定的資料庫識別碼*資料庫*陳述式或如果沒有使用的預設資料庫*資料庫*指定連接發出陳述式。<br /><br /> 您可以利用 DB_ID 函數來決定資料庫的值。|  
|4|**TransactionID**|由系統指派給交易的識別碼。|  
|5|**LineNumber**|包含錯誤行號。 如果事件與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (例如 **SP:StmtStarting**) 有關， **LineNumber** 便會將陳述式的行數包含在預存程序或批次中。|  
|6|**NTUserName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者名稱。|  
|7|**NTDomainName**|使用者所隸屬的 Windows 網域。|  
|8|**HostName**|引發要求的用戶端電腦名稱。|  
|9|**ClientProcessID**|用戶端電腦指派給執行用戶端應用程式之處理序的識別碼。|  
|10|**ApplicationName**|建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體之連接的用戶端應用程式名稱。 這個資料行會填入應用程式所傳送的值，而非程式的顯示名稱。|  
|11|**LoginName**|用戶端的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。|  
|12|**SPID**|由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指派給用戶端關聯之處理序的伺服器處理序識別碼。|  
|13|**有效期間**|事件所經歷的時間 (以百萬分之一秒為單位)。 這個資料行不是由 Hash Warning 事件來擴展。|  
|14|**StartTime**|事件的開始時間 (如果可以取得的話)。|  
|15|**EndTime**|事件結束的時間。 啟動事件類別 (如 **SQL:BatchStarting** 或 **SP:Starting**) 不會擴展這個資料行。 它也不會填入所**Hash Warning**事件。|  
|16|**Reads**|伺服器代表事件執行的邏輯磁碟讀取數。 此資料行不會填入**鎖定： 發行**事件。|  
|17|**Writes**|伺服器代表事件執行的實體磁碟寫入數。|  
|18|**CPU**|事件所用的 CPU 時間 (以毫秒為單位)。|  
|19|**Permissions**|代表權限的點陣圖；供安全性稽核使用。|  
|20|**Severity**|例外狀況的嚴重性層級。|  
|21|**EventSubClass**|事件子類別的類型。 所有事件類別的這個資料行都不會擴展。|  
|22|**Exchange Spill**|系統指派給物件的識別碼。|  
|23|**成功**|嘗試使用權限成功；用來進行稽核。<br /><br /> **1** = 成功**0** = 失敗|  
|24|**IndexID**|事件所影響之物件的索引識別碼。 若要確定物件的索引識別碼，請使用 **sysindexes** 系統資料表的 **indid** 資料行。|  
|25|**IntegerData**|這是一個整數值，會隨著追蹤所擷取的事件類別而不同。|  
|26|**ServerName**|執行個體名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以是*servername*或是*servername\instancename*，所追蹤。|  
|27|**EventClass**|正在記錄之事件類別的類型。|  
|28|**ObjectType**|物件類型，例如資料表、函數或預存程序。|  
|29|**NestLevel**|這個預存程序正在執行的巢狀層級。 請參閱[@@NESTLEVEL &#40;TRANSACT-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)。|  
|30|**State**|發生錯誤時的伺服器狀態。|  
|31|**錯誤**|錯誤號碼。|  
|32|**模式**|取得的鎖定之鎖定模式。 此資料行不會填入**鎖定： 發行**事件。|  
|33|**Handle**|事件所參考之物件的控制代碼。|  
|34|**ObjectName**|所存取之物件的名稱。|  
|35|**DatabaseName**|使用指定的資料庫名稱*資料庫*陳述式。|  
|36|**FileName**|修改的檔案名稱之邏輯名稱。|  
|37|**OwnerName**|參考的物件之擁有者名稱。|  
|38|**RoleName**|陳述式的目標資料庫或伺服器範圍的角色名稱。|  
|39|**TargetUserName**|某動作的目標使用者名稱。|  
|40|**DBUserName**|用戶端的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫使用者名稱。|  
|41|**LoginSid**|已登入之使用者的安全性識別碼 (SID)。|  
|42|**TargetLoginName**|某動作的目標登入名稱。|  
|43|**TargetLoginSid**|某動作之目標登入的 SID。|  
|44|**ColumnPermissions**|資料行層級的權限狀態；供安全性稽核使用。|  
|45|**LinkedServerName**|連結伺服器的名稱。|  
|46|**ProviderName**|OLE DB 提供者的名稱。|  
|47|**MethodName**|OLE DB 方法的名稱。|  
|48|**RowCounts**|批次中的資料列數。|  
|49|**RequestID**|包含陳述式之要求的識別碼。|  
|50|**XactSequence**|用來描述目前交易的 Token。|  
|51|**EventSequence**|此事件的序號。|  
|52|**BigintData1**|**bigint**視追蹤所擷取的事件類別而定的值。|  
|53|**BigintData2**|**bigint**視追蹤所擷取的事件類別而定的值。|  
|54|**GUID**|這是一個 GUID 值，會隨著追蹤所擷取的事件類別而不同。|  
|55|**IntegerData2**|這是一個整數值，會隨著追蹤所擷取的事件類別而不同。|  
|56|**ObjectID2**|相關物件或實體的識別碼 (如果可以取得的話)。|  
|57|**型別**|這是一個整數值，會隨著追蹤所擷取的事件類別而不同。|  
|58|**OwnerID**|擁有鎖定的物件類型。 只適用於鎖定事件。|  
|59|**ParentName**|物件所在結構描述的名稱。|  
|60|**IsSystem**|指出事件是發生在系統處理序或使用者處理序。<br /><br /> **1** = 系統<br /><br /> **0** = 使用者。|  
|61|**Offset**|預存程序或批次內之陳述式的起始位移。|  
|62|**SourceDatabaseID**|物件來源所在的資料庫識別碼。|  
|63|**SqlHandle**|這是一個 64 位元雜湊，以隨選查詢的文字或 SQL 物件的資料庫和物件識別碼為基礎。 這個值可以傳給 **sys.dm_exec_sql_text()** ，以擷取相關聯的 SQL 文字。|  
|64|**SessionLoginName**|引發工作階段的使用者登入名稱。 例如，如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Login1 **連接到** ，卻以 **Login2**執行陳述式，則 **SessionLoginName** 會顯示 **Login1**，而 **LoginName** 會顯示 **Login2**。 此資料行會同時顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 登入。|  
  
 **[ @on=]** *上*  
 指定開啟 ON (1) 或關閉 OFF (0) 事件。 *在 *已**元**，沒有預設值。  
  
 如果*上*設為**1**，並*column_id* NULL，則事件會設為 ON 且已清除所有資料行。 如果*column_id*不是 null，則該事件的資料行設為 ON。  
  
 如果*上*設為**0**，並*column_id*是 NULL，則事件會變成 OFF 且已清除所有資料行。 如果*column_id*不是 null，則資料行已關閉。  
  
 這份表格說明之間的互動**@on**並**@columnid**。  
  
|@on|@columnid|結果|  
|---------|---------------|------------|  
|ON (**1**)|NULL|開啟事件 (ON)。<br /><br /> 清除所有資料行。|  
||NOT NULL|開啟指定事件的資料行 (ON)。|  
|OFF (**0**)|NULL|關閉事件 (OFF)。<br /><br /> 清除所有資料行。|  
||NOT NULL|關閉指定事件的資料行 (OFF)。|  
  
## <a name="return-code-values"></a>傳回碼值  
 下表描述在預存程序完成之後，使用者可能得到的代碼值。  
  
|傳回碼|描述|  
|-----------------|-----------------|  
|0|沒有錯誤。|  
|1|未知的錯誤。|  
|2|追蹤目前在執行中。 此時變更追蹤會產生錯誤。|  
|3|指定的事件無效。 事件可能不存在，也可能是不適合預存程序。|  
|4|指定的資料行無效。|  
|9|指定的追蹤控制代碼無效。|  
|11|在內部使用指定的資料行，無法將它移除。|  
|13|記憶體用完。 當沒有足夠的記憶體可以執行指定的動作時，便傳回這個代碼。|  
|16|函數對於這項追蹤無效。|  
  
## <a name="remarks"></a>備註  
 **sp_trace_setevent**會執行許多先前執行較早版本中可用的擴充預存程序的動作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 使用**sp_trace_setevent**不要使用下列：  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_eventclassrequired**  
  
-   **xp_trace_seteventclassrequired**  
  
 使用者必須執行**sp_trace_setevent**每個資料行加入每個事件。 每個在執行期間，如果**@on**設定為**1**， **sp_trace_setevent**將指定的事件加入至追蹤的事件清單。 如果**@on**設定為**0**， **sp_trace_setevent**從清單中移除指定的事件。  
  
 參數的所有 SQL 追蹤預存程序 (**sp_trace_xx**) 都有強制類型。 如果沒有依照引數描述所指定，以正確的輸入參數資料類型來呼叫這些參數，預存程序會傳回錯誤。  
  
 如需使用追蹤預存程序的範例，請參閱[建立追蹤 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有 ALTER TRACE 權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_trace_geteventinfo &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [SQL Server 事件類別參考](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)  
  
  
