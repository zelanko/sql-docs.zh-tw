---
title: sys.dm_db_tuning_recommendations (TRANSACT-SQL) |Microsoft Docs
description: 了解如何尋找潛在的效能問題和建議的 SQL Server 和 Azure SQL Database 中的修復
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0faae3cec2d71c28056a384b196a9b46929d5d6e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792106"
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_微調\_建議 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  傳回有關微調建議的詳細的資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。

| **資料行名稱** | **Data type** | **說明** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | 建議的唯一名稱。 |
| **type** | **nvarchar(4000)** | 產生的建議，例如自動微調選項的名稱 `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 為什麼提供這項建議的原因。 |
| **valid\_since** | **datetime2** | 第一次產生這項建議。 |
| **最後一個\_重新整理** | **datetime2** | 最後一次產生這項建議。 |
| **state** | **nvarchar(4000)** | 說明建議狀態的 JSON 文件。 可用的欄位如下：<br />-   `currentValue` -建議的目前狀態。<br />-   `reason` – 說明為何建議處於目前狀態的常數。|
| **is\_executable\_action** | **bit** | 1 = 可以針對透過資料庫執行建議[!INCLUDE[tsql_md](../../includes/tsql-md.md)]指令碼。<br />0 = 無法針對資料庫執行建議 (例如： 資訊只有或已還原建議) |
| **已\_revertable\_動作** | **bit** | 1 = 建議可以自動監控和還原資料庫引擎。<br />0 = 建議無法自動監控和還原。 大部分&quot;可執行檔&quot;動作將會是&quot;revertable&quot;。 |
| **execute\_action\_start\_time** | **datetime2** | 套用建議的日期。 |
| **execute\_action\_duration** | **time** | 執行動作的持續時間。 |
| **執行\_動作\_起始\_由** | **nvarchar(4000)** | `User` = 以手動方式強制在建議中的計劃使用者。 <br /> `System` = 系統會自動套用建議。 |
| **執行\_動作\_起始\_時間** | **datetime2** | 已套用建議的日期。 |
| **revert\_action\_start\_time** | **datetime2** | 已還原建議的日期。 |
| **revert\_action\_duration** | **time** | 還原動作的持續時間。 |
| **還原\_動作\_起始\_由** | **nvarchar(4000)** | `User` = 使用者手動強制執行的建議計劃。 <br /> `System` = 系統會自動還原建議。 |
| **還原\_動作\_起始\_時間** | **datetime2** | 已還原建議的日期。 |
| **score** | **int** | 估計值/影響此項建議在 0 到 100 的小數位數 （愈高愈好） |
| **詳細資料** | **nvarchar(max)** | 包含有關建議的更多詳細資料的 JSON 文件。 可用的欄位如下：<br /><br />`planForceDetails`<br />-    `queryId` -查詢\_迴歸查詢的識別碼。<br />-    `regressedPlanId` -plan_id 的迴歸的計畫。<br />-   `regressedPlanExecutionCount` -偵測到之查詢的迴歸的計畫迴歸之前的執行次數。<br />-    `regressedPlanAbortedCount` -迴歸的計畫執行期間偵測到的錯誤數目。<br />-    `regressedPlanCpuTimeAverage` -平均之前偵測到的迴歸，迴歸的查詢所耗用的 CPU 時間。<br />-    `regressedPlanCpuTimeStddev` -偵測到的迴歸之前迴歸的查詢所耗用的 CPU 時間標準差。<br />-    `recommendedPlanId` -應該強制計劃的 plan_id。<br />-   `recommendedPlanExecutionCount`-執行之前偵測到的迴歸應該強制的計劃的查詢數目。<br />-    `recommendedPlanAbortedCount` -應該強制計畫執行期間偵測到的錯誤數目。<br />-    `recommendedPlanCpuTimeAverage` -平均應該強制 （計算迴歸偵測到之前） 的計劃以執行查詢所耗用的 CPU 時間。<br />-    `recommendedPlanCpuTimeStddev` 偵測到的迴歸之前迴歸的查詢所耗用的 CPU 時間的標準差。<br /><br />`implementationDetails`<br />-  `method` -應該用來更正迴歸的方法。 值一律是`TSql`。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 應該強制執行建議的計劃執行的指令碼。 |
  
## <a name="remarks"></a>備註  
 所傳回的資訊`sys.dm_db_tuning_recommendations`資料庫引擎識別潛在的查詢效能變差，而不會保存。 建議會保留只[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新啟動。 如果他們想要保留在伺服器回收之後，資料庫管理員應該定期製作備份複本的微調建議。 

 `currentValue` 欄位`state`資料行可能會有下列值：
 | [狀態] | 描述 |
 |--------|-------------|
 | `Active` | 建議是作用中和未套用。 使用者可以建議指令碼，以手動方式執行它。 |
 | `Verifying` | 藉由套用建議[!INCLUDE[ssde_md](../../includes/ssde_md.md)]和內部的驗證程序會比較迴歸的計畫與強制的計劃的效能。 |
 | `Success` | 已成功套用建議。 |
 | `Reverted` | 因為不有任何顯著效能改善，會還原建議。 |
 | `Expired` | 建議已過期，且無法再套用。 |

中的 JSON 文件`state`資料行包含描述為何建議的目前狀態的原因。 在 [原因] 欄位中的值可能是： 

| Reason | 描述 |
|--------|-------------|
| `SchemaChanged` | 建議過期，因為參考的資料表的結構描述變更。 |
| `StatisticsChanged`| 建議過期，因為參考的資料表上的統計資料變更。 |
| `ForcingFailed` | 無法強制執行建議的計畫，查詢。 尋找`last_force_failure_reason`中[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)檢視，以找出失敗的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` 選項會停用使用者在驗證程序期間。 啟用`FORCE_LAST_GOOD_PLAN`選項使用[ALTER DATABASE 設定 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)陳述式或強制手動使用中的指令碼的計劃`[details]`資料行。 |
| `UnsupportedStatementType` | 無法在查詢上強制計劃。 不支援查詢的範例包括資料指標和`INSERT BULK`陳述式。 |
| `LastGoodPlanForced` | 已成功套用建議。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 識別潛在的效能變差，但是`FORCE_LAST_GOOD_PLAN`選項未啟用，請參閱 < [ALTER DATABASE 設定 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 手動套用建議，或啟用`FORCE_LAST_GOOD_PLAN`選項。 |
| `VerificationAborted`| 驗證程序 zrušena v důsledku 重新啟動或清除查詢存放區。 |
| `VerificationForcedQueryRecompile`| 因為沒有顯著的效能改進，會重新編譯查詢。 |
| `PlanForcedByUser`| 使用者以手動方式強制計劃使用[sp_query_store_force_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)程序。 |
| `PlanUnforcedByUser` | 使用者以手動方式運作計劃使用[sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)程序。 |

 在 詳細資料資料行的統計資料不會顯示執行階段計畫統計資料 （例如，目前 CPU 時間）。 建議的詳細資料會進行迴歸偵測的時間，並說明為什麼[!INCLUDE[ssde_md](../../includes/ssde_md.md)]識別效能變差。 使用`regressedPlanId`並`recommendedPlanId`來查詢[查詢存放區目錄檢視](../../relational-databases/performance/how-query-store-collects-data.md)若要尋找確切執行階段計畫的統計資料。

## <a name="using-tuning-recommendations-information"></a>使用微調建議資訊  
您可以使用下列查詢來取得[!INCLUDE[tsql](../../includes/tsql-md.md)]指令碼，將會修正此問題：  
 
```sql
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 如需有關可用來在 [建議] 檢視中的查詢值的 JSON 函式的詳細資訊，請參閱[JSON 支援](../../relational-databases/json/index.md)在[!INCLUDE[ssde_md](../../includes/ssde_md.md)]。
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   

## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支援](../../relational-databases/json/index.md)
 
