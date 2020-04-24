---
title: 自動調整 |Microsoft Docs
description: 瞭解 SQL Server 和 Azure SQL Database 中的自動調整
ms.custom: fasttrack-edit
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ce830c3fcd5661a01ecc0ad3ad84bed420be2e0
ms.sourcegitcommit: 1f9fc7402b00b9f35e02d5f1e67cad2f5e66e73a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2020
ms.locfileid: "82107981"
---
# <a name="automatic-tuning"></a>自動微調
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

「自動調整」是一種資料庫功能，可深入探索潛在的查詢效能問題、建議解決方法，並且自動修正找到的問題。

中[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]的自動調整會在偵測到潛在的效能問題時通知您，並可讓您套用矯正措施[!INCLUDE[ssde_md](../../includes/ssde_md.md)] ，或讓自動修正效能問題。 中的[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]自動調整可讓您識別並修正**查詢執行計畫選擇回歸**所造成的效能問題。 中的[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自動調整也會建立所需的索引，並卸載未使用的索引。 如需查詢執行計畫的詳細資訊，請參閱[執行計畫](../../relational-databases/performance/execution-plans.md)。

會[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]監視在資料庫上執行的查詢，並自動改善工作負載的效能。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]具有內建的智慧機制，可以透過動態地將資料庫調整為您的工作負載，來自動微調和改善查詢的效能。 有兩個自動調整功能可供使用：

 -  **自動計畫更正**會識別有問題的查詢執行計畫，並修正查詢執行計畫的效能問題。 **適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (從 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 開始) 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **自動索引管理**會識別應該在您的資料庫中新增的索引，以及應該移除的索引。 **適用於**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>為何需要自動調整？

傳統資料庫管理中的三個主要工作，就是監視工作負載、 [!INCLUDE[tsql_md](../../includes/tsql-md.md)]識別重要查詢，以及識別應該加入以改善效能的索引，或是很少使用且可移除的索引以改善效能。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]提供您需要監視之查詢和索引的詳細見解。 不過，持續監控資料庫是一項困難又繁瑣的工作，特別是在處理許多資料庫時。 可能無法有效率地管理大量資料庫。 您可以考慮[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自動調整功能將一些監視和微調動作委派給，而不是手動監視和調整資料庫。

### <a name="how-does-automatic-tuning-work"></a>自動調整的運作方式為何？

自動調整是一種持續的監視和分析程式，它會不斷地瞭解您工作負載的特性，並找出潛在的問題和改進。

![自動調整程序](./media/tuning-process.png)

此程式可讓資料庫藉由尋找哪些索引和計畫可以改善工作負載的效能，以及哪些索引會影響您的工作負載，以動態方式調整您的工作負載。 根據這些結果，自動調整會套用可改善工作負載效能的微調動作。 此外，自動調整會在執行任何變更後持續監視資料庫的效能，以確保它能改善工作負載的效能。 未改善效能的任何動作都會自動還原。 此驗證程式是一項重要功能，可確保自動調整所做的任何變更，都不會降低工作負載的整體效能。

## <a name="automatic-plan-correction"></a>自動計畫更正

自動計畫更正是一個自動調整功能，可識別**執行計畫選擇回歸**，並藉由強制執行最後一個已知的良好計畫來自動修正此問題。 如需查詢執行計畫和查詢最佳化工具的詳細資訊，請參閱[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)。

### <a name="what-is-execution-plan-choice-regression"></a>什麼是執行計畫選擇回歸？

可能[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)]會使用不同的執行計畫來執行[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查詢。 查詢計劃取決於統計資料、索引和其他因素。 根據這些因素的變更而定，應該用[!INCLUDE[tsql_md](../../includes/tsql-md.md)]來執行查詢的最佳計畫可能會隨時間而改變。 在某些情況下，新的計畫可能不會比上一個方案好，而且新的計畫可能會導致效能衰退。

 ![查詢執行計畫選擇回歸](media/plan-choice-regression.png "查詢執行計畫選擇回歸") 

當您注意到計畫選擇回歸時，您應該會發現先前的良好計畫，並強制其使用，而不是目前的方案。 您可以使用`sp_query_store_force_plan`程式來完成這項作業。 中[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]的提供回歸計畫和建議的修正動作的相關資訊。 此外， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]可讓您將此程式完全自動化， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]並讓您修正任何與計畫變更相關的問題。

### <a name="automatic-plan-choice-correction"></a>自動計劃選擇更正

可以[!INCLUDE[ssde_md](../../includes/ssde_md.md)]在偵測到計畫選擇回歸時，自動切換至最後一個已知良好的計畫。

![查詢執行計畫選擇更正](media/force-last-good-plan.png "查詢執行計畫選擇更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會自動偵測任何可能的計畫選擇回歸，包括應該使用的計畫，而不是錯誤的計畫。 當[!INCLUDE[ssde_md](../../includes/ssde_md.md)]套用最後一個已知的良好計畫時，它會自動監視強制計畫的效能。 如果強制計畫不是優於回歸計畫，則會取消新的計畫，而且會編譯新[!INCLUDE[ssde_md](../../includes/ssde_md.md)]的計畫。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]確認強制計畫比回歸計畫好，則會保留強制的計畫。 它將會保留，直到重新編譯發生為止（例如，在下一個統計資料更新或架構變更時）。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的重新開機之間不會保存任何自動強制執行計畫。

### <a name="enabling-automatic-plan-choice-correction"></a>啟用自動計畫選擇更正

您可以啟用 [每個資料庫的自動調整]，並指定在偵測到某些計畫變更回歸時，應該強制執行最後一個良好的計畫。 自動調整已使用下列命令啟用：

```sql   
ALTER DATABASE <yourDatabase>
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

一旦啟用此選項， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]將會自動強制執行估計 CPU 增益高於10秒的任何建議，或是新計畫中的錯誤數目高於建議計畫中的錯誤數目，並確認強制的計畫優於目前的方案。

### <a name="alternative---manual-plan-choice-correction"></a>其他選項 - 手動計畫選擇更正

如果沒有自動調整，使用者必須定期監視系統，並尋找具有回歸的查詢。 如果有任何計畫回歸，使用者應該會發現先前的良好計畫，並使用`sp_query_store_force_plan`程式來強制執行，而不是目前的方案。 最佳做法是強制執行最後一個已知良好的計畫，因為較舊的計畫可能因為統計資料或索引變更而無效。 強制執行最後一個已知良好計畫的使用者，應該使用強制計畫來監視執行查詢的效能，並確認強制計畫如預期般運作。 視監視和分析的結果而定，應強制執行計畫，或使用者應該尋找另一種方式來優化查詢，例如重寫。 手動強制計畫不應永遠強制執行，因為[!INCLUDE[ssde_md](../../includes/ssde_md.md)]應該能夠套用最佳計畫。 使用者或 DBA 最終應該會使用`sp_query_store_unforce_plan`程式來取消強制執行計畫，並讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]尋找最佳的計畫。 

> [!TIP]
> 或者，使用**具有強制計畫的查詢**查詢存放區 view 來尋找並取消強制執行計畫。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供在查詢存放區中監視效能和修正問題所需的所有必要的視圖和程式。

在[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]中，您可以使用查詢存放區系統檢視來尋找計畫選擇回歸。 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]中， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]會偵測並顯示潛在的計畫選擇回歸，以及應該在[dm_db_tuning_recommendations &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)視圖中套用的建議動作。 此視圖會顯示問題的相關資訊、問題的重要性，以及詳細資料，例如已識別的查詢、回歸計畫的識別碼、做為比較基準使用的計畫識別碼，以及可執行以修正問題的[!INCLUDE[tsql_md](../../includes/tsql-md.md)]語句。

| type | description | Datetime | score | 詳細資料 | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | CPU 時間已從4毫秒變更為14毫秒 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | CPU 時間已從37毫秒變更為84毫秒 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

下列清單會說明此視圖中的一些資料行：
 - 建議動作的類型-`FORCE_LAST_GOOD_PLAN`
 - 描述，其中包含[!INCLUDE[ssde_md](../../includes/ssde_md.md)]認為此計畫變更為潛在效能回歸的資訊
 - 偵測到潛在回歸時的日期時間
 - 這項建議的分數
 - 問題的詳細資料，例如偵測到的計畫識別碼、回歸計畫的識別碼、應強制修正問題的計畫識別碼、 [!INCLUDE[tsql_md](../../includes/tsql-md.md)]可能會套用以修正問題的腳本等等。詳細資料會以[JSON 格式](../../relational-databases/json/index.md)儲存

使用下列查詢來取得可修正問題的腳本，以及有關估計增益的其他資訊：

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
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

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | 指令碼 (script) | 查詢\_識別碼 | 目前的\_方案識別碼 | 建議的\_方案識別碼 | 估計\_增益 | 容易\_出錯
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CPU 時間已從3毫秒變更為46毫秒 | 36 | EXEC sp\_查詢\_存放\_區\_強制執行計畫12、17、 | 12 | 28 | 17 | 11.59 | 0

資料行`estimated_gain`代表建議的計畫用於查詢執行，而不是目前的計畫時，所要儲存的估計秒數。 如果增益大於10秒，建議的計畫應強制執行，而不是目前的計畫。 如果目前計畫中的錯誤（例如，超時或已中止的執行）超過建議的計畫，則`error_prone`資料行會設定為值。 `YES` 容易出錯的計畫是建議的計畫應強制執行的另一個原因，而不是目前的方案。

雖然[!INCLUDE[ssde_md](../../includes/ssde_md.md)]提供識別計畫選擇回歸所需的所有資訊，但持續監視和修正效能問題可能會變得繁瑣。 自動調整可讓此程式更容易。

> [!NOTE]
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的重新開機之間不會保存 dm_db_tuning_recommendations DMV 中的資料。

## <a name="automatic-index-management"></a>自動索引管理

在[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]中，索引管理很簡單[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] ，因為瞭解您的工作負載，並確保您的資料一律會以最佳方式編制索引。 您的工作負載要達到最佳效能，有適當的索引設計非常重要，而且自動索引管理可以協助您將索引最佳化。 自動索引管理可以修正資料庫中索引編製不正確所造成的效能問題，或維護和改善現有資料庫結構描述的索引。 中[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]的自動調整會執行下列動作：

 - 識別可改善[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查詢的效能的索引，以從資料表讀取資料。
 - 識別在較長時間內無法移除的重複索引或索引。 移除不必要的索引可改善在資料表中更新資料之查詢的效能。

### <a name="why-do-you-need-index-management"></a>為什麼需要索引管理？

索引會加速一些從資料表讀取資料的查詢，但它們可能會使更新資料的查詢變慢。 您需要仔細分析建立索引的時機，以及要將哪些資料行包含在索引中。 某些索引在一段時間後可能不再需要。 因此，您必須定期識別並卸載這些不會帶來任何好處的索引。 如果您忽略未使用的索引，更新資料之查詢的效能就會減少，而不會對讀取資料的查詢有任何好處。 未使用的索引也會影響整體系統效能，因為其他的更新需要不必要的記錄。

找出一組最佳的索引，能改善查詢從資料表讀取資料時的效能，並對需要持續進行複雜分析的更新之影響降到最低。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]會使用內建智慧和先進的規則來分析您的查詢、識別最適合您目前工作負載的索引，以及識別可能需要移除的索引。 Azure SQL Database 可確保您擁有最少的必要索引，以將讀取資料的查詢優化，並將對其他查詢的影響降至最低。

### <a name="automatic-index-management"></a>自動索引管理

除了偵測， [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可以自動套用已識別的建議。 如果您發現內建規則會改善資料庫的效能，您可以讓[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自動管理您的索引。

若要在中[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]啟用自動調整，並允許自動調整功能來完全管理您的工作負載，請參閱[使用 Azure 入口網站在 Azure SQL Database 中啟用自動調整](/azure/sql-database/sql-database-automatic-tuning-enable)。

當[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]套用建立索引或 DROP INDEX 建議時，它會自動監視受索引影響之查詢的效能。 只有在改善受影響查詢的效能時，才會保留新的索引。 如果有一些查詢因為沒有索引而執行速度較慢，則會自動重新建立卸載的索引。

### <a name="automatic-index-management-considerations"></a>自動索引管理考量

在中[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]建立必要索引所需的動作可能會耗用資源，而暫時會影響工作負載的效能。 若要將索引建立對工作負載效能的影響[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]降至最低，請尋找任何索引管理作業的適當時間範圍。 如果資料庫需要資源來執行您的工作負載，則微調動作會延後，而且當資料庫有足夠的未使用資源可用於維護工作時，就會重新開機。 自動索引管理的其中一項重要功能是驗證動作成效。 當[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]建立或卸載索引時，監視程式會分析工作負載的效能，以確認動作已改善整體效能。 如果未帶來顯著的改善，則會立即還原動作。 如此一來[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] ，可確保自動調整動作不會對工作負載的效能造成負面影響。 基礎結構描述的維護作業清楚了解自動調整所建立的索引。 自動建立索引的存在並不會封鎖卸除或重新命名資料行這類的結構描述變更。 當相關的資料表或資料[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]行卸載時，會立即卸載由自動建立的索引。

### <a name="alternative---manual-index-management"></a>替代-手動索引管理

如果沒有自動索引管理，使用者或 DBA 就必須手動查詢[sys.databases dm_db_missing_index_details &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)視圖，或使用中[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]的 [效能儀表板] 報表來尋找可能會改善效能的索引、使用此視圖中提供的詳細資料來建立索引，以及手動監視查詢的效能。 若要尋找應卸載的索引，使用者應該監視索引的操作使用方式統計資料，以找出很少使用的索引。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]簡化此程式。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]會分析您的工作負載、識別可使用新索引更快執行的查詢，並識別未使用或重複的索引。 如需找出應變更的索引詳細資訊，可在 [Azure 入口網站中的尋找索引建議](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)中找到。

## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [database_automatic_tuning_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [dm_db_tuning_recommendations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [dm_db_missing_index_details &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函式](../../relational-databases/json/index.md)    
 [執行計畫](../../relational-databases/performance/execution-plans.md)    
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [效能監視和微調工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [查詢調整小幫手](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
