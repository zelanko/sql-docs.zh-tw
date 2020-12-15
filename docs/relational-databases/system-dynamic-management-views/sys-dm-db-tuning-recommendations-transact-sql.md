---
title: sys.dm_db_tuning_recommendations (Transact-sql) |Microsoft Docs
description: 瞭解如何在 SQL Server 和 Azure SQL Database 中找出潛在的效能問題和建議的修正
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cad75b88b14fd9bc64acbbd8b167619d3dbcc2e3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472879"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>\_ \_ (transact-sql) 的 sys.dm db 微調 \_ 建議
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  傳回有關微調建議的詳細資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，每個包含不屬於已連線租使用者之資料的資料列都會被篩選掉。

| **資料行名稱** | **Data type** | **說明** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | 建議的唯一名稱。 |
| **type** | **nvarchar(4000)** | 產生建議之自動調整選項的名稱，例如 `FORCE_LAST_GOOD_PLAN` |
| **原因** | **nvarchar(4000)** | 提供此建議的原因。 |
| **有效期限 \_ 自** | **datetime2** | 第一次產生此建議。 |
| **上次 \_ 重新整理** | **datetime2** | 上次產生此建議的時間。 |
| **state** | **nvarchar(4000)** | 描述建議狀態的 JSON 檔。 可用的欄位如下：<br />-   `currentValue` -建議的目前狀態。<br />-   `reason` -常數，描述建議處於目前狀態的原因。|
| **是 \_ 可執行檔 \_ 動作** | **bit** | 1 = 可以透過腳本對資料庫執行建議 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 。<br />0 = 無法針對資料庫執行建議 (例如：僅限資訊或已還原的建議)  |
| **為 \_ revertable \_ 動作** | **bit** | 1 = 建議可由 Database engine 自動監視及還原。<br />0 = 無法自動監視及還原建議。 大部分 &quot; 可執行 &quot; 的動作將會 &quot; revertable &quot; 。 |
| **執行 \_ 動作 \_ 開始 \_ 時間** | **datetime2** | 套用建議的日期。 |
| **執行 \_ 動作 \_ 持續時間** | **time** | 執行動作的持續時間。 |
| **執行 \_ 動作 \_ 起始 \_ 者** | **nvarchar(4000)** | `User` = 使用者在建議中手動強制執行計畫。 <br /> `System` = 系統自動套用建議。 |
| **執行 \_ 動作 \_ 起始 \_ 時間** | **datetime2** | 套用建議的日期。 |
| **還原 \_ 動作 \_ 開始 \_ 時間** | **datetime2** | 還原建議的日期。 |
| **還原 \_ 動作 \_ 持續時間** | **time** | 還原動作的持續時間。 |
| **還原 \_ 動作 \_ 起始 \_ 者** | **nvarchar(4000)** | `User` = 使用者手動 unforced 建議的方案。 <br /> `System` = 系統自動還原的建議。 |
| **還原 \_ 動作 \_ 起始 \_ 時間** | **datetime2** | 還原建議的日期。 |
| **得分** | **int** | 此建議對0-100 規模的估計值/影響 (更大的)  |
| **細節** | **nvarchar(max)** | JSON 檔，其中包含有關建議的更多詳細資料。 可用的欄位如下：<br /><br />`planForceDetails`<br />-    `queryId` - \_ 回歸查詢的查詢識別碼。<br />-    `regressedPlanId` -回歸方案的 plan_id。<br />-   `regressedPlanExecutionCount` -偵測到回歸之前，具有回歸計畫之查詢的執行次數。<br />-    `regressedPlanAbortedCount` -執行回歸計畫期間偵測到的錯誤數目。<br />-    `regressedPlanCpuTimeAverage` -偵測到回歸之前，回歸查詢所耗用的平均 CPU 時間 (以微秒) 。<br />-    `regressedPlanCpuTimeStddev` -偵測到回歸之前，回歸查詢所耗用的 CPU 時間標準差。<br />-    `recommendedPlanId` -應強制的方案 plan_id。<br />-   `recommendedPlanExecutionCount`-在偵測到回歸之前，應強制執行之計畫的查詢執行數目。<br />-    `recommendedPlanAbortedCount` -應強制執行計畫期間偵測到的錯誤數目。<br />-    `recommendedPlanCpuTimeAverage` -平均 CPU 時間 (以微秒) ，此查詢是以在偵測到回歸) 之前強制 (計算的計畫來執行。<br />-    `recommendedPlanCpuTimeStddev` 偵測到回歸之前，回歸查詢所耗用的 CPU 時間標準差。<br /><br />`implementationDetails`<br />-  `method` -應該用來修正回歸的方法。 值一律為 `TSql` 。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 應執行的腳本，以強制執行建議的計畫。 |
  
## <a name="remarks"></a>備註  
 `sys.dm_db_tuning_recommendations`當資料庫引擎識別潛在的查詢效能回歸時，所傳回的資訊就會更新，而且不會保存。 建議只會保留到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新開機為止。 如果資料庫管理員想要在伺服器回收之後保留，請定期製作微調建議的備份副本。 

 `currentValue` 資料行中的欄位 `state` 可能會有下列值：
 
 | 狀態 | 描述 |
 |--------|-------------|
 | `Active` | 建議為使用中且尚未套用。 使用者可以取得建議腳本，並以手動方式執行。 |
 | `Verifying` | 建議是由所套用 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ，而內部驗證程式會比較強制計畫與回歸計畫的效能。 |
 | `Success` | 已成功套用建議。 |
 | `Reverted` | 建議已還原，因為沒有顯著的效能提升。 |
 | `Expired` | 建議已過期，且無法再套用。 |

資料行中的 JSON 檔 `state` 包含描述為什麼目前狀態建議的原因。 [原因] 欄位中的值可能是： 

| 原因 | 描述 |
|--------|-------------|
| `SchemaChanged` | 建議已過期，因為參考資料表的架構已變更。 如果在新的架構上偵測到新的查詢計劃回歸，就會建立新的建議。 |
| `StatisticsChanged`| 由於參考資料表上的統計資料變更，建議已過期。 如果根據新的統計資料偵測到新的查詢計劃回歸，就會建立新的建議。 |
| `ForcingFailed` | 無法強制執行查詢的建議計畫。 `last_force_failure_reason`在[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md) view 中尋找，以找出失敗的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` 在驗證程式期間，使用者已停用此選項。 `FORCE_LAST_GOOD_PLAN`使用[ALTER DATABASE SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)語句啟用選項，或使用資料行中的腳本手動強制執行計畫 `[details]` 。 |
| `UnsupportedStatementType` | 無法在查詢上強制執行計畫。 不支援的查詢範例包括資料指標和 `INSERT BULK` 語句。 |
| `LastGoodPlanForced` | 已成功套用建議。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 識別出潛在的效能回歸，但 `FORCE_LAST_GOOD_PLAN` 未啟用此選項，請參閱 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 手動套用建議或啟用 `FORCE_LAST_GOOD_PLAN` 選項。 |
| `VerificationAborted`| 驗證程式因重新開機或查詢存放區清除而中止。 |
| `VerificationForcedQueryRecompile`| 因為沒有顯著的效能改進，所以會重新編譯查詢。 |
| `PlanForcedByUser`| 使用者使用 [sp_query_store_force_plan &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md) 程式手動強制執行計畫。 如果使用者明確決定強制執行某些計畫，資料庫引擎將不會套用建議。 |
| `PlanUnforcedByUser` | 使用者使用 [sp_query_store_unforce_plan &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md) 程式手動 unforced 計畫。 因為使用者已明確還原建議的計畫，所以資料庫引擎會繼續使用目前的計畫，並且在未來進行某些計畫回歸時產生新的建議。 |

 [詳細資料] 資料行中的統計資料不會顯示執行時間計畫統計資料 (例如，目前的 CPU 時間) 。 建議的詳細資料會在回歸偵測時取得，並說明為何 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 識別的效能回歸。 使用 `regressedPlanId` 和 `recommendedPlanId` 來查詢 [查詢存放區目錄檢視](../../relational-databases/performance/how-query-store-collects-data.md) ，以找出確切的執行時間計畫統計資料。

## <a name="examples-of-using-tuning-recommendations-information"></a>使用微調建議資訊的範例  

### <a name="example-1"></a>範例 1
下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼會取得產生的腳本，以針對任何指定的查詢強制執行良好的計畫：  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>範例 2
下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼會取得產生的腳本，該腳本會針對任何指定的查詢強制執行良好的計畫，以及估計增益的其他相關資訊：

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

### <a name="example-3"></a>範例 3
下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼會取得產生的腳本，該腳本會針對任何指定的查詢強制執行良好的計畫，以及包含查詢文字和儲存在查詢存放區中之查詢計劃的其他資訊：

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

如需可用來查詢建議視圖中的值之 JSON 函數的詳細資訊，請參閱中的 [Json 支援](../json/json-data-sql-server.md) [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 。
  
## <a name="permissions"></a>權限  

需要 `VIEW SERVER STATE` 中的許可權 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 。   
需要 `VIEW DATABASE STATE` 中資料庫的許可權 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 。   

## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支援](../json/json-data-sql-server.md)
