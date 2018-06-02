---
title: 自動調整 |Microsoft 文件
description: 深入了解 SQL Server 和 Azure SQL Database 中的自動調整
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 0e77a1d7e24fa2635b3e699672338e588c1f5c1c
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707766"
---
# <a name="automatic-tuning"></a>自動調整
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  「自動調整」是一種資料庫功能，可深入探索潛在的查詢效能問題、建議解決方法，並且自動修正找到的問題。

的自動調整[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]潛在的效能問題偵測到，而且可讓您套用的矯正措施時通知您，或者讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自動修正效能問題。
的自動調整[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]可讓您識別並修正效能問題所造成**SQL 計畫選擇迴歸**。 的自動調整[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]會建立必要的索引，並卸除未使用的索引。

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 監視資料庫上執行，但會自動改善效能的工作負載的查詢。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 具有內建智慧機制，可自動調整並透過動態調整您的工作負載的資料庫改善查詢效能。 有可用的兩個自動調整功能：

 -  **自動的計劃更正**(用於[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]) 有問題的查詢執行計畫識別並修正 SQL 規劃效能問題。
 -  **自動索引管理**(僅適用於[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)])，識別您的資料庫中，加入的索引和索引應該移除。

## <a name="why-automatic-tuning"></a>為什麼自動微調嗎？

其中一個傳統資料庫管理的主要工作正在監視的工作負載，識別重要[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查詢時，應該加入改善效能，並且很少使用的索引的索引。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 提供深入了解的查詢與您要監視的索引。 不過，不斷地監視 database 是永久且冗長的工作，尤其是在處理具有許多資料庫。 管理大量的資料庫可能會無法有效執行。 而不是監視，並手動調整您的資料庫，您可能會考慮委派給部分監視及調整動作[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自動調整功能。

### <a name="how-does-automatic-tuning-works"></a>自動微調的運作方式？

自動調整是連續的監視和不斷藉以了解您的工作負載特性的分析程序，並識別潛在的問題和增強功能。

![自動微調偵測程序](./media/tuning-process.png)

此程序可動態的方式適應您的工作負載，藉由尋找哪些索引和計劃可能會改善您的工作負載的效能，以及哪些索引會影響您的工作負載的資料庫。 根據這些研究結果，自動調整適用於可改善您的工作負載的效能調整動作。 此外，資料庫會持續監視效能以確保它可以改善您的工作負載的效能來自動微調所做的變更之後。 會自動還原並未改善效能，任何動作。 這個驗證程序是一項重要功能，可確保所做的自動調整的任何變更不會降低您的工作負載的效能。

## <a name="automatic-plan-correction"></a>計劃自動更正

自動的計劃修正是自動調整功能可識別**SQL 計畫選擇迴歸**並自動強制執行最後一個已知的良好計劃中修正問題。

### <a name="what-is-sql-plan-choice-regression"></a>什麼是 SQL 計畫選擇迴歸？

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 可能使用不同的 SQL 計畫來執行[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查詢。 查詢計劃的統計資料、 索引和其他因素而定。 應該用來執行部分的最佳計劃[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查詢可能會變更一段時間。 在某些情況下，新的計劃會優於上一個，而新的計劃可能會導致效能變差。

 ![SQL 計畫選擇迴歸](media/plan-choice-regression.png "SQL 計畫選擇迴歸") 

每當您會注意到計畫選擇迴歸，您應該會發現一些先前的很好的規劃和強制而不是目前另一種使用`sp_query_store_force_plan`程序。
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]提供有關迴歸計劃與建議的更正動作的資訊。
此外，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]可讓您完全自動化此程序，並讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]修正任何找到的問題相關的計劃變更。

### <a name="automatic-plan-choice-correction"></a>自動的計劃選擇更正

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以自動切換至最後一個已知的良好計劃時偵測到計畫選擇迴歸。

![SQL 計畫選擇更正](media/force-last-good-plan.png "SQL 計劃選擇更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會自動偵測包含計劃，而不是錯誤的計劃應該使用任何潛在計畫選擇迴歸。
當[!INCLUDE[ssde_md](../../includes/ssde_md.md)]套用上次已知良好的計劃，它會自動監視強制計畫的效能。 如果強制執行的計畫不是與迴歸的計畫更好的新的方案將會非強迫性和[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會編譯新的計畫。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會強制執行的計畫優於迴歸的其中一個，強制執行的計畫會保留之前 （例如，在下一步的統計資料或結構描述變更） 重新編譯比迴歸的計劃好的驗證。

附註： 任何的計劃自動強制執行動作不重新啟動 SQL Server 執行個體上的 persit。

### <a name="enabling-automatic-plan-choice-correction"></a>啟用自動計劃選擇更正

您可以依每個資料庫啟用自動調整，並指定只要偵測到某些計畫變更迴歸，就應該強制執行最後一個良好的計畫。 自動調整已使用下列命令啟用：

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
一旦您 turn-on 選取此選項，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會自動強制執行任何建議，其中的估計的 CPU 改善高於 10 秒，或新計劃中的錯誤數目高於錯誤數目中建議的計劃，並確認強制的計劃是優於目前的項目。

### <a name="alternative---manual-plan-choice-correction"></a>別名-手動計劃選擇更正

沒有自動調整，使用者必須定期監視系統，並尋找迴歸的查詢。 如果任何計劃迴歸，使用者應該會發現一些先前的很好的規劃和強制而不是目前另一種使用`sp_query_store_force_plan`程序。 最佳作法就是強制執行的最後一個已知的良好計畫，因為較舊的計劃可能無效，因為統計資料或索引的變更。 強制執行最後一個已知的良好計劃的使用者應該監視使用強制執行的計畫來執行查詢的效能，並確認該強制的計劃可以正常運作。 根據監視與分析的結果，應該強制計劃，或使用者應該會發現其他方式來最佳化查詢。
以手動方式強制執行的計畫應該不會強制，因為[!INCLUDE[ssde_md](../../includes/ssde_md.md)]應該要能夠套用最佳計劃。 使用者或 DBA 應該最後取消強制執行計劃使用`sp_query_store_unforce_plan`程序，並讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]尋找最佳的計劃。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供所有必要的檢視和監視效能及修正問題，查詢存放區中所需的程序。

在[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，您可以找到使用查詢存放區系統檢視的計畫選擇迴歸。 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]偵測，並顯示可能的計畫選擇迴歸和建議的動作應該套用在[sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)檢視。 檢視會顯示問題的重要性，問題，以及詳細資料，例如識別查詢的迴歸的計劃 ID、 已做為基準進行比較，使用計畫的識別碼的相關資訊和[!INCLUDE[tsql_md](../../includes/tsql_md.md)]可以修正執行陳述式發生問題。

| 型別 | description | DATETIME | score | 詳細資料 | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 從 4 毫秒變更為 14 毫秒 CPU 時間 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 從 37 毫秒變更為 84 ms 的 CPU 時間 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

下列清單將描述這個檢視中的一些資料行：
 - 建議的動作- `FORCE_LAST_GOOD_PLAN`。
 - 描述，其中包含的資訊為何[!INCLUDE[ssde_md](../../includes/ssde_md.md)]此計劃變更是潛在的效能變差。
 - 偵測到潛在的迴歸時的日期時間。
 - 這項建議的分數。 
 - 例如，偵測到計劃的迴歸的計劃，若要修正此問題，應該強制的計畫識別碼識別碼的識別碼問題詳細資訊 [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 若要修正問題等可能會套用的指令碼。詳細資料會儲存在[JSON 格式](../../relational-databases/json/index.md)。

取得使用下列查詢來取得的指令碼，修正的問題和相關的預估的其他資訊：

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | 指令碼 (script) | 查詢\_識別碼 | 目前的計劃\_識別碼 | 建議您計劃\_識別碼 | 估計\_取得 | 錯誤\_容易出錯
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 從 3 毫秒變更為 46 ms 的 CPU 時間 | 36 | EXEC sp\_查詢\_儲存\_強制\_計劃 12，17。 | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 代表的估計的秒數，如果會執行建議的計劃，而不是目前的計劃會儲存。 建議的計劃應該強制而非目前的計畫，如果提升的大於 10 秒。 如果有多個錯誤 （例如，逾時或已中止的執行） 比目前的計劃中建議計劃，資料行`error_prone`會設定為值`YES`。 錯誤容易出錯的計劃是另一個原因而不是目前為什麼應該強制建議的計劃。

雖然[!INCLUDE[ssde_md](../../includes/ssde_md.md)]提供找出計畫選擇迴歸; 連續監視並修正效能問題所需的所有資訊可能都是一件耗時。 自動調整使此程序更為容易。

注意： 這個 DMV 中的資料不保留任何 SQL Server 執行個體重新啟動之後。

## <a name="automatic-index-management"></a>自動索引管理

在[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]，索引管理很容易因為[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]藉以了解您的工作負載，並確保您的資料永遠以最佳方式編製索引。 適當的索引設計是非常重要，您的工作負載的最佳效能，並自動索引管理可以協助您最佳化您的索引。 自動索引管理可以是在資料庫中不正確的索引，修正效能問題或維護和改善現有的資料庫結構描述的索引。 的自動調整[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]執行下列動作：

 - 識別無法改善您從資料表讀取資料的 T-SQL 查詢效能的索引。
 - 識別重複的索引或在較長的時間內無法移除未使用的索引。 移除不必要的索引可改善更新資料表中的資料的查詢效能。

### <a name="why-do-you-need-index-management"></a>為什麼您需要索引管理？

索引加速某些查詢讀取資料的資料表。不過，它們變慢的查詢，更新資料。 您需要仔細分析建立索引的時機和哪些資料行要包含在索引中。 某些索引可能不需要一段時間後。 因此，您必須定期找出並卸除索引不會帶來任何益處。 如果您略過未使用的索引，更新資料的查詢效能會降低而沒有任何好處，在讀取資料的查詢。 未使用的索引也會影響整體系統效能，因為其他的更新需要不必要的記錄。

尋找一組最佳的索引可改善效能的查詢，從資料表讀取資料，以及對更新的影響降到最低的可能需要連續且複雜的分析。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 使用內建智慧和分析您查詢的進階的規則識別會是最適合您目前的工作負載的索引和索引可能會移除。 Azure SQL Database 可確保您已最佳化讀取的資料，與其他查詢的最小化影響查詢的索引所需的最小集合。

### <a name="automatic-index-management"></a>自動索引管理

除了偵測[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可以自動套用識別的建議。 如果您發現內建規則改善您資料庫的效能，您可能會讓[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自動管理您的索引。

若要啟用自動調整 Azure SQL Database 中，並讓完整管理您的工作負載自動調整功能，請參閱[啟用使用 Azure 入口網站的 Azure SQL Database 中的自動調整](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable)。

當[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]適用於建立索引或卸除索引建議事項，它會自動監視受影響的索引查詢的效能。 只有當受影響的查詢的效能已獲得改善，仍會保留新的索引。 如果有一些查詢來執行得較慢，因為索引不存在，就會自動重新建立卸除的索引。

### <a name="automatic-index-management-considerations"></a>自動索引管理考量

若要建立必要的索引所需的動作[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可能會耗用資源並暫時影響 工作負載效能。 索引建立工作負載效能的影響降到最低，Azure SQL Database，請尋找任何索引管理作業的適當的時間間隔。 微調動作就會延後，如果資料庫需要的資源來執行您的工作負載，並啟動時資料庫有足夠的資源運用於維護工作。 自動索引管理中的其中一項重要功能是一項動作的驗證。 當 Azure SQL Database 建立或卸除索引時，監視的處理序會分析您的工作負載，以確認此動作會提升效能的效能。 如果它未使顯著改進 – 立即還原動作。 如此一來，Azure SQL Database 可確保，自動動作不會影響您的工作負載的效能。 自動調整所建立的索引而言是透明的基礎結構描述的維護作業的。 例如，卸除或重新命名資料行的結構描述變更不會封鎖自動建立索引的存在。 自動建立的 Azure SQL Database 會立即卸除索引時相關的資料表或資料行遭到卸除。

### <a name="alternative---manual-index-management"></a>別名-手動索引管理

如果沒有自動索引管理功能，使用者必須手動查詢[sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)檢視來尋找的索引，可能會改善效能，建立索引使用的詳細資料此檢視，並手動監視效能的查詢中提供。 若要尋找應該卸除的索引，使用者應該監視尋找很少使用的索引的索引作業的使用量統計資料。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 簡化此程序。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 分析您的工作負載，會識別與新的索引，可能會更快速執行的查詢並找出未使用或重複的索引。 尋找詳細資訊的索引，應該在變更識別[在 Azure 入口網站中尋找的索引建議](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)。

## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函式](../../relational-databases/json/index.md)
