---
title: 使用擴充事件尋找持有最多鎖定的物件
description: 本文說明如何尋找具有最多鎖定的物件。 資料庫管理員可能需要尋找鎖定最多的物件，以改善資料庫效能。
ms.date: 10/18/2019
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d173a174323beab2323fcba856be89062dc5e774
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79434025"
---
# <a name="find-the-objects-that-have-the-most-locks-taken-on-them"></a>尋找持有最多鎖定的物件

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

資料庫管理員經常需要識別阻礙資料庫效能的鎖定來源。  
  
例如，您正在監視實際伺服器，以找出任何可能的瓶頸。 您懷疑可能有高度爭用的資源，而且想要了解這些物件所持有的鎖定數量。 一旦識別出最常鎖定的物件之後，就可以採取步驟來最佳化爭用物件的存取。  
  
若要這樣做，請在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中使用查詢編輯器。  
  
### <a name="to-find-the-objects-that-have-the-most-locks"></a>尋找持有最多鎖定的物件  
  
1. 在查詢編輯器中，發出下列陳述式。

    ```sql
    -- Find objects in a particular database that have the most
    -- lock acquired. This sample uses AdventureWorksDW2012.
    -- Create the session and add an event and target.
    
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='LockCounts')
        DROP EVENT session LockCounts ON SERVER;
    GO
    DECLARE @dbid int;
  
    SELECT @dbid = db_id('AdventureWorksDW2012');
  
    DECLARE @sql nvarchar(1024);
    SET @sql = '
        CREATE event session LockCounts ON SERVER
            ADD EVENT sqlserver.lock_acquired (WHERE database_id ='
                + CAST(@dbid AS nvarchar) +')
            ADD TARGET package0.histogram(
                SET filtering_event_name=''sqlserver.lock_acquired'',
                    source_type=0, source=''resource_0'')';
  
    EXEC (@sql);
    GO
    ALTER EVENT session LockCounts ON SERVER
        STATE=start;
    GO
    -- Create a simple workload that takes locks.
    
    USE AdventureWorksDW2012;
    GO
    SELECT TOP 1 * FROM dbo.vAssocSeqLineItems;
    GO
    -- The histogram target output is available from the
    -- sys.dm_xe_session_targets dynamic management view in
    -- XML format.
    -- The following query joins the bucketizing target output with
    -- sys.objects to obtain the object names.
    
    SELECT name, object_id, lock_count
        FROM
        (
        SELECT objstats.value('.','bigint') AS lobject_id,
            objstats.value('@count', 'bigint') AS lock_count
            FROM (
                SELECT CAST(xest.target_data AS XML)
                    LockData
                FROM     sys.dm_xe_session_targets xest
                    JOIN sys.dm_xe_sessions        xes  ON xes.address = xest.event_session_address
                    JOIN sys.server_event_sessions ses  ON xes.name    = ses.name
                WHERE xest.target_name = 'histogram' AND xes.name = 'LockCounts'
                 ) Locks
            CROSS APPLY LockData.nodes('//HistogramTarget/Slot') AS T(objstats)
        ) LockedObjects
        INNER JOIN sys.objects o  ON LockedObjects.lobject_id = o.object_id
        WHERE o.type != 'S' AND o.type = 'U'
        ORDER BY lock_count desc;
    GO
    
    -- Stop the event session.
    
    ALTER EVENT SESSION LockCounts ON SERVER
        state=stop;
    GO
    ```

> [!NOTE]
> 上述的 Transact-SQL 程式碼範例會在 SQL Server 內部部署上執行，但極可能_無法在 Azure SQL Database 上執行。_ 直接涉及事件的範例核心部分，例如 `ADD EVENT sqlserver.lock_acquired` 也會在 Azure SQL Database 上工作。 但是初步項目 (例如 `sys.server_event_sessions`) 必須編輯至其 Azure SQL Database 對應項 (例如 `sys.database_event_sessions`)，才能執行範例。
> 如需 SQL Server 內部部署與 Azure SQL Database 之間次要差異的詳細資訊，請參閱下列文章：
> - [Azure SQL Database 中的擴充事件](/azure/sql-database/sql-database-xevent-db-diff-from-svr#transact-sql-differences)
> - [支援擴充事件的系統物件](xevents-references-system-objects.md)

當前述 Transact-SQL 指令碼中的陳述式完成後，查詢編輯器的 [結果]  索引標籤會顯示下列資料行：
  
- NAME
- object_id
- lock_count
  
## <a name="see-also"></a>另請參閱

[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)  
[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)  
[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)  
[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
