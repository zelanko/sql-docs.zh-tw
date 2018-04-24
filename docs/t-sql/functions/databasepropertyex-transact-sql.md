---
title: DATABASEPROPERTYEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASEPROPERTYEX
- DATABASEPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DATABASEPROPERTYEX function
- displaying database properties
- database properties [SQL Server]
ms.assetid: 8a9e0ffb-28b5-4640-95b2-a54e3e5ad941
caps.latest.revision: 84
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4331e2c3e4b68a3c439ed72a16f0941068b76802
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="databasepropertyex-transact-sql"></a>DATABASEPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中指定資料庫之指定資料庫選項或屬性的目前設定。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATABASEPROPERTYEX ( database , property )  
```  
  
## <a name="arguments"></a>引數  
*database*  
這是代表傳回的具名屬性資訊所針對之資料庫名稱的運算式。 *database* 為 **nvarchar(128)**。  
針對 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，必須是目前資料庫的名稱。 如果提供了不同的資料庫名稱，則對所有屬性傳回 NULL。
  
*property*  
這是代表要傳回之資料庫屬性的運算式。 *property* 為 **varchar(128)**，而且可以是下列值之一。 傳回型別為 **sql_variant**。 下表顯示了每一屬性值的基底資料型別。
  
> [!NOTE]  
>  如果沒有啟動資料庫，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 透過直接存取資料庫 (而非從中繼資料中擷取值) 所擷取的屬性會傳回 NULL。 也就是說，如果資料庫的 AUTO_CLOSE 設成 ON，否則資料庫會離線。  
  
|屬性|描述|傳回的值|  
|---|---|---|
|定序|資料庫的預設定序名稱。|定序名稱<br /><br /> NULL = 資料庫未啟動。<br /><br /> 基底資料型別：**nvarchar(128)**|  
|ComparisonStyle|Windows 的定序比較樣式。 ComparisonStyle 是使用下列可能樣式的值所計算的點陣圖。<br /><br /> 忽略大小寫：1<br /><br /> 忽略腔調字：2<br /><br /> 忽略假名：65536<br /><br /> 忽略寬度：131072<br /><br /> <br /><br /> 例如，預設值 196609 是結合「忽略大小寫」、「忽略假名」和「忽略寬度」等選項的結果。|傳回比較樣式。<br /><br /> 所有的二進位定序皆傳回 0。<br /><br /> 基底資料類型：**int**|  
|版本|資料庫版本或服務層。|**適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。<br /><br /> <br /><br /> 一般用途<br /><br /> 業務關鍵<br /><br /> [基本]<br /><br /> Standard<br /><br /> Premium<br /><br /> 系統 (適用於 master 資料庫)<br /><br /> NULL = 資料庫未啟動。<br /><br /> 基底資料型別：**nvarchar**(64)|  
|IsAnsiNullDefault|資料庫遵照允許 Null 值的 ISO 規則。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAnsiNullsEnabled|所有對於 Null 的比較，都會得出「未知」。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAnsiPaddingEnabled|字串在進行比較或插入處理之前，先填補至相同的長度。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAnsiWarningsEnabled|當發生標準錯誤狀況時，會發出錯誤或警告訊息。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsArithmeticAbortEnabled|在查詢執行期間，當發生溢位或除以零的錯誤時，會停止查詢。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAutoClose|在最後一個使用者結束之後，資料庫完整關機並釋出資源。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAutoCreateStatistics|查詢最佳化工具會視需要建立單一資料行統計資料來改善查詢效能。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAutoCreateStatisticsIncremental|自動建立的單一資料行統計資料會累加 (如果可能)。|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAutoShrink|資料庫檔案是自動定期壓縮的候選項。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsAutoUpdateStatistics|當查詢使用現有的統計資料而且這些統計資料可能已過期時，查詢最佳化工具就會更新這些統計資料。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|
|IsClone|資料庫僅為使用者資料庫的結構描述及統計資料複本。|**適用對象**：[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**| 
|IsCloseCursorsOnCommitEnabled|關閉認可交易時在開啟狀態的資料指標。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsFulltextEnabled|資料庫已啟用全文檢索和語意索引。|**適用於**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**<br /><br /> **注意：**此屬性的值沒有任何作用。 使用者資料庫一定會啟用全文檢索搜尋。 未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本將移除這個資料行。 請勿在新的開發工作中使用此資料行，並且儘速修改目前使用任何一個資料行的應用程式。|  
|IsInStandBy|資料庫在線上唯讀，允許還原記錄。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsLocalCursorsDefault|資料指標宣告預設為 LOCAL。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsMemoryOptimizedElevateToSnapshotEnabled|當工作階段設定 TRANSACTION ISOLATION LEVEL 設定為較低的隔離等級 READ COMMITTED 或 READ UNCOMMITTED 時，會使用 SNAPSHOT 隔離存取記憶體最佳化的資料表。|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> 基底資料類型：**int**|  
|IsMergePublished|可以為合併式複寫發行的資料庫資料表 (若已安裝複寫功能)。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsNullConcat|Null 串連運算元產生 NULL。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsNumericRoundAbortEnabled|當運算式發生遺失有效位數的情形時，則產生錯誤。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsParameterizationForced|PARAMETERIZATION 資料庫 SET 選項是 FORCED。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效|  
|IsQuotedIdentifiersEnabled|識別碼可以使用雙引號。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsPublished|可以為快照集或異動複寫發行的資料庫資料表 (若已安裝複寫功能)。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsRecursiveTriggersEnabled|啟用觸發程序的遞迴引發。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsSubscribed|將資料庫訂閱到發行集中。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsSyncWithBackup|該資料庫是已發行的資料庫或散發資料庫，並且能在不干擾異動複寫的情況下被還原。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsTornPageDetectionEnabled|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 偵測到因為斷電或其他系統失效所造成的不完全 I/O 作業。|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效<br /><br /> 基底資料類型：**int**|  
|IsXTPSupported|指出資料庫是否支援記憶體內部 OLTP，即建立及使用記憶體最佳化資料表和原生編譯模組。<br /><br /> 特定於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]：<br /><br /> IsXTPSupported 是獨立於任何建立記憶體內部 OLTP 物件所必須之 MEMORY_OPTIMIZED_DATA 檔案群組的存在之外。|**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])、[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。<br /><br /> **適用對象**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始)。<br /><br /> <br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = 輸入無效、發生錯誤或不適用<br /><br /> 基底資料類型：**int**|  
|LCID|Windows 的定序地區設定識別碼 (LCID)。|LCID 值 (十進位格式)。<br /><br /> 基底資料類型：**int**|  
|MaxSizeInBytes|資料庫的大小上限 (以位元組為單位)。|**適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]、[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。<br /><br /> <br /><br /> 1073741824<br /><br /> 5368709120<br /><br /> 10737418240<br /><br /> 21474836480<br /><br /> 32212254720<br /><br /> 42949672960<br /><br /> 53687091200<br /><br /> NULL = 資料庫未啟動<br /><br /> 基底資料型別：**bigint**|  
|復原|資料庫的復原模式。|FULL = 完全復原模式<br /><br /> BULK_LOGGED = 大量記錄模式<br /><br /> SIMPLE = 簡單復原模式<br /><br /> 基底資料型別：**nvarchar(128)**|  
|ServiceObjective|描述 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 或 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 中資料庫的效能層級。|可以是下列其中一項：<br /><br /> Null：資料庫尚未啟動<br /><br /> 共用 (適用於 Web/Business 版本)<br /><br /> [基本]<br /><br /> S0<br /><br /> S1<br /><br /> S2<br /><br /> S3<br /><br /> P1<br /><br /> P2<br /><br /> P3<br /><br /> ElasticPool<br /><br /> 系統 (適用於 master 資料庫)<br /><br /> 基底資料型別：**nvarchar(32)**|  
|ServiceObjectiveId|[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 中服務目標的識別碼。|識別服務目標的 **uniqueidentifier**。|  
|SQLSortOrder|舊版 SQL Server 中所支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序順序識別碼。|0 = 資料庫使用 Windows 定序<br /><br /> >0 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序順序識別碼<br /><br /> NULL = 輸入無效或未啟動資料庫。<br /><br /> 基底資料型別：**tinyint**|  
|[狀態]|資料庫狀態。|ONLINE = 資料庫可用於查詢。<br /><br /> **注意：**當資料庫開啟中且尚未復原時，可能會傳回 ONLINE 狀態。 若要識別資料庫可接受連線的時間，請查詢 **DATABASEPROPERTYEX** 的 Collation 屬性。 當資料庫定序傳回非 Null 值時，表示資料庫可接受連接。 對於 AlwaysOn 資料庫，可查詢 sys.dm_hadr_database_replica_states 的 database_state 或 database_state_desc 資料行。<br /><br /> OFFLINE = 資料庫明確離線。<br /><br /> RESTORING = 正在還原資料庫。<br /><br /> RECOVERING = 資料庫復原中，無法進行查詢。<br /><br /> SUSPECT = 資料庫未復原。<br /><br /> EMERGENCY = 資料庫處於緊急、唯讀的狀態。 存取限於系統管理員 (sysadmin) 成員<br /><br /> 基底資料型別：**nvarchar(128)**|  
|Updateability|指出資料是否可以修改。|READ_ONLY = 資料可以讀取，但無法修改。<br /><br /> READ_WRITE = 資料可以讀取及修改。<br /><br /> 基底資料型別：**nvarchar(128)**|  
|UserAccess|指定那些使用者可以存取資料庫。|SINGLE_USER = 一次只有一個 db_owner、資料庫建立者 (dbcreator) 或系統管理員 (sysadmin) 使用者<br /><br /> RESTRICTED_USER = 只有 db_owner、資料庫建立者 (dbcreator) 和系統管理員 (sysadmin) 角色<br /><br /> MULTI_USER = 所有使用者<br /><br /> 基底資料型別：**nvarchar(128)**|  
|Version|建立資料庫所用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式碼的內部版本號碼。 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|版本號碼 = 資料庫是開啟的。<br /><br /> NULL = 資料庫未啟動。<br /><br /> 基底資料類型：**int**|  
  
## <a name="return-types"></a>傳回類型
**sql_variant**
  
## <a name="exceptions"></a>例外狀況  
當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，OBJECT_ID) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>Remarks  
DATABASEPROPERTYEX 一次只傳回一個屬性設定。 若要顯示多個屬性設定，請使用 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 目錄檢視。
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-the-status-of-the-autoshrink-database-option"></a>A. 擷取 AUTO_SHRINK 資料庫選項的狀態  
下列範例會傳回 `AdventureWorks` 資料庫 AUTO_SHRINK 資料庫選項的狀態。
  
```sql
SELECT DATABASEPROPERTYEX('AdventureWorks2014', 'IsAutoShrink');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)] 這表示 AUTO_SHRINK 是關閉狀態。
  
```sql
------------------  
0  
```  
  
### <a name="b-retrieving-the-default-collation-for-a-database"></a>B. 擷取資料庫的預設定序  
下列範例會傳回 `AdventureWorks` 資料庫的多個屬性。
  
```sql
SELECT   
    DATABASEPROPERTYEX('AdventureWorks2014', 'Collation') AS Collation,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'Edition') AS Edition,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'ServiceObjective') AS ServiceObjective,  
    DATABASEPROPERTYEX('AdventureWorks2014', 'MaxSizeInBytes') AS MaxSizeInBytes  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Collation                     Edition        ServiceObjective  MaxSizeInBytes  
----------------------------  -------------  ----------------  --------------  
SQL_Latin1_General_CP1_CI_AS  DataWarehouse  DW1000            5368709120  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[資料庫狀態](../../relational-databases/databases/database-states.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)  
[SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)
  
  
