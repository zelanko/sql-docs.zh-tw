---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: b217787d0cba0a1d62ab8393ef7fac76d7665bb0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "77568061"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>按一下產品！

在下列資料列中，按一下您感興趣的產品名稱。 視您所按下的產品而定，此點選會在本網頁的這裡顯示不同的內容。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL Database<br />受控執行個體](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server 和 SQL Database 受控執行個體

建立資源管理員工作負載群組，並將工作負載群組與資源管理員資源集區產生關聯。 並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中都可使用 Resource Governor。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>語法

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>引數

*group_name*</br>
這是工作負載群組的使用者定義名稱。 *group_name* 是英數字元，最多可有 128 個字元，而且在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體內必須是唯一的，並須符合[識別碼](../../relational-databases/databases/database-identifiers.md)的規則。

IMPORTANCE = { LOW | **MEDIUM** | HIGH }</br>
指定要求在工作負載群組中的相對重要性。 下列任一個為其重要性，其中 MEDIUM 為預設值：

- LOW
- MEDIUM (預設值)
- HIGH

> [!NOTE]
> 每個重要性設定在內部都會儲存為計算所使用的數字。

IMPORTANCE 的資源集區範圍為本機；相同資源集區內部不同重要性的工作負載群組會彼此影響，但不會影響另一個資源集區中的工作負載群組。

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*</br>
指定單一要求可由集區中獲取的記憶體最大數量。 *value* 是相對於 MAX_MEMORY_PERCENT 所指定的資源集區大小的百分比。

*value* 在 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 之前是整數，從 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 開始以及在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 受控執行個體中則為浮點數。 預設值為 25。 允許的 *value* 範圍為 1 至 100。

> [!IMPORTANT]  
> 指定的數量僅參考查詢執行授與記憶體。
>
> 將 *value* 設定為 0 會避免在使用者定義的工作負載群組中，執行具有 SORT 和 HASH JOIN 作業的查詢。
>
> 不建議您將 *value* 設定為大於 70，因為如果其他並行查詢正在執行，伺服器可能無法將足夠的記憶體擱置在一旁。 最後，這可能會導致查詢逾時錯誤 8645。
>
> 如果查詢記憶體需求超過這個參數所指定的限制，伺服器會執行以下作業：
>
> - 如果是使用者定義的工作負載群組，伺服器會嘗試減少查詢的平行處理原則程度，直到記憶體需求低於此限制，或是直到平行處理原則程度等於 1 為止。 如果查詢記憶體需求仍然大於此限制，將會發生錯誤 8657。
>
> - 如果是內部和預設的工作負載群組，伺服器會允許查詢取得所需的記憶體。
>
> 請注意，如果伺服器沒有足夠的實體記憶體，這兩種情況都會受限於逾時錯誤 8645。

REQUEST_MAX_CPU_TIME_SEC = *value*</br>
指定要求可以使用的最大 CPU 時間量 (以秒為單位)。 *value* 必須是 0 或正整數。 *value* 的預設設定為 0，這代表沒有限制。

> [!NOTE]
> 根據預設，Resource Governor 不會在超過最大時間時，阻止要求繼續執行。 不過，系統將會產生某個事件。 如需詳細資訊，請參閱[超過 CPU 閾值事件類別](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)。
> [!IMPORTANT]
> 從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 和 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 開始，並使用[追蹤旗標 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，Resource Governor 將在超過時間上限時中止要求。

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*</br>
指定查詢能夠等待記憶體授權 (工作緩衝區記憶體) 變成可用的最大時間 (以秒為單位)。 *value* 必須是 0 或正整數。 *value* 的預設設定 0 會根據查詢成本使用內部計算來判斷最大時間。

> [!NOTE]
> 到達記憶體授權的逾時值時，查詢不一定會失敗。 只有當有太多並行的查詢正在執行時，查詢才會失敗。 否則，查詢可能只會得到最小的記憶體授權，導致查詢效能降低。

MAX_DOP = *value*</br>
為平行查詢執行指定**平行處理原則的最大程度 (MAXDOP)** 。 *value* 必須是 0 或正整數。 *value* 允許範圍是從 0 至 64。 *value* 的預設設定 0 會使用全域設定。 MAX_DOP 會以下列方式處理：

> [!NOTE]
> 工作負載群組 MAX_DOP 會覆寫[平行處理原則的最大程度伺服器組態](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)與 **MAXDOP** [資料庫範圍組態](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。

> [!TIP]
> 若要在查詢層級完成此操作，請使用 **MAXDOP** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。 將平行處理原則的最大程度設定為查詢提示非常有效，只要它不預期工作負載群組 MAX_DOP。 如果 MAXDOP 查詢提示值超過使用 Resource Governor 所設定的值，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 就會使用 Resource Governor `MAX_DOP` 值。 MAXDOP [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)一律會覆寫[平行處理原則的最大程度伺服器組態](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。
>
> 若要在資料庫層級完成此操作，請使用 **MAXDOP** [資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。
>
> 若要在伺服器層級完成此操作，請使用**平行處理原則的最大程度 (MAXDOP)** [伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。

GROUP_MAX_REQUESTS = *value*</br>
指定在工作負載群組中可允許執行的最大同時要求數。 *value* 必須為 0 或正整數。 *value* 的預設值為 0，會允許無限制的要求。 達到最大並行要求時，該群組中的使用者可以登入，但是會處於等候狀態，直到並行要求低於指定的值為止。

USING { *pool_name* |  **"default"** }</br>
將工作負載群組與 *pool_name* 所識別之使用者定義資源集區產生關聯。 這樣會將工作負載群組實際放到資源集區中。 如果未提供 *pool_name* 或未使用 USING 引數，工作負載群組會放入預先定義的 Resource Governor 預設集區。

"default" 是保留字，而且當搭配 USING 使用時，必須加上引號 ("") 或方括號 ([])。

> [!NOTE]
> 預先定義的工作負載群組和資源集區都會使用小寫名稱，例如 "default"。 如果是使用區分大小寫之定序的伺服器，則應該將此列入考量。 具有不區分大小寫之定序 (如 SQL_Latin1_General_CP1_CI_AS) 的伺服器會將 "default" 和 "Default" 視為相同。

EXTERNAL external_pool_name | "default"</br>
**適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 起)。

工作負載群組可指定外部資源集區。 您可以定義工作負載群組，並與兩個集區產生關聯：

- 一個用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作負載和查詢的資源集區
- 一個用於外部處理的外部資源集區。 如需詳細資訊，請參閱 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="remarks"></a>備註

使用 `REQUEST_MEMORY_GRANT_PERCENT` 時，在建立索引時將可使用比一開始授與的記憶體更多的工作空間記憶體來改善效能。 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，資源管理員支援這種特殊的處理。 不過，初始授與和任何額外的記憶體授與都受到資源集區和工作負載群組設定的限制。

`MAX_DOP` 限制是以[工作](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)為基礎。 它不是根據[要求](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)或查詢限制。 這表示在平行查詢執行期間，單一要求可能會繁衍指派至[排程器](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)的多個工作。 如需詳細資訊，請參閱[執行緒與工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)。

當使用 `MAX_DOP` 且查詢在編譯時間被標示為序列，不管工作負載群組或伺服器組態設定為何，都無法在執行階段將該查詢變更回平行。 在設定 `MAX_DOP` 之後，只有在由於記憶體壓力的情況下才能將它降低。 在授與記憶體佇列中等候時，看不到工作負載群組的重新組態。

### <a name="index-creation-on-a-partitioned-table"></a>分割區資料表上的索引建立

非對齊式分割區資料表上之索引建立所耗用的記憶體，與相關的分割區數目成正比。 如果所需的總記憶體超出資源管理員工作負載群組設定所設的每個查詢限制 `REQUEST_MAX_MEMORY_GRANT_PERCENT`，這個索引建立動作就可能無法執行。 由於 *"default"* 工作負載群組允許查詢超過每個查詢限制，而且具有所需的記憶體下限，因此使用者或許能夠在 *"default"* 工作負載群組中執行相同的索引建立動作，但前提是 *"default"* 資源集區有設定足夠的總記憶體來執行這類查詢。

## <a name="permissions"></a>權限

需要 `CONTROL SERVER` 權限。

## <a name="example"></a>範例

建立名為 `newReports` 的工作負載群組，它會使用 Resource Governor 預設設定，而且位於 Resource Governor 預設集區中。 此範例會指定 `default` 集區，但這不是必要的。

```sql
CREATE WORKLOAD GROUP newReports
WITH
    (REQUEST_MAX_MEMORY_GRANT_PERCENT = 2.5
      , REQUEST_MAX_CPU_TIME_SEC = 100
      , MAX_DOP = 4)    
USING "default" ;
GO
```

## <a name="see-also"></a>另請參閱

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />受控執行個體](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* Azure Synapse<br />Analytics \*_** &nbsp;||||

&nbsp;

## <a name="azure-synapse-analytics-preview"></a>Azure Synapse Analytics (預覽)

建立工作負載群組。 工作負載群組是一組要求的容器，而且是在系統上設定工作負載管理的基礎。 工作負載群組提供保留資源以進行工作負載隔離、包含資源、定義每個要求的資源，以及遵守執行規則的能力。 一旦陳述式完成，設定就會生效。

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

```
CREATE WORKLOAD GROUP group_name
[ WITH
 (  [ MIN_PERCENTAGE_RESOURCE = value ]
  [ [ , ] CAP_PERCENTAGE_RESOURCE = value ]
  [ [ , ] REQUEST_MIN_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH } ]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )
  [ ; ]
]
```

*group_name*</br>
指定用來識別工作負載群組的名稱。 *group_name* 是一種 sysname。 它的長度最多可以是 128 個字元，且在執行個體內必須是唯一的。

*MIN_PERCENTAGE_RESOURCE* = 值</br>
針對該工作負載群組指定一個保證的最小資源配置，該資源不會與其他工作負載群組共用。 *value* 為從 0 到 100 的整數範圍。 所有工作負載群組之間的 min_percentage_resource 總和不能超過 100。 min_percentage_resource 的值不能大於 cap_percentage_resource。 每個服務等級允許最小的有效值。 如需詳細資訊，請參閱[有效值](#effective-values)。

*CAP_PERCENTAGE_RESOURCE* = 值</br>
指定工作負載群組中所有要求的資源使用率上限。 允許的整數值範圍為 1 到 100。 cap_percentage_resource 的值必須大於 min_percentage_resource。 如果 min_percentage_resource 在其他工作負載群組中設定為大於零，則可以減小 cap_percentage_resource 的有效值。

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = 值</br>
設定每個要求配置的最小資源量。 *value* 為必要的參數，其十進位範圍介於 0.75 到 100.00 之間。 request_min_resource_grant_percent 的值必須是 0.25 的倍數，必須是 min_percentage_resource 的因數，而且小於 cap_percentage_resource。 每個服務等級允許最小的有效值。 如需詳細資訊，請參閱[有效值](#effective-values)。

例如：

```sql
CREATE WORKLOAD GROUP wgSample 
WITH
  ( MIN_PERCENTAGE_RESOURCE = 26                -- integer value
    , REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
    , CAP_PERCENTAGE_RESOURCE = 100 )
```

請考慮用於資源類別的值，作為 request_min_resource_grant_percent 的指導方針。  下表包含 Gen2 的資源配置。

|資源類別|資源百分比|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = 值</br>         
設定每個要求配置的資源數量上限。 *value* 為選擇性參數，預設值等於 request_min_resource_grant_percent。 *value* 必須大於或等於 request_min_resource_grant_percent。 當 equest_max_resource_grant_percent 的值大於 request_min_resource_grant_percent 而且有可用的系統資源時，會將其他資源配置給要求。

*IMPORTANCE* = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>        
指定要求在工作負載群組中的相對重要性。 下列任一個為其重要性，其中 NORMAL 為預設值：

- LOW
- BELOW_NORMAL
- NORMAL (預設)
- ABOVE_NORMAL
- HIGH

在工作負載群組中設定的重要性，是工作負載群組中所有要求的預設重要性。 使用者也可以在分類器層級設定重要性，該重要性可以覆寫工作負載群組的重要性設定。 這樣可以區分工作負載群組內要求的重要性，以便更快速地存取非保留的資源。 當跨工作負載群組的 min_percentage_resource 總和小於 100 時，會根據重要性來指派非保留的資源。

*QUERY_EXECUTION_TIMEOUT_SEC* = 值</br>     
指定查詢在取消之前可以執行的最長時間 (以秒為單位)。 *value* 必須是 0 或正整數。 值的預設設定為 0，這代表查詢永不逾時。QUERY_EXECUTION_TIMEOUT_SEC 會在查詢處於執行中狀態時計算，而非在查詢排入佇列時。

## <a name="remarks"></a>備註

系統會針對回溯相容性自動建立對應至資源類別的工作負載群組。 這些系統定義的工作負載群組無法卸除。 可以建立額外 8 位使用者定義的工作負載群組。

如果工作負載群組是在 `min_percentage_resource` 大於零的情況下建立，則 `CREATE WORKLOAD GROUP` 陳述式將會排入佇列，直到有足夠的資源可建立工作負載群組為止。

## <a name="effective-values"></a>有效值

`min_percentage_resource`、`cap_percentage_resource`、`request_min_resource_grant_percent` 和 `request_max_resource_grant_percent` 參數具有在目前服務層級內容及其他工作負載群組組態中調整的有效值。

每個服務層級支援的並行與使用資源類定義每個查詢的資源授與時相同，因此，request_min_resource_grant_percent 的支援值取決於執行個體所設定的服務層級。 在最低服務層級 DW100c，每個要求需要最少 25% 的資源。 在 DW100c，已設定之工作負載群組的有效 request_min_resource_grant_percent 可以是 25% 以上。 請參閱下表，以取得如何衍生有效值的進一步詳細資料。

|服務等級|REQUEST_MIN_RESOURCE_GRANT_PERCENT 的最低有效值|並行查詢數目上限|
|---|---|---|
|DW100c|25%|4|
|DW200c|12.5%|8|
|DW300c|8%|12|
|DW400c|6.25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1.5%|64|
|DW5000c|1.5%|64|
|DW6000c|0.75%|128|
|DW7500c|0.75%|128|
|DW10000c|0.75%|128|
|DW15000c|0.75%|128|
|DW30000c|0.75%|128|
||||

同樣地，request_min_resource_grant_percent、min_percentage_resource 必須大於或等於有效的 request_min_resource_grant_percent。 `min_percentage_resource` 設定為小於有效 `min_percentage_resource` 的工作負載群組，其值在執行階段會調整為零。 發生這種情況時，針對 `min_percentage_resource` 設定的資源可在所有工作負載群組間共用。 例如，`min_percentage_resource` 為 10% 且在 DW1000c 上執行的工作負載群組 `wgAdHoc`，會有 10% 的有效 `min_percentage_resource` (3.25% 是 DW1000c 所支援的最小值)。 `wgAdhoc` 在 DW100c 上的有效 min_percentage_resource 為 0%。 針對 `wgAdhoc` 設定的 10% 會在所有工作負載群組之間共用。

`cap_percentage_resource` 也具有有效值。 如果工作負載群組 `wgAdhoc` 設定為 100% 的 `cap_percentage_resource`，而另一個工作負載群組 `wgDashboards` 是以 25% 的 `min_percentage_resource` 所建立，則 `wgAdhoc` 的有效 `cap_percentage_resource` 會變成 75%。

若要了解工作負載群組的執行階段值，最簡單的方式就是查詢系統檢視 [sys.databases dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)。

## <a name="permissions"></a>權限

需要 `CONTROL DATABASE` 權限

## <a name="see-also"></a>另請參閱

- [DROP WORKLOAD GROUP (Transact-SQL)](drop-workload-group-transact-sql.md)
- [sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md)
- [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md)
- 有關如何建立及使用[工作負載群組](https://docs.microsoft.com/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)的快速入門

::: moniker-end
