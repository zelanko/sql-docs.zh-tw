---
title: sys.dm_exec_sessions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
caps.latest.revision: 60
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: fac27390005afad19f67c5e774c381067ee78745
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542098"
---
# <a name="sysdmexecsessions-transact-sql"></a>sys.dm_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上經過驗證的各個工作階段傳回一個資料列。 sys.dm_exec_sessions 是伺服器範圍檢視表，會顯示所有作用中使用者連接和內部工作的相關資訊。 這些資訊包括用戶端版本、用戶端程式名稱、用戶端登入時間、登入使用者、目前工作階段設定等。 請先使用 sys.dm_exec_sessions 檢視目前系統負載和找出所需的工作階段，然後再使用其他動態管理檢視或動態管理函數，取得該工作階段的更多資訊。  
  
 Sys.dm_exec_connections、 sys.dm_exec_sessions 和 sys.dm_exec_requests 動態管理檢視會對應到[sys.sysprocesses](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)系統資料表。  
  
> **注意：** 呼叫這個屬性從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_sessions**。  
  
|資料行名稱|資料類型|描述與特定版本資訊|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|識別每個使用中的主要連接所關聯的工作階段。 不可為 Null。|  
|login_time|**datetime**|建立工作階段的時間。 不可為 Null。|  
|host_name|**nvarchar(128)**|工作階段的特定用戶端工作站名稱。 內部工作階段的值為 NULL。 可為 Null。<br /><br /> **安全性注意事項：** 用戶端應用程式提供工作站名稱，而且可以提供不正確的資料。 請勿依賴 HOST_NAME 當做安全性功能。|  
|program_name|**nvarchar(128)**|起始工作階段的用戶端程式名稱。 內部工作階段的值為 NULL。 可為 Null。|  
|host_process_id|**int**|起始工作階段之用戶端程式的處理序識別碼。 內部工作階段的值為 NULL。 可為 Null。|  
|client_version|**int**|用戶端連接伺服器所用介面的 TDS 通訊協定版本。 內部工作階段的值為 NULL。 可為 Null。|  
|client_interface_name|**nvarchar(32)**|用戶端與伺服器通訊所使用的程式庫/驅動程式的名稱。 內部工作階段的值為 NULL。 可為 Null。|  
|security_id|**varbinary(85)**|與登入相關聯之 Microsoft Windows 安全性識別碼。 不可為 Null。|  
|login_name|**nvarchar(128)**|目前用來執行工作階段的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 如需建立工作階段的原始登入名稱，請參閱 original_login_name。 可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]驗證登入名稱或 Windows 驗證的網域使用者名稱。 不可為 Null。|  
|nt_domain|**nvarchar(128)**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 用戶端的 Windows 網域 (如果工作階段使用 Windows 驗證或信任連接)。 內部工作階段和非網域使用者的這個值為 NULL。 可為 Null。|  
|nt_user_name|**nvarchar(128)**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 用戶端的 Windows 使用者名稱 (如果工作階段使用 Windows 驗證或信任連接)。 內部工作階段和非網域使用者的這個值為 NULL。 可為 Null。|  
|status|**nvarchar(30)**|工作階段的狀態。 可能的值如下：<br /><br /> **執行**-目前執行中的一或多個要求<br /><br /> **睡眠**-目前執行中的任何要求<br /><br /> **休眠**– 工作階段因連接共用已重設，但現在處於登入前的狀態。<br /><br /> **Preconnect** -工作階段處於資源管理員分類。<br /><br /> 不可為 Null。|  
|context_info|**varbinary(128)**|工作階段的 CONTEXT_INFO 值。 內容資訊由使用者設定使用[SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md)陳述式。 可為 Null。|  
|cpu_time|**int**|工作階段所使用的 CPU 時間，以毫秒為單位。 不可為 Null。|  
|memory_usage|**int**|此工作階段所用記憶體的 8 KB 頁數。 不可為 Null。|  
|total_scheduled_time|**int**|工作階段 (內含要求) 排程執行的總時間，以毫秒為單位。 不可為 Null。|  
|total_elapsed_time|**int**|自工作階段建立以來的時間，以毫秒為單位。 不可為 Null。|  
|endpoint_id|**int**|工作階段所關聯的端點識別碼。 不可為 Null。|  
|last_request_start_time|**datetime**|工作階段最後一項要求的開始時間。 其中包括目前在執行的要求。 不可為 Null。|  
|last_request_end_time|**datetime**|工作階段要求最後完成的時間。 可為 Null。|  
|reads|**bigint**|在此工作階段期間，此工作階段的要求所執行的讀取次數。 不可為 Null。|  
|writes|**bigint**|在此工作階段期間，此工作階段的要求所執行的寫入次數。 不可為 Null。|  
|logical_reads|**bigint**|工作階段所執行的邏輯讀取數。 不可為 Null。|  
|is_user_process|**bit**|如果工作階段是系統工作階段，便是 0。 否則，便為 1。 不可為 Null。|  
|text_size|**int**|工作階段的 TEXTSIZE 設定。 不可為 Null。|  
|language|**nvarchar(128)**|工作階段的 LANGUAGE 設定。 可為 Null。|  
|date_format|**nvarchar(3)**|工作階段的 DATEFORMAT 設定。 可為 Null。|  
|date_first|**smallint**|工作階段的 DATEFIRST 設定。 不可為 Null。|  
|quoted_identifier|**bit**|工作階段的 QUOTED_IDENTIFIER 設定。 不可為 Null。|  
|arithabort|**bit**|工作階段的 ARITHABORT 設定。 不可為 Null。|  
|ansi_null_dflt_on|**bit**|工作階段的 ANSI_NULL_DFLT_ON 設定。 不可為 Null。|  
|ansi_defaults|**bit**|工作階段的 ANSI_DEFAULTS 設定。 不可為 Null。|  
|ansi_warnings|**bit**|工作階段的 ANSI_WARNINGS 設定。 不可為 Null。|  
|ansi_padding|**bit**|工作階段的 ANSI_PADDING 設定。 不可為 Null。|  
|ansi_nulls|**bit**|工作階段的 ANSI_NULLS 設定。 不可為 Null。|  
|concat_null_yields_null|**bit**|工作階段的 CONCAT_NULL_YIELDS_NULL 設定。 不可為 Null。|  
|transaction_isolation_level|**smallint**|工作階段的交易隔離等級。<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Snapshot<br /><br /> 不可為 Null。|  
|lock_timeout|**int**|工作階段的 LOCK_TIMEOUT 設定。 值會以毫秒來表示。 不可為 Null。|  
|deadlock_priority|**int**|工作階段的 DEADLOCK_PRIORITY 設定。 不可為 Null。|  
|row_count|**bigint**|到目前為止，工作階段傳回的資料列數。 不可為 Null。|  
|prev_error|**int**|在工作階段傳回的最後一個錯誤的識別碼。 不可為 Null。|  
|original_security_id|**varbinary(85)**|與 original_login_name 相關聯的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 安全性識別碼。 不可為 Null。|  
|original_login_name|**nvarchar(128)**|用戶端建立此工作階段所用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入名稱。 這可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證登入名稱、Windows 驗證網域使用者名稱或自主資料庫使用者。 請注意，在初始連接之後，工作階段可能已經歷過多次隱含或明確內容切換。 例如，如果[EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)用。 不可為 Null。|  
|last_successful_logon|**datetime**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 目前工作階段開始之前，original_login_name 上一次登入成功的時間。|  
|last_unsuccessful_logon|**datetime**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 目前工作階段開始之前，original_login_name 上一次登入不成功的時間。|  
|unsuccessful_logons|**bigint**|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 在 last_successful_logon 與 login_time 之間，original_login_name 嘗試登入不成功的次數。|  
|group_id|**int**|這個工作階段所屬之工作負載群組的識別碼。 不可為 Null。|  
|database_id|**smallint**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 每個工作階段之目前資料庫的識別碼。|  
|authenticating_database_id|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 驗證主體之資料庫的識別碼。 如果是登入，此值會是 0。 如果是自主資料庫使用者，此值會是自主資料庫的資料庫識別碼。|  
|open_transaction_count|**int**|**適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 每個工作階段的開啟交易數目。|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
## <a name="permissions"></a>Permissions  
每個人都可以看到自己的工作階段資訊。  
**[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:** 需要`VIEW SERVER STATE`權限[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]以查看在伺服器上的所有工作階段。  
**[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]:** 需要`VIEW DATABASE STATE`若要查看目前資料庫的所有連線。 `VIEW DATABASE STATE` 無法授與在`master`資料庫。 
  
  
## <a name="remarks"></a>備註  
 當**啟用通用條件合規性**啟用伺服器組態選項，則登入統計資料會顯示下列資料行。  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 如果沒有啟用這個選項，這些資料行會傳回 null 值。 如需如何設定此伺服器組態選項的詳細資訊，請參閱[符合通用準則已啟用伺服器組態選項](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)。  
 
 
 Azure SQL Database 上的系統管理員連線將會看到每個已驗證的工作階段的一個資料列。 "Sa"工作階段，會出現在結果集，並沒有造成任何影響的使用者配額的工作階段。 非系統管理員身分連線只會看到他們的資料庫使用者工作階段的相關資訊。
 
  
## <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|開啟/套用|關聯性|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|一對零或一對多|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|一對零或一對多|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|一對零或一對多|  
|sys.dm_exec_sessions|[sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|一對零或一對多|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|一對一|  
  
## <a name="examples"></a>範例  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. 尋找連接至伺服器的使用者  
 下列範例會找出連接伺服器的使用者，然後傳回每位使用者的工作階段數。  
  
```sql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>B. 尋找長時間執行的資料指標  
 下列範例會找出開啟超過一段特定時間的資料指標、資料指標的建立者以及資料指標所在工作階段。  
  
```sql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. 尋找具有尚未完成之異動的閒置工作階段  
 下列範例會找出有開啟交易且閒置的工作階段。 閒置工作階段是指目前未執行要求的工作階段。  
  
```sql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. 尋找有關查詢自有連接的資訊  
 收集查詢自有連接相關資訊的典型查詢。  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



