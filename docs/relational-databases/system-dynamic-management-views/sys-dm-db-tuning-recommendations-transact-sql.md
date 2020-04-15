---
title: 系統dm_db_tuning_recommendations(轉算-SQL) |微軟文件
description: 瞭解如何在 SQL Server 和 Azure SQL 資料庫中尋找潛在的效能問題和建議修復程式
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
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285468"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_db\_調優建議(轉算 SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  返回有關調優建議的詳細資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為避免公開此資訊,將篩選出包含不屬於連接租戶的數據的每一行。

| **資料行名稱** | **資料類型** | **說明** |
| --- | --- | --- |
| **名稱** | **nvarchar(4000)** | 推薦的唯一名稱。 |
| **型別** | **nvarchar(4000)** | 生成建議的自動調優選項的名稱,例如,`FORCE_LAST_GOOD_PLAN` |
| **原因** | **nvarchar(4000)** | 提供這項建議的原因。 |
| **有效\_,因為** | **datetime2** | 首次生成此建議。 |
| **上次\_刷新** | **datetime2** | 上次生成此建議時。 |
| **state** | **nvarchar(4000)** | 描述建議的狀態的 JSON 文檔。 以下欄位可用:<br />-   `currentValue`- 建議的當前狀態。<br />-   `reason`- 描述建議處於當前狀態的原因的常量。|
| **可\_\_執行作業** | **bit** | 1 =[!INCLUDE[tsql_md](../../includes/tsql-md.md)]建議可以通過 腳本針對資料庫執行。<br />0 = 無法針對資料庫執行建議(例如:僅資訊或還原建議) |
| **可\_回復\_操作** | **bit** | 1 = 建議可以自動監視並由資料庫引擎還原。<br />0 = 無法自動監視和還原建議。 大多數&quot;可&quot;執行操作將&quot;&quot;可 還原。 |
| **執行\_動作\_開始\_時間** | **datetime2** | 應用建議的日期。 |
| **執行\_操作\_持續時間** | **time** | 執行操作的持續時間。 |
| **\_\_執行\_由** | **nvarchar(4000)** | `User`• 建議中的用戶手動強制計劃。 <br /> `System`* 系統自動應用建議。 |
| **執行\_操作\_啟動\_時間** | **datetime2** | 應用建議的日期。 |
| **回復\_動作\_開始\_時間** | **datetime2** | 恢復建議的日期。 |
| **回復\_操作\_持續時間** | **time** | 還原操作的持續時間。 |
| **\_還原\_\_由** | **nvarchar(4000)** | `User`• 用戶手動非強制推薦計劃。 <br /> `System`• 系統會自動還原建議。 |
| **回復\_操作\_啟動\_時間** | **datetime2** | 恢復建議的日期。 |
| **得分** | **int** | 此建議在 0-100 比額表上的估計值/影響(越大越好) |
| **詳細資料** | **恩瓦爾恰爾(最大)** | 包含有關建議的更多詳細資訊的 JSON 文檔。 以下欄位可用:<br /><br />`planForceDetails`<br />-    `queryId`-\_回歸查詢的查詢 ID。<br />-    `regressedPlanId`- plan_id倒退計劃。<br />-   `regressedPlanExecutionCount`- 在檢測到回歸之前,使用回歸計劃執行查詢的次數。<br />-    `regressedPlanAbortedCount`- 執行回歸計劃期間檢測到的錯誤數。<br />-    `regressedPlanCpuTimeAverage`- 在檢測到回歸之前,回歸查詢消耗的平均 CPU 時間(以微秒為單位)。<br />-    `regressedPlanCpuTimeStddev`- 在檢測到回歸之前,回歸查詢消耗的 CPU 時間的標準偏差。<br />-    `recommendedPlanId`- plan_id應該強制的計劃。<br />-   `recommendedPlanExecutionCount`- 查詢的執行次數,在檢測到回歸之前應強制執行計劃。<br />-    `recommendedPlanAbortedCount`- 執行應強制執行計畫期間檢測到的錯誤數。<br />-    `recommendedPlanCpuTimeAverage`- 使用應強制執行的計劃執行的查詢消耗的平均 CPU 時間(以微秒為單位)(在檢測到回歸之前計算)。<br />-    `recommendedPlanCpuTimeStddev`在檢測到回歸之前,回歸查詢消耗的 CPU 時間的標準偏差。<br /><br />`implementationDetails`<br />-  `method`- 應用於更正回歸的方法。 價值總是`TSql`。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]應執行以強制建議計劃的腳本。 |
  
## <a name="remarks"></a>備註  
 返回的`sys.dm_db_tuning_recommendations`資訊 將在資料庫引擎標識潛在的查詢性能回歸時更新,並且不會持久化。 建議僅保留到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新啟動為止。 如果資料庫管理員希望在伺服器回收后保留調優建議,則應定期製作該建議的備份副本。 

 `currentValue`欄位`state`可能具有以下值:
 
 | 狀態 | 描述 |
 |--------|-------------|
 | `Active` | 建議處於活動狀態,尚未應用。 用戶可以採用推薦腳本並手動執行它。 |
 | `Verifying` | 建議由應用[!INCLUDE[ssde_md](../../includes/ssde_md.md)],內部驗證過程將強制計劃的性能與遞減計劃進行比較。 |
 | `Success` | 已成功應用建議。 |
 | `Reverted` | 建議被還原,因為沒有顯著的性能提升。 |
 | `Expired` | 建議已過期,無法再應用。 |

列中的`state`JSON 文檔包含描述建議處於當前狀態的原因。 原因欄位中的值可能是: 

| 原因 | 描述 |
|--------|-------------|
| `SchemaChanged` | 建議已過期,因為引用表的架構已更改。 如果在新架構上檢測到新的查詢計劃回歸,將創建新建議。 |
| `StatisticsChanged`| 由於引用的表上的統計資訊更改,建議已過期。 如果根據新統計資訊檢測到新的查詢計劃回歸,將創建新建議。 |
| `ForcingFailed` | 不能強制查詢上建議的計劃。 `last_force_failure_reason`在[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)檢視中查找失敗的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`在驗證過程中,使用者禁用了選項。 使用`FORCE_LAST_GOOD_PLAN` [ALTER 資料庫集AUTOMATIC_TUNING&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)語句啟用選項`[details]`,或強制使用列 中的腳本手動操作計劃。 |
| `UnsupportedStatementType` | 無法強制在查詢上進行計劃。 不支援的查詢的範例包括游標和`INSERT BULK`語句。 |
| `LastGoodPlanForced` | 已成功應用建議。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]已辨識潛在的效能回歸,但`FORCE_LAST_GOOD_PLAN`未啟用這個選項 - 請參閱[ALTER 資料庫集AUTOMATIC_TUNING&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 手動應用建議或啟用`FORCE_LAST_GOOD_PLAN`選項。 |
| `VerificationAborted`| 由於重新啟動或查詢存儲清理,驗證過程將中止。 |
| `VerificationForcedQueryRecompile`| 重新編譯查詢,因為性能沒有顯著改善。 |
| `PlanForcedByUser`| 使用者使用[sp_query_store_force_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)過程手動強制計劃。 如果使用者明確決定強制某些計劃,資料庫引擎將不會應用該建議。 |
| `PlanUnforcedByUser` | 使用者使用[sp_query_store_unforce_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)過程手動取消強制計劃。 由於使用者顯式還原了建議的計劃,因此資料庫引擎將繼續使用當前計劃,並在將來發生某些計劃回歸時生成新的建議。 |

 詳細資訊列中的統計資訊不顯示運行時計劃統計資訊(例如,當前 CPU 時間)。 建議詳細資訊在回歸檢測時獲取,並說明識別的效能回歸原因[!INCLUDE[ssde_md](../../includes/ssde_md.md)]。 使用`regressedPlanId``recommendedPlanId`和查詢[存儲目錄檢視](../../relational-databases/performance/how-query-store-collects-data.md)以查找準確的運行時計劃統計資訊。

## <a name="examples-of-using-tuning-recommendations-information"></a>使用調優建議資訊的範例  

### <a name="example-1"></a>範例 1
下面獲取生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]腳本,該腳本強制為任何給定查詢制定良好的計劃:  
 
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
下面獲取生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]腳本,該腳本強制為任何給定查詢制定好計劃,並獲取有關估計收益的其他資訊:

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
下面取得生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]文稿,該文本強制為任何給定查詢制定好計劃,並取得包含查詢文本和儲存在查詢儲存中的查詢計劃的其他資訊:

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

有關可用於查詢建議檢視中的值的 JSON 函數的詳細資訊,請參閱[!INCLUDE[ssde_md](../../includes/ssde_md.md)]中的[JSON 支援](../../relational-databases/json/index.md)。
  
## <a name="permissions"></a>權限  

需要`VIEW SERVER STATE`中的[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]許可權。   
需要`VIEW DATABASE STATE`中的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料庫的許可權。   

## <a name="see-also"></a>另請參閱  
 [自動調諧](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [系統database_automatic_tuning_options&#40;轉算-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [系統database_query_store_options&#40;轉瞬即發-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支援](../../relational-databases/json/index.md)
 
