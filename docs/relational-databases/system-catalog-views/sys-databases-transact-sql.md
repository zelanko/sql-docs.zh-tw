---
title: sys.databases (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- databases
- databases_TSQL
- sys.databases
- sys.databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.databases catalog view
ms.assetid: 46c288c1-3410-4d68-a027-3bbf33239289
caps.latest.revision: 152
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fd67499570aec52824789d72ddf8333899e9ade7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39566192"
---
# <a name="sysdatabases-transact-sql"></a>sys.databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體中的每個資料庫，各包含一個資料列。  
  
 如果資料庫不是`ONLINE`，或`AUTO_CLOSE`設為`ON`和資料庫已關閉，某些資料行的值可能`NULL`。 如果資料庫是`OFFLINE`，低權限的使用者看不到 對應的資料列。 若要查看對應的資料列，如果資料庫位於`OFFLINE`，使用者必須具備至少`ALTER ANY DATABASE`伺服器層級權限，或有`CREATE DATABASE`中的權限`master`資料庫。  
  

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料庫的名稱，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]伺服器內是唯一的。|  
|**database_id**|**int**|資料庫的識別碼，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]伺服器內是唯一的。|  
|**sys.databases**|**int**|Non-NULL = 這個資料庫快照集的來源資料庫識別碼。<br /> NULL = 不是資料庫快照集。|  
|**owner_sid**|**varbinary(85)**|資料庫外部擁有者的 SID (安全性識別碼)，亦即在伺服器註冊所用的識別碼。 誰可以擁有資料庫的相關資訊，請參閱**資料庫的 ALTER AUTHORIZATION**一節[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)。|  
|**create_date**|**datetime**|資料庫建立或重新命名的日期。 針對**tempdb**，這個值會變更每次重新啟動伺服器。|  
|**compatibility_level**|**tinyint**|對應於與行為相容之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的整數：<br /> **值**:**適用於**<br /> 70:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 80:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /> 90:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /> 100:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 110:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 120:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 130:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] |  
|**collation_name**|**sysname**|資料庫的定序。 它是資料庫中的預設定序。<br /> NULL = 資料庫不在線上，或者 AUTO_CLOSE 設為 ON 且資料庫已關閉。|  
|**user_access**|**tinyint**|使用者存取設定：<br /> 0 = 指定了 MULTI_USER<br /> 1 = 指定了 SINGLE_USER<br /> 2 = 指定了 RESTRICTED_USER|  
|**user_access_desc**|**nvarchar(60)**|使用者存取設定的描述。|  
|**is_read_only**|**bit**|1 = 資料庫是 READ_ONLY<br /> 0 = 資料庫是 READ_WRITE|  
|**is_auto_close_on**|**bit**|1 = AUTO_CLOSE 是 ON<br /> 0 = AUTO_CLOSE 是 OFF|  
|**is_auto_shrink_on**|**bit**|1 = AUTO_SHRINK 是 ON<br /> 0 = AUTO_SHRINK 是 OFF|  
|**state**|**tinyint**|**值&#124;適用於**<br /> 0 = ONLINE  <br /> 1 = RESTORING <br /> 2 = 正在復原：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 3 = recovery_pending，否則便：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 4 = SUSPECT <br /> 5 = 緊急：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 6 = 離線：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 7 = 正在複製： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /> 10 = OFFLINE_SECONDARY: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] <br /><br /> **注意：** 對於 Alwayson 資料庫查詢`database_state`或是`database_state_desc`的資料行[sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。|  
|**state_desc**|**nvarchar(60)**|資料庫狀態的描述。 請參閱狀態。|  
|**is_in_standby**|**bit**|還原記錄的資料庫是唯讀資料庫。|  
|**is_cleanly_shutdown**|**bit**|1 = 資料庫完全關閉；不必在啟動時復原<br /> 0 = 資料庫並未完全關閉；必須在啟動時復原|  
|**is_supplemental_logging_enabled**|**bit**|1 = SUPPLEMENTAL_LOGGING 是 ON<br /> 0 = SUPPLEMENTAL_LOGGING 是 OFF|  
|**snapshot_isolation_state**|**tinyint**|允許進行的快照集隔離交易狀態，由 ALLOW_SNAPSHOT_ISOLATION 選項設定：<br /> 0 = 快照集隔離狀態是 OFF (預設值)。 不接受快照集隔離。<br /> 1 = 快照集隔離狀態是 ON。 接受快照集隔離。<br /> 2 = 快照集隔離狀態正轉移為 OFF 狀態。 所有的交易都把自己的修改版本化了。 新交易無法利用快照集隔離加以啟動。 資料庫仍然保持在轉移為 OFF 狀態的過渡時期，必須等到在執行 ALTER DATABASE 時，所有使用中的交易可以完成為止。<br /> 3 = 快照集隔離狀態正轉移為 ON 狀態。 新交易都把自己的修改版本化了。 除非快照集隔離狀態變成 1 (ON)，否則交易無法使用快照集隔離。 資料庫仍然保持在轉移為 ON 狀態的過渡時期，必須等到在執行 ALTER DATABASE 時，所有使用中的更新交易可以完成為止。|  
|**snapshot_isolation_state_desc**|**nvarchar(60)**|允許進行的快照集隔離交易狀態的描述，由 ALLOW_SNAPSHOT_ISOLATION 選項設定。|  
|**is_read_committed_snapshot_on**|**bit**|1 = READ_COMMITTED_SNAPSHOT 選項為 ON。 讀取認可隔離等級下的讀取作業是以快照集掃描為基礎，沒有取得鎖定。<br /> 0 = READ_COMMITTED_SNAPSHOT 選項為 OFF (預設)。 讀取認可隔離等級下的讀取作業是使用共用鎖定。|  
|**recovery_model**|**tinyint**|所選的復原模式：<br /> 1 = FULL<br /> 2 = BULK_LOGGED<br /> 3 = SIMPLE|  
|**recovery_model_desc**|**nvarchar(60)**|所選之復原模式的描述。|  
|**page_verify_option**|**tinyint**|PAGE_VERIFY 選項的設定：<br /> 0 = NONE<br /> 1 = TORN_PAGE_DETECTION<br /> 2 = CHECKSUM|  
|**page_verify_option_desc**|**nvarchar(60)**|PAGE_VERIFY 選項設定的描述。|  
|**is_auto_create_stats_on**|**bit**|1 = AUTO_CREATE_STATISTICS 是 ON<br /> 0 = AUTO_CREATE_STATISTICS 是 OFF|  
|**is_auto_create_stats_incremental_on**|**bit**|表示 Auto Stats 之累加選項的預設設定。<br /> 0 = 自動建立非累加的統計資料<br /> 1 = 盡可能自動建立累加的統計資料<br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**is_auto_update_stats_on**|**bit**|1 = AUTO_UPDATE_STATISTICS 是 ON<br /> 0 = AUTO_UPDATE_STATISTICS 是 OFF|  
|**is_auto_update_stats_async_on**|**bit**|1 = AUTO_UPDATE_STATISTICS_ASYNC 是 ON<br /> 0 = AUTO_UPDATE_STATISTICS_ASYNC 是 OFF|  
|**is_ansi_null_default_on**|**bit**|1 = ANSI_NULL_DEFAULT 是 ON<br /> 0 = ANSI_NULL_DEFAULT 是 OFF|  
|**is_ansi_nulls_on**|**bit**|1 = ANSI_NULLS 是 ON<br /> 0 = ANSI_NULLS 是 OFF|  
|**is_ansi_padding_on**|**bit**|1 = ANSI_PADDING 是 ON<br /> 0 = ANSI_PADDING 是 OFF|  
|**is_ansi_warnings_on**|**bit**|1 = ANSI_WARNINGS 是 ON<br /> 0 = ANSI_WARNINGS 是 OFF|  
|**is_arithabort_on**|**bit**|1 = ARITHABORT 是 ON<br /> 0 = ARITHABORT 是 OFF|  
|**is_concat_null_yields_null_on**|**bit**|1 = CONCAT_NULL_YIELDS_NULL 是 ON<br /> 0 = CONCAT_NULL_YIELDS_NULL 是 OFF|  
|**is_numeric_roundabort_on**|**bit**|1 = NUMERIC_ROUNDABORT 是 ON<br /> 0 = NUMERIC_ROUNDABORT 是 OFF|  
|**is_quoted_identifier_on**|**bit**|1 = QUOTED_IDENTIFIER 是 ON<br /> 0 = QUOTED_IDENTIFIER 是 OFF|  
|**is_recursive_triggers_on**|**bit**|1 = RECURSIVE_TRIGGERS 是 ON<br /> 0 = RECURSIVE_TRIGGERS 是 OFF|  
|**sys.databases**|**bit**|1 = CURSOR_CLOSE_ON_COMMIT 是 ON<br /> 0 = CURSOR_CLOSE_ON_COMMIT 是 OFF|  
|**is_local_cursor_default**|**bit**|1 = CURSOR_DEFAULT 是區域<br /> 0 = CURSOR_DEFAULT 是全域|  
|**is_fulltext_enabled**|**bit**|1 = 資料庫啟用全文檢索<br /> 0 = 資料庫停用全文檢索|  
|**is_trustworthy_on**|**bit**|1 = 資料庫已被標示為可信任<br /> 0 = 資料庫尚未標示為可信任|  
|**is_db_chaining_on**|**bit**|1 = 跨資料庫擁有權鏈結是 ON<br /> 0 = 跨資料庫擁有權鏈結是 OFF|  
|**is_parameterization_forced**|**bit**|1 = 參數化是 FORCED<br /> 0 = 參數化是 SIMPLE|  
|**is_master_key_encrypted_by_server**|**bit**|1 = 資料庫具有已加密的主要金鑰<br /> 0 = 資料庫沒有已加密的主要金鑰|  
|**is_query_store_on**|**bit**|1 = 查詢存放區會啟用此資料庫。 請檢查[sys.database_query_store_options](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)檢視的查詢存放區狀態。<br /> 0 = 查詢存放區未啟用<br /> **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
|**is_published**|**bit**|1 = 資料庫是交易式或快照式複寫拓撲的發行集資料庫<br /> 0 = 不是發行集資料庫|  
|**is_subscribed**|**bit**|不使用這個資料行。 不論資料庫的訂閱者狀態為何，它一定會傳回 0。|  
|**is_merge_published**|**bit**|1 = 資料庫是合併式複寫拓撲的發行集資料庫<br /> 0 = 不是合併式複寫拓撲的發行集資料庫|  
|**is_distributor**|**bit**|1 = 資料庫是複寫拓撲的散發資料庫<br /> 0 = 不是複寫拓撲的散發資料庫|  
|**is_sync_with_backup**|**bit**|1 = 資料庫是標示為利用備份進行複寫同步處理<br /> 0 = 不是標示為利用備份進行複寫同步處理|  
|**service_broker_guid**|**uniqueidentifier**|這個資料庫的 Service Broker 識別碼。 做**broker_instance**的路由表中的目標。|  
|**is_broker_enabled**|**bit**|1 = 這個資料庫中的 Broker，目前正在收送訊息。<br /> 0 = 所有傳送的訊息，都會停留在傳輸佇列中，而收到的訊息並不會置於這個資料庫的佇列中。<br /> 依預設，還原或附加的資料庫都會停用 Broker。 但資料庫鏡像例外，它會在容錯移轉之後啟用 Broker。|  
|**log_reuse_wait**|**tinyint**|交易記錄空間的重複利用正等待進行最後一個檢查點的下列其中一個。 (如需詳細說明這些值，請參閱[交易記錄](../../relational-databases/logs/the-transaction-log-sql-server.md)。)<br /> 0 = 無<br />   1 = 檢查點 (當資料庫使用復原模式而且擁有記憶體最佳化的資料檔案群組時，您應該預期會看見 log_reuse_wait 資料行指出檢查點或 xtp_checkpoint)。**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  2 = 記錄備份**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  3 = 使用中的備份或還原**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  4 = 使用中交易**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  5 = 資料庫鏡像**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  6 = 複寫**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  7 = 建立資料庫快照集**適用於**[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  8 = 掃描記錄**適用於**<br />  9 = Alwayson 可用性群組次要複本會將此資料庫的交易記錄檔記錄套用到對應的次要資料庫。 **適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 在舊版的 SQL Server，9 = 其他 (暫時性)。<br />  10 = 僅供內部使用**適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  11 = 僅供內部使用**適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 12 = 僅供內部使用**適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />13 = 最舊的網頁**適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 14 = 其他**適用於**[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />  16 = XTP_CHECKPOINT (當資料庫使用復原模式而且擁有記憶體最佳化的資料檔案群組時，您應該預期會看見 log_reuse_wait 資料行指出檢查點或 xtp_checkpoint)。**適用於**[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**log_reuse_wait_desc**|**nvarchar(60)**|描述交易記錄空間的重複利用正等待最後一個檢查點。|  
|**is_date_correlation_on**|**bit**|1 = DATE_CORRELATION_OPTIMIZATION 是 ON<br /> 0 = DATE_CORRELATION_OPTIMIZATION 是 OFF|  
|**is_cdc_enabled**|**bit**|1 = 資料庫已啟用異動資料擷取。 如需詳細資訊，請參閱 < [sys.sp_cdc_enable_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)。|  
|**is_encrypted**|**bit**|指示是否加密資料庫 (反映上次使用 ALTER DATABASE SET ENCRYPTION 子句所設定的狀態)。 可為下列其中一個值：<br /> 1 = 已加密<br /> 0 = 未加密<br /> 如需資料庫加密的詳細資訊，請參閱[透明資料加密 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)。<br /> 如果資料庫正在進行解密， **is_encrypted**顯示值為 0。 您可以使用，以查看加密程序的狀態[sys.dm_database_encryption_keys](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)動態管理檢視。|  
|**is_honor_broker_priority_on**|**bit**|指示資料庫是否要接受交談優先權 (反映上次使用 ALTER DATABASE SET HONOR_BROKER_PRIORITY 子句所設定的狀態)。 可為下列其中一個值：<br /> 1 = HONOR_BROKER_PRIORITY 為 ON<br /> 0 = HONOR_BROKER_PRIORITY 為 OFF|  
|**replica_id**|**uniqueidentifier**|資料庫正在參與之可用性群組 (如果有) 的本機 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]可用性複本的唯一識別碼。<br /> NULL = 資料庫不是可用性群組中可用性複本的一部分。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**group_database_id**|**uniqueidentifier**|Always On 可用性群組內，如果任何資料庫正在參與之資料庫的唯一識別碼。 **group_database_id**是相同的主要複本上和所在資料庫已聯結至可用性群組的每個次要複本的這個資料庫。<br /> NULL = 資料庫不是任何可用性群組中可用性複本的一部分。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**resource_pool_id**|**int**|對應到這個資料庫之資源集區的識別碼。 這個資源集區會控制可供這個資料庫中記憶體最佳化資料表使用的記憶體總量。<br /> **適用於**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**default_language_lcid**|**smallint**|表示自主資料庫預設語言的地區設定識別碼 (LCID)。<br /> **附註**當做[設定 default language 伺服器組態選項](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)的**sp_configure**。 這個值是**null**非自主資料庫。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_language_name**|**nvarchar(128)**|表示自主資料庫的預設語言。<br /> 這個值是**null**非自主資料庫。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_lcid**|**int**|表示自主資料庫預設全文檢索語言的地區設定識別碼 (LCID)。<br /> **附註**做為預設值[設定預設全文檢索語言伺服器組態選項](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md)的**sp_configure**。 這個值是**null**非自主資料庫。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**default_fulltext_language_name**|**nvarchar(128)**|表示自主資料庫的預設全文檢索語言。<br /> 這個值是**null**非自主資料庫。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_nested_triggers_on**|**bit**|指出自主資料庫是否允許巢狀觸發程序。<br /> 0 = 不允許巢狀觸發程序。<br /> 1 = 允許巢狀觸發程序。<br /> **附註**當做[設定 nested 的 triggers 伺服器組態選項](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)的**sp_configure**。 這個值是**null**非自主資料庫。 請參閱[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)如需詳細資訊。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_transform_noise_words_on**|**bit**|指出自主資料庫中是否應該轉換非搜尋字。<br /> 0 = 不應該轉換非搜尋字。<br /> 1 = 應該轉換非搜尋字。<br /> **附註**當做[轉換非搜尋字伺服器組態選項](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)的**sp_configure**。 這個值是**null**非自主資料庫。 請參閱[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)如需詳細資訊。<br /> **適用於**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**two_digit_year_cutoff**|**smallint**|表示 1753 與 9999 之間的數值，代表將二位數年份解譯為四位數年份時的截斷年份 (Cutoff Year)。<br /> **附註**當做[設定 two digit year cutoff 伺服器組態選項](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)的**sp_configure**。 這個值是**null**非自主資料庫。 請參閱[sys.configurations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)如需詳細資訊。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**containment**|**非 null 的 tinyint**|指示資料庫的內含項目狀態。<br />  0 = 資料庫內含項目已關閉。 **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]<br /> 1 = 資料庫處於部分內含項目**適用於**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|**containment_desc**|**nvarchar(60) 不是 null**|指示資料庫的內含項目狀態。<br /> NONE = 舊版資料庫 (零個內含項目)<br /> PARTIAL = 部分自主資料庫<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**target_recovery_time_in_seconds**|**int**|復原資料庫的預估時間 (以秒為單位)。 可為 Null。<br /> **適用對象**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**delayed_durability**|**int**|延遲的持久性設定：<br /> 0 = 停用<br /> 1 = 允許<br /> 2 = 強制<br /> 如需詳細資訊，請參閱[控制交易持久性](../../relational-databases/logs/control-transaction-durability.md)。<br /> **適用於**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
|**delayed_durability_desc**|**nvarchar(60)**|延遲的持久性設定：<br /> DISABLED<br /> ALLOWED<br /> FORCED<br /> **適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /> **適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**is_memory_optimized_elevate_to_snapshot_on**|**bit**|當工作階段設定 TRANSACTION ISOLATION LEVEL 設定為較低的隔離等級 READ COMMITTED 或 READ UNCOMMITTED 時，會使用 SNAPSHOT 隔離存取記憶體最佳化的資料表。<br /> 1 = 最低隔離等級為 SNAPSHOT。<br /> 0 = 不提高隔離等級。|  
|**is_federation_member**|**bit**|表示資料庫是否為同盟的成員。<br /> **適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
|**is_remote_data_archive_enabled**|**bit**|指出是否要延展的資料庫。<br /> 0 = 資料庫不是已啟用延展功能。<br /> 1 = 資料庫是已啟用延展功能。<br /> **適用於**：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 如需詳細資訊，請參閱 < [Stretch Database](../../sql-server/stretch-database/stretch-database.md)。|  
|**is_mixed_page_allocation_on**|**bit**|指出是否在資料庫中資料表和索引可以初始頁面從配置混合範圍。<br /> 0 = 資料表，並在資料庫中的索引一律從一致範圍配置初始頁面。<br /> 1 = 資料表和資料庫中的索引可以從混合範圍配置初始頁面。<br /> **適用於**：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /> 如需詳細資訊，請參閱的 SET MIXED_PAGE_ALLOCATION 選項[ALTER DATABASE SET 選項&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。|  
|**is_temporal_retention_enabled**|**bit**|指出是否已啟用時態保留原則的清除工作。<br /> **適用於**: Azure SQL Database|
|**catalog_collation_type**|**int**|目錄定序設定：<br />0 = DATABASE_DEFAULT<br />2 = SQL_Latin_1_General_CP1_CI_AS<br /> **適用於**: Azure SQL Database|
|**catalog_collation_type_desc**|**nvarchar(60)**|目錄定序設定：<br />COLLATE<br />SQL_Latin_1_General_CP1_CI_AS<br /> **適用於**: Azure SQL Database|
  
## <a name="permissions"></a>Permissions  
 如果呼叫端`sys.databases`不是資料庫的擁有者，而且資料庫不是`master`或`tempdb`，請參閱對應的資料列所需的最低權限會`ALTER ANY DATABASE`或`VIEW ANY DATABASE`伺服器層級權限或`CREATE DATABASE`中的權限`master`資料庫。 呼叫端連接的資料庫可以永遠會被視為在`sys.databases`。  
  
> [!IMPORTANT]  
>  根據預設，公用角色具備`VIEW ANY DATABASE`權限，允許所有登入查看資料庫資訊。 若要封鎖登入，以偵測資料庫的能力`REVOKE``VIEW ANY DATABASE`權限`public`，或`DENY`' 個別登入的 VIEW ANY DATABASE 權限。  
  
## <a name="includesssdsincludessssds-mdmd-remarks"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)]備註  
 在  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，此檢視位於`master`資料庫和使用者資料庫中。 在 `master`資料庫，此檢視傳回的資訊`master`資料庫和伺服器上的所有使用者資料庫。 在使用者資料庫中，這個檢視只會傳回有關目前資料庫和 master 資料庫的資訊。  
  
 使用建立新資料庫所在的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 伺服器上 `master` 資料庫中的 `sys.databases` 檢視。 資料庫複製開始之後，您可以查詢`sys.databases`而`sys.dm_database_copies`檢視從`master`目的地伺服器，以擷取有關複製進度的詳細資訊的資料庫。  
  
## <a name="examples"></a>範例  
  
### <a name="a-query-the-sysdatabases-view"></a>A. 查詢 sys.databases 檢視  
 下列範例會傳回在可用的資料行數`sys.databases`檢視。  
  
```  
SELECT name, user_access_desc, is_read_only, state_desc, recovery_model_desc  
FROM sys.databases;  
```  
  
### <a name="b-check-the-copying-status-in-includesssdsincludessssds-mdmd"></a>B. 檢查 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中的複製狀態  
 下列範例會查詢`sys.databases`和`sys.dm_database_copies`檢視，以傳回資料庫的相關資訊複製作業。  
  
**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]|  
  
```  
-- Execute from the master database.  
SELECT a.name, a.state_desc, b.start_date, b.modify_date, b.percentage_complete  
FROM sys.databases AS a  
INNER JOIN sys.dm_database_copies AS b ON a.database_id = b.database_id  
WHERE a.state = 7;  
```  
### <a name="c-check-the-temporal-retention-policy-status-in-includesssdsincludessssds-mdmd"></a>C. 簽入時態保留原則狀態 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
 下列範例會查詢`sys.databases`傳回資訊是否已啟用時態保留清除工作。 請注意，還原作業後時態保留預設會停用。 使用`ALTER DATABASE`若要明確啟用它。
  
**適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
```  
-- Execute from the master database.  
SELECT a.name, a.is_temporal_history_retention_enabled 
FROM sys.databases AS a;
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_recovery_status &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-recovery-status-transact-sql.md)   
 [資料庫和檔案目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [sys.dm_database_copies &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)  
  
  
