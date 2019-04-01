---
title: 尋找持有最多鎖定的物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- objects [SQL Server], extended events
- xe
- extended events [SQL Server], locks
- objects [SQL Server], locks
ms.assetid: fcbadbda-c91c-43f0-a1b5-601e40110e07
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 038fb2ba6760f01f0a762b3436bb82ba8117ff4f
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478093"
---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>尋找持有最多鎖定的物件

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  資料庫管理員經常需要識別阻礙資料庫效能的鎖定來源。  
  
 例如，您正在監視實際伺服器，以找出任何可能的瓶頸。 您懷疑可能有高度爭用的資源，而且想要了解這些物件所持有的鎖定數量。 一旦識別出最常鎖定的物件之後，就可以採取步驟來最佳化爭用物件的存取。  
  
 若要這樣做，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用查詢編輯器。  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>尋找持有最多鎖定的物件  
  
1.  在查詢編輯器中，發出下列陳述式。  
  
    ```  
    -- Find objects in a particular database that have the most  
    -- lock acquired. This sample uses AdventureWorksDW2012.  
    -- Create the session and add an event and target.  
    --   
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')  
    DROP EVENT session LockCounts ON SERVER  
    GO  
    DECLARE @dbid int  
  
    SELECT @dbid = db_id('AdventureWorksDW2012')  
  
    DECLARE @sql nvarchar(1024)  
    SET @sql = '  
    CREATE event session LockCounts ON SERVER  
    ADD EVENT sqlserver.lock_acquired (WHERE database_id =' + CAST(@dbid AS nvarchar) +')  
    ADD TARGET package0.histogram(   
    SET filtering_event_name=''sqlserver.lock_acquired'', source_type=0, source=''resource_0'')'  
  
    EXEC (@sql)  
    GO  
    ALTER EVENT session LockCounts ON SERVER   
    STATE=start  
    GO  
    --   
    -- Create a simple workload that takes locks.  
    --   
    USE AdventureWorksDW2012  
    GO  
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems  
    GO  
    -- The histogram target output is available from the   
    -- sys.dm_xe_session_targets dynamic management view in  
    -- XML format.  
    -- The following query joins the bucketizing target output with  
    -- sys.objects to obtain the object names.  
    --  
    SELECT name, object_id, lock_count FROM   
    (SELECT objstats.value('.','bigint') AS lobject_id,   
    objstats.value('@count', 'bigint') AS lock_count  
    FROM (  
    SELECT CAST(xest.target_data AS XML)  
    LockData  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'  
    ) Locks  
    CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)  
     ) LockedObjects   
    INNER JOIN sys.objects o  
    ON LockedObjects.lobject_id = o.object_id  
    WHERE o.type != 'S' AND o.type = 'U'  
    ORDER BY lock_count desc  
    GO  
    --   
    -- Stop the event session.  
    --   
    ALTER EVENT SESSION LockCounts ON SERVER  
    state=stop  
    GO  
  
    ```  
  
 當此程序中的陳述式完成之後，查詢編輯器的 **[結果]** 索引標籤會顯示以下資料行：  
  
-   NAME  
  
-   object_id  
  
-   lock_count  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  
