---
title: "建立使用一般 T-SQL 查詢收集器型別的自訂收集組 (Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "T-SQL 查詢收集器類型"
  - "收集組 [SQL Server], 建立自訂"
ms.assetid: 6b06db5b-cfdc-4ce0-addd-ec643460605b
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# 建立使用一般 T-SQL 查詢收集器型別的自訂收集組 (Transact-SQL)
  您可以使用資料收集器所提供的預存程序，建立包含使用一般 T-SQL 查詢收集器型別之收集項的自訂收集組。 完成這項工作需要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來進行以下程序：  
  
-   設定上傳排程。  
  
-   定義和建立收集組。  
  
-   定義和建立收集項。  
  
-   確認收集組與收集項確實存在。  
  
> [!NOTE]  
>  在您建立自訂收集組之前，必須先設定資料收集參數。 如需詳細資訊，請參閱[設定資料收集參數 &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)。  
  
### 定義和建立收集組  
  
1.  使用 sp_syscollector_create_collection_set 預存程序來定義新的收集組。  
  
    ```  
    USE msdb;  
    DECLARE @collection_set_id int;  
    DECLARE @collection_set_uid uniqueidentifier;  
    EXEC sp_syscollector_create_collection_set   
        @name=N'DMV Test 1',   
        @collection_mode=0,   
        @description=N'This is a test collection set',   
        @logging_level=1,   
        @days_until_expiration=14,   
        @schedule_name=N'CollectorSchedule_Every_15min',   
        @collection_set_id=@collection_set_id OUTPUT,   
        @collection_set_uid=@collection_set_uid OUTPUT;  
    SELECT @collection_set_id, @collection_set_uid;  
    ```  
  
     收集模式可以設定為 0 (快取) 或 1 (非快取)。  
  
     記錄層級可以設定為 0、1 或 2。  
  
     下面是資料收集器所提供的預先設定排程：  
  
    -   CollectorSchedule_Every_5min  
  
    -   CollectorSchedule_Every_10min  
  
    -   CollectorSchedule_Every_15min  
  
    -   CollectorSchedule_Every_30min  
  
    -   CollectorSchedule_Every_60min  
  
    -   CollectorSchedule_Every_6h  
  
     如果您不想要使用所提供的其中一個排程，可以建立新的排程，然後將它用於收集組。 如需詳細資訊，請參閱[建立及附加排程至作業](../../ssms/agent/create-and-attach-schedules-to-jobs.md)。  
  
### 定義和建立收集項  
  
1.  因為新的收集項是以已經安裝的一般收集器型別為基礎，所以您可以執行下列程式碼，將 GUID 設定為對應至一般 T-SQL 查詢收集器型別。  
  
    ```tsql  
    DECLARE @collector_type_uid uniqueidentifier;  
    SELECT @collector_type_uid = collector_type_uid FROM [msdb].[dbo].[syscollector_collector_types]   
    WHERE name = N'Generic T-SQL Query Collector Type';  
    DECLARE @collection_item_id int;  
    ```  
  
2.  使用 sp_syscollector_create_collection_item 預存程序來建立收集項。 宣告收集項的結構描述，好讓它對應到一般 T-SQL 查詢收集器型別所需的結構描述。  
  
    ```tsql  
    EXEC sp_syscollector_create_collection_item   
        @name=N'Query Stats - Test 1',   
        @parameters=N'  
            <ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
            <Value>SELECT * FROM sys.dm_exec_query_stats</Value>  
            <OutputTable>dm_exec_query_stats</OutputTable>  
            </Query>  
            </ns:TSQLQueryCollector>',   
        @collection_item_id=@collection_item_id OUTPUT,   
        @frequency=5,   
        @collection_set_id=@collection_set_id,   
        @collector_type_uid=@collector_type_uid;  
    SELECT @collection_item_id;  
    ```  
  
### 確認新的收集組與收集項確實存在  
  
1.  在啟動新的收集組之前，請執行下列查詢來確認新的收集組和它的收集項確實已經建立。  
  
    ```tsql  
    USE msdb;  
    SELECT * FROM syscollector_collection_sets;  
    SELECT * FROM syscollector_collection_items;  
    GO  
    ```  
  
     您也可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中進行目視檢查。 在物件總管中，展開 [管理] 節點，然後展開 [資料收集]。 將會顯示新的收集組。 收集組的紅色圓圈圖示是表示此收集組已經停止。  
  
## 範例  
 下列程式碼範例會結合上述步驟所列的範例。 請注意，這時針對收集項所設定的收集頻率 (5 秒) 將會遭到忽略，因為收集組的收集模式設定為 0，而這是快取模式。 如需相關資訊，請參閱 [Data Collection](../../relational-databases/data-collection/data-collection.md)。  
  
```tsql  
USE msdb;  
  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier  
  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'DMV Stats Test 1',  
    @collection_mode = 0,  
    @description = N'This is a test collection set',  
    @logging_level=1,  
    @days_until_expiration = 14,  
    @schedule_name=N'CollectorSchedule_Every_15min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
SELECT @collection_set_id,@collection_set_uid;  
  
DECLARE @collector_type_uid uniqueidentifier;  
SELECT @collector_type_uid = collector_type_uid FROM syscollector_collector_types   
WHERE name = N'Generic T-SQL Query Collector Type';  
  
DECLARE @collection_item_id int;  
EXEC sp_syscollector_create_collection_item  
@name= N'Query Stats - Test 1',  
@parameters=N'  
<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
<Query>  
  <Value>select * from sys.dm_exec_query_stats</Value>  
  <OutputTable>dm_exec_query_stats</OutputTable>  
</Query>  
 </ns:TSQLQueryCollector>',  
    @collection_item_id = @collection_item_id OUTPUT,  
    @frequency = 5, -- This parameter is ignored in cached mode  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid;  
SELECT @collection_item_id;  
  
GO  
```  
  
## 另請參閱  
 [資料收集器預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理排程](../../ssms/agent/manage-schedules.md)   
 [啟動或停止收集組](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
  