---
title: 使用擴充事件監視系統活動 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e44cb9ed2c5009dffce1373c57d512b8e578d025
ms.sourcegitcommit: 715683b5fc7a8e28a86be8949a194226b72ac915
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/26/2019
ms.locfileid: "58478123"
---
# <a name="monitor-system-activity-using-extended-events"></a>使用擴充事件監視系統活動

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  此程序說明如何搭配 Windows 事件追蹤 (ETW) 來使用擴充的事件，以監視系統活動。 此程序也會示範如何使用 CREATE EVENT SESSION、ALTER EVENT SESSION 和 DROP EVENT SESSION 陳述式。  
  
 完成這些工作需要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中使用查詢編輯器來進行以下程序。 此程序也需要使用命令提示字元來執行 ETW 命令。  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>使用擴充的事件監視系統活動  
  
1.  在查詢編輯器中，發出下列陳述式來建立事件工作階段及加入兩個事件。 這些 checkpoint_begin 和 checkpoint_end 事件會在資料庫中斷點的開頭和結尾引發。  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  加入具有 32 個值區的值區目標，以根據資料庫識別碼計算中斷點的數目。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  發出下列陳述式來加入 ETW 目標， 如此將可讓您看到開頭和結束事件，這可用來判斷中斷點所花的時間長度。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  發出下列陳述式，以啟動工作階段及開始事件收集。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  發出下列陳述式來引發三個事件。  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  發出下列陳述式來檢視事件計數。  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  在命令提示字元下，發出下列命令來檢視 ETW 資料。  
  
    > [!NOTE]  
    >  若要取得 **tracerpt** 命令的說明，請在命令提示字元上輸入 `tracerpt /?`。  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  發出下列陳述式，以停止事件工作階段，並從伺服器中將它移除。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [擴充的事件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [擴充的事件動態管理檢視](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [SQL Server 擴充的事件目標](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)  
  
  
