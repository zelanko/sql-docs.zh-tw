

### <a name="index-stats-options"></a>索引統計資料選項

<!--
This includes/paragraph-content/ file was created when processing vsts sqlbuvsts01 2999014 (5589131).  genemi  2017-07-21

Initially used in:
- relational-databases/maintenance-plans/rebuild-index-task-maintenance-plan.md
- relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md
-->


在舊版的 Microsoft SQL Server 中，於重新組織或重建大型索引時，可能會導致系統變慢。 SQL Server 2016 已針對這類索引作業實作重大效能改善。

此外，舊版中控制的細微性相對較不精確。 這使系統在某些索引並未嚴重片段化的情況下，也會對它們進行重新組織或重建，進而浪費資源。 維護計畫使用者介面 (UI) 上的新控制項，可讓您根據索引統計資料準則，排除不需要重新整理的索引。 針對此功能，會在內部使用下列 Transact-SQL 動態管理檢視 (DMV)：


- [sys.dm_db_index_usage_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)
- [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)


 **掃描類型**  
 系統必須使用資源來收集索引統計資料。 您可以根據所需的索引統計資料精確度，選擇使用相對較少或更多的資源。 UI 會提供下列精確度層級的清單，您必須選擇其中一個：


- 快速
- 取樣
- 詳細


 **只在下列情況下才進行索引最佳化:**  
 UI 提供下列可調整的篩選條件，可讓您用來避免重新整理還不需要立即重新整理的索引：


- 片段 &gt; *(%)*
- 頁面計數 &gt;
- 使用時間在過去 (天) 

