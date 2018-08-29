---
title: ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/142018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- ALTER_DATABASE_SCOPED_CONFIGURATION
- ALTER_DATABASE_SCOPED_CONFIGURATION_TSQL
- DATABASE_SCOPED_CONFIGURATION_TSQL
- SCOPED_CONFIGURATION_TSQL
- SCOPED_TSQL
- ALTER_DATABASE_SCOPED_TSQL
- DATABASE_SCOPED_TSQL
helpviewer_keywords:
- ALTER DATABASE SCOPED CONFIGURATION statement
- configuration [SQL Server], ALTER DATABASE SCOPED CONFIGURATION statement
ms.assetid: 63373c2f-9a0b-431b-b9d2-6fa35641571a
caps.latest.revision: 32
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1e4dab492102f4505c22dd5b415a590372855294
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406713"
---
# <a name="alter-database-scoped-configuration-transact-sql"></a>ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  此陳述式可啟用數個**個別資料庫**層級的資料庫組態設定。 在 [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 及從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中都有提供此陳述式。 這些設定包括：  
  
- 清除程序快取。  
- 針對主要資料庫將 MAXDOP 參數設定為任意值 (1、2、...，以最適用於該特定資料庫的值為準)，並且針對所使用的所有次要資料庫 (例如，用於報告查詢) 設定不同的值 (例如 0)。  
- 將與資料庫無關的查詢最佳化工具基數估計模型設定為相容性層級。  
- 在資料庫層級啟用或停用參數探測。
- 在資料庫層級啟用或停用查詢最佳化。
- 在資料庫層級啟用或停用識別快取。
- 允許或不允許在第一次編譯批次時，將已編譯的計劃虛設常式儲存在快取中。  
- 啟用或停用原生編譯 T-SQL 模組的執行統計資料收集。
- 為支援 ONLINE= syntax 的 DDL 陳述式啟用或停用預設為連線的選項。
- 為支援 RESUMABLE= syntax 的 DDL 陳述式啟用或停用預設可繼續的選項。 

 ![連結圖示](../../database-engine/configure-windows/media/topic-link.gif "連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ALTER DATABASE SCOPED CONFIGURATION  
{        
     {  [ FOR SECONDARY] SET <set_options>  }    
}  
| CLEAR PROCEDURE_CACHE  
| SET < set_options >
[;]    
  
< set_options > ::=    
{  
    MAXDOP = { <value> | PRIMARY}    
    | LEGACY_CARDINALITY_ESTIMATION = { ON | OFF | PRIMARY}    
    | PARAMETER_SNIFFING = { ON | OFF | PRIMARY}    
    | QUERY_OPTIMIZER_HOTFIXES = { ON | OFF | PRIMARY}
    | IDENTITY_CACHE = { ON | OFF }
    | OPTIMIZE_FOR_AD_HOC_WORKLOADS = { ON | OFF }
    | XTP_PROCEDURE_EXECUTION_STATISTICS = { ON | OFF } 
    | XTP_QUERY_EXECUTION_STATISTICS = { ON | OFF }    
    | ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED } 
    | ELEVATE_RESUMABLE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }  
}  
```  
  
## <a name="arguments"></a>引數  
 
FOR SECONDARY  
 
指定次要資料庫的設定 (所有次要資料庫都必須具有相同的值)。  
  
MAXDOP **=** {\<value> | PRIMARY }  
**\<value>**  
  
指定應該用於陳述式的預設 MAXDOP 設定。 0 是預設值，表示將改用伺服器組態。 資料庫範圍的 MAXDOP 會覆寫 (設定為 0 時除外) sp_configure 在伺服器層級設定的**平行處理原則的最大程度**。 查詢提示仍然可以覆寫 DB 範圍的 MAXDOP 來調整需要不同設定的特定查詢。 所有這些設定都會受到針對「工作負載群組」設定的 MAXDOP 限制。   

您可以使用 max degree of parallelism 選項來限制要用於平行計畫執行的處理器數目。 SQL Server 會針對查詢、索引資料定義語言 (DDL) 作業、平行插入、線上改變資料行、平行統計資料收集，以及靜態和索引鍵集驅動資料指標填入，考慮進行平行執行計劃。
 
若要在執行個體層級設定此選項，請參閱[設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 

> [!TIP] 
> 若要在查詢層級完成此操作，請新增 **MAXDOP** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。  
  
PRIMARY  
  
只能在資料庫位於主要端上時，針對次要端進行此設定，並且表示將採用針對主要端設定的組態。 如果主要端的組態發生變更，次要端上的值將會相應地變更，而無須明確地設定次要端值。 **PRIMARY** 是次要端的預設設定。  
  
LEGACY_CARDINALITY_ESTIMATION **=** { ON | **OFF** | PRIMARY }  

可讓您將查詢最佳化工具基數估計模型設定為 SQL Server 2012 和更舊版本，而不根據資料庫的相容性層級。 預設值為 **OFF**，這會根據資料庫的相容性層級來設定查詢最佳化工具基數估計模型。 將此值設定為 **ON** 相當於啟用[追蹤旗標 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 

> [!TIP] 
> 若要在查詢層級完成此操作，請新增 **QUERYTRACEON** [查詢提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 開始，若要在查詢層級完成此操作，請新增 **USE HINT** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)，而不要使用追蹤旗標。 
  
PRIMARY  
  
只有在資料庫位於主要端上時，此值才會在次要端上有效，並且指定所有次要端上的查詢最佳化工具基數估計模型設定將採用針對主要端設定的值。 如果主要端上查詢最佳化工具基數估計模型的組態發生變更，次要端上的值將會相應地變更。 **PRIMARY** 是次要端的預設設定。  
  
PARAMETER_SNIFFING **=** { **ON** | OFF | PRIMARY}  

啟用或停用[參數探查](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)。 預設值是 ON。 這與 [追蹤旗標 4136](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)相同。   

> [!TIP] 
> 若要在查詢層級完成此操作，請參閱 **OPTIMIZE FOR UNKNOWN** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 開始，若要在查詢層級完成此操作，也可以使用 **USE HINT** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。 
  
PRIMARY  
  
只有在資料庫位於主要端上時，此值才會在次要端上有效，並且指定所有次要端上此設定的值將採用針對主要端設定的值。 如果主要端上使用[參數探查](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)的組態發生變更，次要端上的值將會相應地變更，而無須明確地設定次要端值。 這是次要端的預設設定。  
  
QUERY_OPTIMIZER_HOTFIXES **=** { ON | **OFF** | PRIMARY }  

啟用或停用查詢最佳化 Hotfix，而不管資料庫的相容性層級為何。 預設值為 **OFF**，這會停用在針對特定版本導入最高可用相容性層級之後 (RTM 後) 發行的查詢最佳化 Hotfix。 將此值設定為 **ON** 相當於啟用[追蹤旗標 4199](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。   

> [!TIP] 
> 若要在查詢層級完成此操作，請新增 **QUERYTRACEON** [查詢提示](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 開始，若要在查詢層級完成此操作，請新增 USE HINT [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)，而不要使用追蹤旗標。  
  
PRIMARY  
  
只有在資料庫位於主要端上時，此值才會在次要端上有效，並且指定所有次要端上此設定的值將採用針對主要端設定的值。 如果主要端的組態發生變更，次要端上的值將會相應地變更，而無須明確地設定次要端值。 這是次要端的預設設定。  
  
CLEAR PROCEDURE_CACHE  

清除資料庫的程序 (計劃) 快取。 這可以在主要端上執行，也可以在次要端上執行。  

IDENTITY_CACHE **=** { **ON** | OFF }  

**適用於**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 

在資料庫層級啟用或停用識別快取。 預設值為 **ON**。 識別快取可用來改善含有識別資料行之資料表上的 INSERT 效能。 若要避免因伺服器意外重新啟動或容錯移轉至次要伺服器，而導致識別資料行值不連貫，請停用 IDENTITY_CACHE 選項。 此選項類似於現有的[追蹤旗標 272](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)差異在於此選項可以在資料庫層級設定，而不僅止於在伺服器層級設定。   

> [!NOTE] 
> 只能針對 PRIMARY 設定此選項。 如需詳細資訊，請參閱[識別資料行](create-table-transact-sql-identity-property.md)。  

OPTIMIZE_FOR_AD_HOC_WORKLOADS **=** { ON | **OFF** }  

**適用於**：[!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)] 

允許或不允許在第一次編譯批次時，將已編譯的計劃虛設常式儲存在快取中。 預設值為 OFF。 針對資料庫啟用 OPTIMIZE_FOR_AD_HOC_WORKLOADS 資料庫範圍組態之後，在第一次編譯批次時，就會將已編譯的計劃虛設常式儲存在快取中。 與完整的已編譯計劃大小相比，計劃虛設常式的記憶體耗用量較少。  如果再次編譯或執行某個批次，就會移除已編譯的計劃虛設常式，並以完整的已編譯計劃取代。

XTP_PROCEDURE_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 

在目前的資料庫上啟用或停用原生編譯 T-SQL 模組的模組層級執行統計資料收集。 預設值為 OFF。 執行統計資料會反映在 [sys.dm_exec_procedure_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)。

如果這個選項是 ON，或已透過 [sp_xtp_control_proc_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql.md) 啟用統計資料收集，則會收集原生編譯 T-SQL 模組的模組層級執行統計資料。

XTP_QUERY_EXECUTION_STATISTICS  **=** { ON | **OFF** }  

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]

在目前的資料庫上啟用或停用原生編譯 T-SQL 模組的陳述式層級執行統計資料收集。 預設值為 OFF。 執行統計資料會反映在 [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md) 和[查詢存放區](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)。

如果這個選項是 ON，或已透過 [sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md) 啟用統計資料收集，則會收集原生編譯 T-SQL 模組的陳述式層級執行統計資料。

如需原生編譯 T-SQL 模組效能監控的詳細資料，請參閱[監視原生編譯預存程序的效能](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)。

ELEVATE_ONLINE = { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (功能處於公開預覽階段)

可讓您選取選項，讓引擎自動將支援的作業提升至線上。 預設為 OFF，這表示除非在陳述式中指定，否則不會將作業提升至線上。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 會反映 ELEVATE_ONLINE 目前的值。 這些選項將僅適用於線上普遍支援的作業。  

FAIL_UNSUPPORTED

此值會將所有支援的 DLL 作業提升至 ONLINE。 不支援線上執行的作業將會失敗並擲回警告。

WHEN_SUPPORTED  

此值會提升支援 ONLINE 的作業。 不支援線上的作業將離線執行。

> [!NOTE]
> 您可以在指定 ONLINE 選項的情形下提交陳述式，進而覆寫預設設定。 
 
ELEVATE_RESUMABLE= { OFF | WHEN_SUPPORTED | FAIL_UNSUPPORTED }

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (功能處於公開預覽階段)

可讓您選取選項，讓引擎自動將支援的作業提升至可繼續。 預設為 OFF，這表示除非在陳述式中指定，否則不會將作業提升至可繼續。 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 會反映 ELEVATE_RESUMABLE 目前的值。 這些選項僅適用於可繼續普遍支援的作業。 

FAIL_UNSUPPORTED

此值會將所有支援的 DLL 作業提升至 RESUMABLE。 不支援可繼續執行的作業會失敗並擲回警告。

WHEN_SUPPORTED  

此值會提升支援 RESUMABLE 的作業。 不支援可繼續的作業會在非可繼續的情況下執行。  

> [!NOTE]
> 您可以在指定 RESUMABLE 選項的情形下提交陳述式，進而覆寫預設設定。 

##  <a name="Permissions"></a> 權限  
 需要資料庫上的 ALTER ANY DATABASE SCOPE CONFIGURATION   
。 可由在資料庫上具有 CONTROL 權限的使用者來授與此權限。  
  
## <a name="general-remarks"></a>一般備註  
 雖然您可以設定讓次要資料庫擁有與其主要資料庫不同的範圍組態設定，但所有次要資料庫都會使用相同的組態。 無法為個別次要資料庫設定不同的設定。  
  
 執行此陳述式會清除目前資料庫中的程序快取，這意謂著所有查詢都必須重新編譯。  
  
 針對有 3 部分名稱的查詢，會採用查詢的目前資料庫連線設定，而不會採用在目前資料庫內容中編譯之 SQL 模組 (例如程序、函式及觸發程序) 的設定，因此會使用其所在資料庫的選項。  
  
 ALTER_DATABASE_SCOPED_CONFIGURATION 事件會以 DDL 事件的形式新增，可用來引發 DDL 觸發程序。 這是 ALTER_DATABASE_EVENTS 觸發程序群組的子系。  
 
 資料庫範圍組態設定會伴隨著資料庫。 這意謂著還原或附加指定的資料庫時，現有的組態設定會持續存留。
  
## <a name="limitations-and-restrictions"></a>限制事項  
**MAXDOP**  
  
 細微的設定可以覆寫全域設定，而資源管理員則可以設定所有其他 MAXDOP 設定的限制。  以下是 MAXDOP 設定的邏輯：  
  
-   查詢提示會覆寫 sp_configure 和資料庫範圍設定。 如果已針對工作負載群組設定資源群組 MAXDOP：  
  
    -   如果將查詢提示設定為 0，資源管理員設定就會覆寫它。  
  
    -   如果查詢提示不是 0，就會以資源管理員設定作為其限制。  
  
-   除非有查詢提示，否則 DB 範圍設定 (值為 0 時除外) 會覆寫 sp_configure 設定，並以資源管理員設定作為其限制。  
  
-   資源管理員設定會覆寫 sp_configure 設定。  
  
**QUERY_OPTIMIZER_HOTFIXES**  
  
 使用 QUERYTRACEON 提示來啟用舊版查詢最佳化工具或查詢最佳化工具 Hotfix 時，在查詢提示與資料庫範圍組態設定之間會是 OR 條件，也就是說，如果啟用兩者其中之一，就會套用選項。  
  
**GeoDR**  
  
 可讀取的次要資料庫 (例如「Always On 可用性群組」和 GeoReplication) 會藉由檢查資料庫的狀態來使用次要值。 儘管重新編譯並不會發生在容錯移轉時，而且就技術而言，新的主要資料庫會有使用次要設定的查詢，但主要資料庫與次要資料庫之間的設定只有在工作負載不同時會有差異，因此快取的查詢會使用最佳設定，而新查詢則會挑選適合它們的新設定。  
  
**DacFx**  
  
 由於 ALTER DATABASE SCOPED CONFIGURATION 是 Azure SQL Database 及從 SQL Server 2016 開始之 SQL Server 的新功能且會影響資料庫結構描述，因此無法將資料庫結構的匯出項目 (不論是否含有資料) 匯入至舊版 SQL Server，例如 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]。 例如，從使用此新功能的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 或 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 資料庫匯出至 [DACPAC](../../relational-databases/data-tier-applications/data-tier-applications.md) 或 [BACPAC](../../relational-databases/data-tier-applications/data-tier-applications.md) 的匯出項目，將無法匯入至舊版伺服器。  

**ELEVATE_ONLINE** 

此選項僅適用於支援 WITH(ONLINE= syntax) 的 DDL 陳述式。 不會影響 XML 索引 

**ELEVATE_RESUMABLE**

此選項僅適用於支援 WITH(ONLINE= syntax) 的 DDL 陳述式。 不會影響 XML 索引 

  
## <a name="metadata"></a>中繼資料  

[sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) 系統檢視會提供有關資料庫內範圍組態的資訊。 資料庫範圍組態選項只會出現在 sys.database_scoped_configurations 中，因為它們會覆寫伺服器層級預設設定。 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 系統檢視只會顯示伺服器層級設定。  
  
## <a name="examples"></a>範例  
下列範例示範如何使用 ALTER DATABASE SCOPED CONFIGURATION  
  
### <a name="a-grant-permission"></a>A. 授與權限  

此範例會將執行 ALTER DATABASE SCOPED CONFIGURATION 所需的權限     
授與使用者 [Joe]。  
  
```sql  
GRANT ALTER ANY DATABASE SCOPED CONFIGURATION to [Joe] ;  
```  
  
### <a name="b-set-maxdop"></a>B. 設定 MAXDOP  

此範例會在異地複寫案例中，針對主要資料庫設定 MAXDOP = 1，並針對次要資料庫設定 MAXDOP = 4。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET MAXDOP = 1 ;  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=4 ;  
```  
  
此範例會在異地複寫案例中，將次要資料庫及其主要資料庫的 MAXDOP 設定為相同。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP=PRIMARY ;
```  
  
### <a name="c-set-legacycardinalityestimation"></a>C. 設定 LEGACY_CARDINALITY_ESTIMATION  

此範例會在異地複寫案例中，將次要資料庫的 LEGACY_CARDINALITY_ESTIMATION 設定為 ON。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=ON ;  
```  
  
此範例會在異地複寫案例中，將次要資料庫及其主要資料庫的 LEGACY_CARDINALITY_ESTIMATION 設定為相同。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET LEGACY_CARDINALITY_ESTIMATION=PRIMARY ;  
```  
  
### <a name="d-set-parametersniffing"></a>D. 設定 PARAMETER_SNIFFING  

此範例會在異地複寫案例中，將主要資料庫的 PARAMETER_SNIFFING 設定為 OFF。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION SET PARAMETER_SNIFFING =OFF ;  
```  
  
此範例會在異地複寫案例中，將主要資料庫的 PARAMETER_SNIFFING 設定為 OFF。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=OFF ;  
```  
  
此範例會在異地複寫案例中，將次要資料庫及主要資料庫的 PARAMETER_SNIFFING 設定為相同。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET PARAMETER_SNIFFING=PRIMARY ;  
```  
  
### <a name="e-set-queryoptimizerhotfixes"></a>E. 設定 QUERY_OPTIMIZER_HOTFIXES  

在異地複寫案例中，將主要資料庫的 QUERY_OPTIMIZER_HOTFIXES 設定為 ON。  

```sql  
ALTER DATABASE SCOPED CONFIGURATION SET QUERY_OPTIMIZER_HOTFIXES=ON ;  
```  
  
### <a name="f-clear-procedure-cache"></a>F. 清除程序快取  

此範例會清除程序快取 (可能僅適用於主要資料庫)。  
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE ;  
```  

### <a name="g-set-identitycache"></a>G. 設定 IDENTITY_CACHE

**適用於**：[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 和 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] (功能目前為公開預覽版) 

此範例會停用識別快取。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET IDENTITY_CACHE=OFF ; 
```

### <a name="h-set-optimizeforadhocworkloads"></a>H. 設定 OPTIMIZE_FOR_AD_HOC_WORKLOADS

**適用於**：[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 

此範例會允許在第一次編譯批次時，將已編譯的計劃虛設常式儲存在快取中。

```sql 
ALTER DATABASE SCOPED CONFIGURATION SET OPTIMIZE_FOR_AD_HOC_WORKLOADS = ON;
```

### <a name="i--set-elevateonline"></a>I.  設定 ELEVATE_ONLINE 

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (功能處於公開預覽階段)
 
此範例會將 ELEVATE_ONLINE 設定為 FAIL_UNSUPPORTED。  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_ONLINE=FAIL_UNSUPPORTED ;
```  

### <a name="j-set-elevateresumable"></a>J. 設定 ELEVATE_RESUMABLE 

**適用於**：[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] (功能處於公開預覽階段)

此範例會將 ELEVEATE_RESUMABLE 設定為 WHEN_SUPPORTED。  tsqlCopy 

```sql
ALTER DATABASE SCOPED CONFIGURATION SET ELEVATE_RESUMABLE=WHEN_SUPPORTED ;  
``` 

## <a name="additional-resources"></a>其他資源

### <a name="maxdop-resources"></a>MAXDOP 資源 
* [平行處理原則的程度](../../relational-databases/query-processing-architecture-guide.md#DOP)
* [SQL Server 的 "max degree of parallelism" 組態選項的建議和指導方針](https://support.microsoft.com/en-us/kb/2806535) 

### <a name="legacycardinalityestimation-resources"></a>LEGACY_CARDINALITY_ESTIMATION 資源    
* [基數估計 (SQL Server)](../../relational-databases/performance/cardinality-estimation-sql-server.md)
* [Optimizing Your Query Plans with the SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) (使用 SQL Server 2014 基數估算程式最佳化您的查詢計劃)

### <a name="parametersniffing-resources"></a>PARAMETER_SNIFFING 資源    
* [參數探測](../../relational-databases/query-processing-architecture-guide.md#ParamSniffing)
* [參數的運用](https://blogs.msdn.microsoft.com/queryoptteam/2006/03/31/i-smell-a-parameter/) \(英文\)

### <a name="queryoptimizerhotfixes-resources"></a>QUERY_OPTIMIZER_HOTFIXES 資源    
* [追蹤旗標](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
* [SQL Server 查詢最佳化工具 Hotfix 追蹤旗標 4199 服務模型](https://support.microsoft.com/en-us/kb/974006)

### <a name="elevateonline-resources"></a>ELEVATE_ONLINE 資源 

- [線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 

### <a name="elevateresumable-resources"></a>ELEVATE_RESUMABLE 資源 

- [線上索引作業的指導方針](../../relational-databases/indexes/guidelines-for-online-index-operations.md) 
 
## <a name="more-information"></a>詳細資訊  
 [sys.database_scoped_configurations](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)   
 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [資料庫和檔案目錄檢視](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [伺服器組態選項](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)  
 
