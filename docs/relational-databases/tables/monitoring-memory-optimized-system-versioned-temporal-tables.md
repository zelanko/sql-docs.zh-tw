---
title: "監視記憶體最佳化的系統版本設定時態表 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7a06785d-dbcb-44de-b95c-26b131471bee
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9a998ba89645d568585d475b50037adaab72657c
ms.lasthandoff: 04/11/2017

---
# <a name="monitoring-memory-optimized-system-versioned-temporal-tables"></a>監視記憶體最佳化的系統建立版本時態表
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對每個系統建立版本的記憶體最佳化資料表，您可以使用現有的檢視來追蹤其詳細和摘要記憶體耗用量。  
  
 詳細的記憶體耗用量 (依據每個主要的系統建立版本和內部歷程記錄暫存表格分割)：  
  
```  
--Details of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
      , T1.object_id AS TemporalTableObjectId  
      , IT.object_id AS InternalTableObjectId  
      , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
      , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
  
SELECT   
     TemporalTableSchema  
   , T.TemporalTableName  
   , T.InternalHistoryStagingName,    
     CASE   
        WHEN C.object_id = T.TemporalTableObjectId   
        THEN 'Temporal Table Consumption'   
         ELSE 'Internal Table Consumption'   
         END ConsumedBy  
     , C.*   
   FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
   WHERE T.TemporalTableSchema = 'dbo' AND  T.TemporalTableName = 'FXCurrencyPairs' ;  
  
```  
  
 記憶體耗用量的摘要 (系統建立版本的記憶體最佳化資料表累加值)︰  
  
```  
--Summary of memory consumption   
WITH InMemoryTemporalTables   
AS   
(   
   SELECT SCHEMA_NAME ( T1.schema_id ) AS TemporalTableSchema  
     , T1.object_id AS TemporalTableObjectId  
     , IT.object_id AS InternalTableObjectId  
     , OBJECT_NAME ( IT.parent_object_id ) AS TemporalTableName  
     , IT.Name AS InternalHistoryStagingName   
   FROM sys.internal_tables IT    
   JOIN sys.tables T1 ON IT.parent_object_id = T1.object_id   
   WHERE T1.is_memory_optimized  = 1 AND T1.temporal_type = 2    
)   
, DetailedConsumption   
AS   
(   
   SELECT TemporalTableSchema  
      , T.TemporalTableName  
      , T.InternalHistoryStagingName  
      , CASE   
           WHEN C.object_id = T.TemporalTableObjectId   
           THEN 'Temporal Table Consumption'   
           ELSE 'Internal Table Consumption'   
           END ConsumedBy  
      , C.*   
    FROM sys.dm_db_xtp_memory_consumers C   
   JOIN InMemoryTemporalTables T   
      ON C.object_id = T.TemporalTableObjectId OR C.object_id = T.InternalTableObjectId   
)   
  
SELECT TemporalTableSchema  
     TemporalTableName  
   , sum ( allocated_bytes ) AS allocated_bytes  
   , sum ( used_bytes ) AS used_bytes   
FROM DetailedConsumption   
WHERE TemporalTableSchema = 'dbo' AND  TemporalTableName = 'FXCurrencyPairs'   
GROUP BY TemporalTableSchema, TemporalTableName ;  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請將您的意見傳送到 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Monitoring%20Memory-Optimized%20System-Versioned%20Temporal%20Tables%20page)  
  
## <a name="see-also"></a>另請參閱  
 [系統版本設定時態表與記憶體最佳化資料表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [建立記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/creating-a-memory-optimized-system-versioned-temporal-table.md)   
 [使用記憶體最佳化的系統版本設定時態表](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)   
 [記憶體最佳化系統版本設定時態表的效能考量](../../relational-databases/tables/memory-optimized-system-versioned-temporal-tables-performance.md)   
 [時態表](../../relational-databases/tables/temporal-tables.md)   
 [時態表系統一致性檢查](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [管理系統設定版本之時態表中的歷程記錄資料保留](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [暫存資料表中繼資料檢視和函數](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  

