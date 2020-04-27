---
title: 建立和測試分類使用者定義函式 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5118ebcb3da31b97859ca0b2b38e3ad552604990
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "68212000"
---
# <a name="create-and-test-a-classifier-user-defined-function"></a>建立和測試分類使用者定義函數
  本主題說明如何建立和測試分類使用者定義函數 (UDF)。 這些步驟將包含在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢編輯器中執行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 陳述式。  
  
 下列程序所示的範例會說明建立相當複雜之分類使用者定義函數的可能性。  
  
 在我們的範例中：  
  
-   建立資源集區 (pProductionProcessing) 和工作負載群組 (gProductionProcessing)，以便在指定的時間範圍內進行生產處理。  
  
-   建立資源集區 (pOffHoursProcessing) 和工作負載群組 (gOffHoursProcessing)，以便處理不符合生產處理需求的連接。  
  
-   在 master 中建立資料表 (TblClassificationTimeTable)，以便保存可以針對登入時間評估的開始和結束時間。 這份資料表必須建立在 master 中，因為資源管理員會使用分類函數的結構描述繫結。  
  
    > [!NOTE]  
    >  最佳作法是避免將龐大且經常更新的資料表儲存在 master 中。  
  
 分類函數會延長登入時間。 任何過度複雜的函數都可能會導致登入逾時或降低快速連接的速度。  
  
### <a name="to-create-the-classifier-user-defined-function"></a>建立分類使用者定義函數  
  
1.  建立並設定新的資源集區和工作負載群組。 將每個工作負載群組指派給適當的資源集區。  
  
    ```  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    )  
    GO  
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    )  
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    )  
    GO  
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing  
    GO  
    ```  
  
2.  更新記憶體中組態。  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
3.  建立資料表並定義生產處理時間範圍的開始和結束時間。  
  
    ```  
    USE master  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    )  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM')  
    go  
    ```  
  
4.  建立使用時間函數和值 (可針對查閱資料表中的時間評估) 的分類函數。 如需在分類函式使用中使用查閱資料表的詳細資訊，請參閱本主題中的＜在分類函式中使用查閱資料表的最佳做法＞。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了一組擴充的日期與時間資料類型和函數。 如需詳細資訊，請參閱[日期和時間資料類型與函數 &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)。  
  
    ```  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable  
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END  
    GO  
    ```  
  
5.  註冊此分類函數並更新記憶體中組態。  
  
    ```  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier)  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
### <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>確認資源集區、工作負載群組和分類使用者定義函數  
  
1.  使用下列查詢來取得資源集區和工作負載群組組態。  
  
    ```  
    USE master  
    SELECT * FROM sys.resource_governor_resource_pools  
    SELECT * FROM sys.resource_governor_workload_groups  
    GO  
    ```  
  
2.  使用下列查詢來確認分類函數存在而且已啟用。  
  
    ```  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration  
  
    ```  
  
3.  使用下列查詢來取得資源集區和工作負載群組的目前執行階段資料。  
  
    ```  
    SELECT * FROM sys.dm_resource_governor_resource_pools  
    SELECT * FROM sys.dm_resource_governor_workload_groups  
    GO  
    ```  
  
4.  使用下列查詢來了解每個群組中含有哪些工作階段。  
  
    ```  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
              FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
              ON g.group_id = s.group_id  
    ORDER BY g.name  
    GO  
    ```  
  
5.  使用下列查詢來了解每個群組中含有哪些要求。  
  
    ```  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
                ON g.group_id = r.group_id  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
6.  使用下列查詢來了解哪些要求正在分類中執行。  
  
    ```  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
               FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = s.group_id  
                     AND 'preconnect' = s.status  
    ORDER BY g.name  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = r.group_id  
                     AND 'preconnect' = r.status  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
### <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>在分類函數中使用查閱資料表的最佳做法  
  
1.  除非絕對必要，否則不要使用查閱資料表。 如果您需要使用查閱資料表，它可能以硬編碼的方式將本身寫入函數中；不過它需要與分類函數的複雜度和動態變更相互平衡。  
  
2.  限制針對查閱資料庫執行的 I/O。  
  
    1.  使用 TOP 1 只會傳回一個資料列。  
  
    2.  最小化資料表中的資料列數目。  
  
    3.  在單一頁面或是盡量少的頁面上顯示資料表的所有資料列。  
  
    4.  確認使用索引搜尋作業找到的資料列盡可能使用多個搜尋資料行。  
  
    5.  如果您考慮透過聯結使用多個資料表，則反正規化為單一資料表。  
  
3.  避免在查閱資料表上進行封鎖。  
  
    1.  使用 `NOLOCK` 提示避免鎖定，或是在函數中使用最大值 1000 毫秒的 `SET LOCK_TIMEOUT` 。  
  
    2.  資料表必須在 master 資料庫中 (master 資料庫是在用戶端電腦嘗試連線時，唯一保證可以復原的資料庫)。  
  
    3.  務必以結構描述完整限定資料庫名稱。 資料庫名稱並非必要，因為一定要是 master 資料庫。  
  
    4.  資料表上沒有觸發程序。  
  
    5.  如果您要更新資料表內容，則務必使用快照隔離等級交易避免寫入器封鎖讀取器。 請注意，使用 `NOLOCK` 提示也可以防止這種情況發生。  
  
    6.  如有可能，變更資料表內容時，請停用分類函數。  
  
        > [!WARNING]  
        >  以下是我們建議的最佳做法。 如果有問題導致無法遵循下列最佳做法，建議您連絡 Microsoft 支援部門，以便主動避免未來發生任何問題。  
  
## <a name="see-also"></a>另請參閱  
 [Resource Governor](resource-governor.md)   
 [啟用 Resource Governor](enable-resource-governor.md)   
 [Resource Governor 資源集區](resource-governor-resource-pool.md)   
 [Resource Governor 工作負載群組](resource-governor-workload-group.md)   
 [使用範本設定 Resource Governor](configure-resource-governor-using-a-template.md)   
 [View Resource Governor 屬性](view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-sql&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)   
 [建立資源集區 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [建立工作負載群組 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION &#40;Transact-sql&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
