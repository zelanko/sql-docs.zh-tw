---
title: "sys.dm_db_tuning_recommendations (TRANSACT-SQL) |Microsoft 文件"
description: "了解如何找出潛在的效能問題，並建議修正 SQL Server 和 Azure SQL Database"
ms.custom: 
ms.date: 07/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 43acc4c2bfbcb9458f93f2ad89414e3781a7836d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_tuning\_recommendations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  傳回有關微調建議的詳細的資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。

| **資料行名稱** | **資料類型** | **說明** |
| --- | --- | --- |
| **name** | **nvarchar(4000)** | 建議的唯一名稱。 |
| **type** | **nvarchar(4000)** | 產生的建議，例如自動微調選項的名稱`FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 為什麼提供這項建議的原因。 |
| **valid\_since** | **datetime2** | 第一次產生這項建議。 |
| **last\_refresh** | **datetime2** | 最後一次產生這項建議。 |
| **狀態** | **nvarchar(4000)** | JSON 文件描述建議事項的狀態。 可用的欄位如下：<br />-   `currentValue`-建議的目前狀態。<br />-   `reason`– 說明建議處於目前狀態的常數。|
| **is\_executable\_action** | **bit** | 1 = 建議可以針對透過資料庫來執行[!INCLUDE[tsql_md](../../includes/tsql_md.md)]指令碼。<br />0 = 無法針對資料庫執行的建議事項 (例如： 資訊只有或已還原的建議) |
| **is\_revertable\_action** | **bit** | 1 = 建議可以自動監控和 Database engine 所還原。<br />0 = 建議無法自動監控和還原。 大部分&quot;可執行檔&quot;動作將會是&quot;revertable&quot;。 |
| **execute\_action\_start\_time** | **datetime2** | 套用建議的日期。 |
| **execute\_action\_duration** | **time** | 執行動作的持續時間。 |
| **execute\_action\_initiated\_by** | **nvarchar(4000)** | `User`= 使用者手動強制建議事項中的計劃。 <br /> `System`= 系統會自動套用建議事項。 |
| **execute\_action\_initiated\_time** | **datetime2** | 已套用建議的日期。 |
| **revert\_action\_start\_time** | **datetime2** | 建議已還原的日期。 |
| **revert\_action\_duration** | **time** | 還原動作的持續時間。 |
| **revert\_action\_initiated\_by** | **nvarchar(4000)** | `User`= 使用者手動非強迫性的建議計劃。 <br /> `System`= 系統會自動還原建議。 |
| **revert\_action\_initiated\_time** | **datetime2** | 建議已還原的日期。 |
| **score** | **int** | 估計值/影響此建議在 0 到 100 之間的小數位數 （越大越好） |
| **details** | **nvarchar(max)** | 包含建議的更多詳細的 JSON 文件。 可用的欄位如下：<br /><br />`planForceDetails`<br />-    `queryId`-查詢\_迴歸查詢的識別碼。<br />-    `regressedPlanId`-plan_id 迴歸的計劃。<br />-   `regressedPlanExecutionCount`的偵測到執行與迴歸的計劃之前，迴歸查詢的次數。<br />-    `regressedPlanAbortedCount`-迴歸的計畫執行期間偵測到的錯誤數目。<br />-    `regressedPlanCpuTimeAverage`的在偵測到迴歸之前由迴歸查詢平均 CPU 時間。<br />-    `regressedPlanCpuTimeStddev`的偵測到的迴歸之前迴歸的查詢所耗用的 CPU 時間標準差。<br />-    `recommendedPlanId`-plan_id 應該強制的計畫。<br />-   `recommendedPlanExecutionCount`-執行具有在偵測到迴歸之前應該強制的計劃的查詢數目。<br />-    `recommendedPlanAbortedCount`-應該強制的計畫執行期間偵測到的錯誤數目。<br />-    `recommendedPlanCpuTimeAverage`-平均 （計算之前偵測到迴歸） 應該強制計畫來執行查詢所耗用的 CPU 時間。<br />-    `recommendedPlanCpuTimeStddev`偵測到的迴歸之前迴歸的查詢所耗用的 CPU 時間的標準差。<br /><br />`implementationDetails`<br />-  `method`的應該用來更正迴歸方法。 值一律是`TSql`。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)]應強制執行建議的計畫執行的指令碼。 |
  
## <a name="remarks"></a>備註  
 所傳回的資訊`sys.dm_db_tuning_recommendations`資料庫引擎會識別可能發生的查詢效能低下，並不會保存時，會更新。 建議會保留只[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新啟動。 如果想要保留在伺服器回收之後，資料庫管理員應該定期製作微調建議的備份副本。 

 `currentValue`欄位中`state`資料行可能會有下列值：
 | 狀態 | Description |
 |--------|-------------|
 | `Active` | 建議是使用中和未套用。 使用者可以使用建議指令碼，並手動執行它。 |
 | `Verifying` | 建議由套用[!INCLUDE[ssde_md](../../includes/ssde_md.md)]和內部驗證程序的比較與迴歸的計劃強制執行的計畫的效能。 |
 | `Success` | 已成功套用建議事項。 |
 | `Reverted` | 建議被還原，因為不有任何顯著的效能提升。 |
 | `Expired` | 建議已經過期，且無法再套用。 |

中的 JSON 文件`state`資料行包含描述為何中的目前狀態的建議動作的原因。 在 [原因] 欄位中的值可能是： 

| Reason | Description |
|--------|-------------|
| `SchemaChanged` | 建議過期，因為參考的資料表結構描述變更。 |
| `StatisticsChanged`| 建議過期，因為被參考的資料表上統計資料變更。 |
| `ForcingFailed` | 無法查詢上強制建議計劃。 尋找`last_force_failure_reason`中[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)檢視，以找出失敗的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`選項會停用使用者驗證程序期間。 啟用`FORCE_LAST_GOOD_PLAN`選項使用[設定 AUTOMATIC_TUNING ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)陳述式或強制的計劃使用中的指令碼，以手動方式`[details]`資料行。 |
| `UnsupportedStatementType` | 無法查詢上強制計劃。 不支援查詢的範例包括資料指標和`INSERT BULK`陳述式。 |
| `LastGoodPlanForced` | 已成功套用建議事項。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 識別潛在的效能變差，但是`FORCE_LAST_GOOD_PLAN`選項未啟用 – 請參閱[設定 AUTOMATIC_TUNING ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 手動套用建議，或啟用`FORCE_LAST_GOOD_PLAN`選項。 |
| `VerificationAborted`| 驗證程序會因重新啟動或中止查詢存放區清除。 |
| `VerificationForcedQueryRecompile`| 查詢會重新編譯，因為沒有顯著的效能改進。 |
| `PlanForcedByUser`| 使用者以手動方式強制執行計劃使用[sp_query_store_force_plan &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)程序。 |
| `PlanUnforcedByUser` | 使用者以手動方式運作計劃使用[sp_query_store_unforce_plan &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)程序。 |

 在詳細資料資料行的統計資料不會顯示執行階段計畫統計資料 （例如，目前 CPU 時間）。 建議的詳細資料所攝取的迴歸偵測和描述為何[!INCLUDE[ssde_md](../../includes/ssde_md.md)]識別效能變差。 使用`regressedPlanId`和`recommendedPlanId`查詢[查詢存放區目錄檢視](../../relational-databases/performance/how-query-store-collects-data.md)尋找確切執行階段計畫的統計資料。

## <a name="using-tuning-recommendations-information"></a>使用微調建議的資訊  
 若要取得的 T-SQL 指令碼會修正此問題，您可以使用下列查詢：  
 
```
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
  
 如需可用於建議檢視中查詢值的 JSON 函式的詳細資訊，請參閱[JSON 支援](../../relational-databases/json/index.md)中[!INCLUDE[ssde_md](../../includes/ssde_md.md)]。
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要`Server admin`或`Azure Active Directory admin`帳戶。  
  
## <a name="see-also"></a>另請參閱  
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支援](../../relational-databases/json/index.md)
 
