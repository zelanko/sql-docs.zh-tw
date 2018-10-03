---
title: 自動調整 |Microsoft Docs
description: 深入了解 SQL Server 和 Azure SQL Database 中的自動調整
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 639b2f5fd09ad017f94881358f8b2731cbd39c51
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849326"
---
# <a name="automatic-tuning"></a>自動調整
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  「自動調整」是一種資料庫功能，可深入探索潛在的查詢效能問題、建議解決方法，並且自動修正找到的問題。

中的自動調整[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]通知您，只要偵測到，潛在的效能問題，並可讓您套用矯正措施，或讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自動修正效能問題。
中的自動調整[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]可讓您識別並修正效能問題所造成**SQL 計畫選擇迴歸**。 中的自動調整[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]會建立必要的索引，並卸除未使用的索引。

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 監視的查詢，在資料庫上執行，並會自動改善工作負載的效能。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 有內建智慧機制可自動調整並改善查詢效能的動態調整您的工作負載的資料庫。 有兩個自動調整功能，可用：

 -  **自動計劃更正**(用於[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)])，識別有問題的查詢執行計劃，並修正 SQL 計劃效能問題。
 -  **自動索引管理**(僅適用於[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)])，識別應該在資料庫中，新增的索引和索引，應該移除。

## <a name="why-automatic-tuning"></a>為什麼自動調整？

三個傳統資料庫系統管理的主要工作正在監視的工作負載中，然後再用來識別重要[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查詢時，應新增以提升效能，以及識別很少使用的索引。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 提供之查詢和索引，您需要監視的詳細的解析。 不過，持續監視資料庫是困難且單調乏味的工作，特別是在處理多個資料庫。 管理大量資料庫可能無法有效率地。 而不是監視和手動調整您的資料庫，您可以考慮委派部分監視和微調動作[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自動調整功能。

### <a name="how-does-automatic-tuning-work"></a>自動調整的方式為何？

自動調整是以持續監視和分析程序，持續了解您的工作負載的特性，並識別潛在的問題和增強功能。

![自動調整程序](./media/tuning-process.png)

此程序會讓資料庫可動態地適應您的工作負載，找出哪些索引和計劃可能會改善您的工作負載的效能，以及哪些索引會影響您的工作負載。 根據這些調查結果，自動調整會套用可改善您的工作負載的效能調整動作。 此外，資料庫會持續監視以確保它可以改善效能，您的工作負載自動調整所做的任何變更之後的效能。 未能改善效能的任何動作都會自動還原。 這個驗證程序是一項重要功能，可確保自動調整所做的任何變更不會降低工作負載的效能。

## <a name="automatic-plan-correction"></a>自動計劃更正

自動計劃更正程序的自動調整功能，可識別**SQL 計畫選擇迴歸**自動強制執行最後一個已知的良好計畫中修正此問題。

### <a name="what-is-sql-plan-choice-regression"></a>什麼是 SQL 計畫選擇迴歸？

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 可能使用不同的 SQL 計劃來執行[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查詢。 查詢計劃，需視統計資料、 索引和其他因素而定。 應該用來執行某些的最佳計劃[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查詢可能會變更一段時間。 在某些情況下，新的計劃可能無法高於前一個位置，而且新的計劃可能會導致效能變差。

 ![SQL 計畫選擇迴歸](media/plan-choice-regression.png "SQL 計畫選擇迴歸") 

每當您注意到計畫選擇迴歸，您應該會發現一些先前的良好計劃，並強制而不是目前另一種使用`sp_query_store_force_plan`程序。
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]提供有關迴歸計畫與建議的更正動作的資訊。
此外，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]可讓您完全自動化此程序，並讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]修正任何發現的問題相關的計劃變更。

### <a name="automatic-plan-choice-correction"></a>自動計畫選擇更正

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以自動切換至最後一個已知的良好計畫時偵測到計畫選擇迴歸。

![SQL 計畫選擇更正](media/force-last-good-plan.png "SQL 計畫選擇更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會自動偵測任何可能的計畫選擇迴歸包括應該使用而不是錯誤的計劃的計劃。
當[!INCLUDE[ssde_md](../../includes/ssde_md.md)]套用最後一個已知的良好計劃，它會自動監視強制計畫的效能。 如果強制執行的計畫不比迴歸計畫好，新的方案將會強制執行和[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會編譯新計畫。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]確認強制的計畫比迴歸的一個好，比迴歸計畫好，將會重新編譯 （例如，在下一步 的統計資料或結構描述變更） 之前保留強制的計畫。

注意： 強制執行任何計劃自動執行不 persit 上重新啟動 SQL Server 執行個體。

### <a name="enabling-automatic-plan-choice-correction"></a>啟用自動計畫選擇更正

您可以依每個資料庫啟用自動調整，並指定只要偵測到某些計畫變更迴歸，就應該強制執行最後一個良好的計畫。 自動調整已使用下列命令啟用：

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
一旦您開啟此選項，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]會自動強制執行任何建議，估計的 CPU 增量高於 10 秒，或在新的計劃中的錯誤數目高於錯誤數目為建議的方案，並確認強制計劃是優於目前的項目。

### <a name="alternative---manual-plan-choice-correction"></a>其他選項-手動計畫選擇更正

沒有自動調整，使用者必須定期監視系統，並尋找迴歸的查詢。 如果任何計畫迴歸，使用者應該會發現一些先前的良好計劃，並強制而不是目前另一種使用`sp_query_store_force_plan`程序。 最佳做法是強制執行最後一個已知的良好計畫，因為較舊的計劃可能無效，因為統計資料或索引的變更。 強制執行最後一個已知的良好計畫的使用者應該監視會使用強制的計劃來執行查詢的效能，並確認該強制的計劃可以正常運作。 根據監視與分析的結果，應該強制執行計畫，或使用者應該會發現某種其他方式來最佳化查詢。
以手動方式強制計劃應該不會強制，因為[!INCLUDE[ssde_md](../../includes/ssde_md.md)]應該能夠套用最佳的計劃。 使用者或 DBA 應該最後取消強制執行計劃使用`sp_query_store_unforce_plan`程序，並讓[!INCLUDE[ssde_md](../../includes/ssde_md.md)]尋找最佳的計劃。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供所有必要的檢視和監視效能和查詢存放區中修正問題所需的程序。

在  [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，您可以找到使用查詢存放區的系統檢視的計畫選擇迴歸。 中[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]，則[!INCLUDE[ssde_md](../../includes/ssde_md.md)]偵測到，並顯示可能的計畫選擇迴歸和建議的動作應該套用在[sys.dm_db_tuning_recommendations &#40;-&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)檢視。 檢視會顯示相關問題的重要性，問題，以及詳細資料，例如識別查詢中，迴歸的計畫的識別碼，用來作為基礎進行比較，計畫的識別碼資訊和[!INCLUDE[tsql_md](../../includes/tsql-md.md)]可以執行，以修正的陳述式發生問題。

| 型別 | description | DATETIME | score | 詳細資料 | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 從 4 毫秒變更為 14 毫秒的 CPU 時間 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 從 37 毫秒變更為 84 毫秒的 CPU 時間 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

從這個檢視中的某些資料行是以下列清單所述：
 - 建議的動作- `FORCE_LAST_GOOD_PLAN`。
 - 為何要包含資訊的描述[!INCLUDE[ssde_md](../../includes/ssde_md.md)]認為此計劃變更是潛在的效能變差。
 - 日期時間偵測到潛在的迴歸。
 - 此建議的分數。 
 - 偵測到的計畫迴歸的計畫，以修正此問題，應該強制計畫的識別碼的識別碼的識別碼等問題的詳細資料[!INCLUDE[tsql_md](../../includes/tsql-md.md)]指令碼，可能會套用至修正的問題，依此類推。詳細資料會儲存在[JSON 格式](../../relational-databases/json/index.md)。

使用下列查詢，以取得修正的問題和相關的預估的其他資訊的指令碼取得：

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
| 從 3 毫秒變更為 46 毫秒的 CPU 時間 | 36 | EXEC sp\_查詢\_儲存\_強制\_計劃 12，17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 代表估計如果會執行建議的計劃，而不是目前的計劃會儲存的秒數。 建議的計劃應該強制而不是目前的計劃，如果增益很大於 10 秒。 如果多個錯誤 （例如，逾時或已中止的執行） 比目前的計劃中有建議計劃，資料行`error_prone`會設定為值`YES`。 錯誤很容易出錯的計劃是為什麼應該強制建議的方案而不是目前的另一個原因。

雖然[!INCLUDE[ssde_md](../../includes/ssde_md.md)]識別計畫選擇迴歸，持續監視並修正效能問題所需的所有資訊都可能冗長的程序。 自動調整可讓此程序更容易。

注意： 這個 DMV 中的資料不會保存在 SQL Server 執行個體重新啟動之後。

## <a name="automatic-index-management"></a>自動索引管理

在  [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]，所以索引管理很容易因為[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]會了解您的工作負載，並可確保您的資料會永遠以最佳方式編製索引。 適當的索引設計非常重要的工作負載，達到最佳效能，並自動索引管理可以協助您最佳化您的索引。 自動索引管理可以修正不正確索引的資料庫中的效能問題或維護並改善現有的資料庫結構描述的索引。 中的自動調整[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]執行下列動作：

 - 找出可改善效能的 T-SQL 查詢從資料表讀取資料的索引。
 - 識別重複的索引或未使用的較長的一段時間無法移除的索引。 移除不必要的索引可改善更新資料表中的資料的查詢效能。

### <a name="why-do-you-need-index-management"></a>為什麼需要索引管理？

索引可加速某些從資料表讀取資料查詢不過，這些變慢的查詢，更新資料。 您需要仔細分析建立索引的時機及哪些資料行要包含在索引中。 某些索引可能不需要一些時間之後。 因此，您必須定期找出並卸除索引不會帶來任何好處。 如果您忽略未使用的索引時，更新資料的查詢效能會減少讀取資料的查詢上毫無益處。 未使用的索引也會影響整體系統效能，因為其他的更新需要不必要的記錄。

尋找一組最佳的索引可改善效能的查詢，從資料表讀取資料，並對更新的影響降到最低的可能需要持續進行複雜分析。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 使用內建智慧和進階的規則，以分析您的查詢，識別會是最適合您目前的工作負載的索引和索引可能會移除。 Azure SQL Database 可確保最佳化讀取資料，以對其他查詢的影響降到最低的查詢的索引所需的最小集合。

### <a name="automatic-index-management"></a>自動索引管理

除了偵測[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可以自動套用已識別的建議。 如果您發現內建的規則，改善您資料庫的效能，您可能會讓[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自動管理索引。

若要啟用自動調整 Azure SQL Database 中，並讓自動調整的功能完全管理您的工作負載，請參閱[啟用使用 Azure 入口網站的 Azure SQL Database 中的自動調整](https://docs.microsoft.com/azure/sql-database/sql-database-automatic-tuning-enable)。

當[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]適用於建立索引或卸除索引建議，它會自動監視受影響的索引查詢的效能。 只有當受影響之查詢的效能改進，仍會保留新的索引。 如果有一些由於沒有索引的執行速度變慢的查詢，就會自動重新建立已卸除的索引。

### <a name="automatic-index-management-considerations"></a>自動索引管理考量

建立必要索引所需的動作[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可能會耗用資源並暫時影響工作負載效能。 索引建立工作負載效能的影響降到最低，Azure SQL Database 會尋找適當的時間範圍的任何索引管理作業。 微調動作就會延後，如果資料庫需要的資源來執行您的工作負載，並啟動時在資料庫有足夠的資源運用於維護工作。 自動索引管理中的一個重要功能是驗證動作成效。 當 Azure SQL Database 建立或卸除索引時，監視的程序會分析您的工作負載，以確認該動作可以改善效能的效能。 如果沒有顯著改善-就會立即還原動作。 如此一來，Azure SQL Database 可確保自動動作執行不造成負面影響工作負載的效能。 自動調整所建立的索引而言是透明的基礎結構描述的維護作業。 例如卸除或重新命名資料行的結構描述變更不會封鎖所自動建立索引的目前狀態。 自動建立的 Azure SQL Database 會立即卸除索引時相關的資料表或資料行遭到卸除。

### <a name="alternative---manual-index-management"></a>其他選項-手動索引管理

如果沒有自動索引管理功能，使用者必須以手動方式查詢[sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)若要尋找的索引，可能會改善效能，建立索引使用的詳細資料檢視在此檢視中，並手動監視效能的查詢中提供。 若要尋找應該卸除索引，使用者應該監視作業的使用量統計資料，很少使用的尋找索引的索引。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 簡化此程序。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 分析工作負載，找出無法使用新的索引，更快速執行查詢，找出未使用或重複的索引。 找到的索引，應該在變更的詳細資訊[Azure 入口網站中尋找索引建議](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)。

## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函式](../../relational-databases/json/index.md)
