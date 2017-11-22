---
title: "SQL Server 中的擴充事件目標 | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47c64144-4432-4778-93b5-00496749665b
caps.latest.revision: "2"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de12dd7f28eb427429ecc0260ce37707ff0cec99
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="targets-for-extended-events-in-sql-server"></a>SQL Server 中的擴充事件目標
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


本文說明何時及如何將 package0 目標用於 SQL Server 中的擴充事件。 針對每個目標，現有文章說明︰

- 它收集和報告事件所傳送資料的能力。
- 它的參數 (其一目了然的參數除外)。


#### <a name="xquery-example"></a>XQuery 範例


[ring_buffer](#h2_target_ring_buffer) 一節包含 [在 Transact-SQL 中使用 XQuery](../../xquery/xquery-language-reference-sql-server.md) 將 XML 的字串複製至關聯式資料列集的範例。


### <a name="prerequisites"></a>必要條件


- 請熟悉擴充事件基本概念 (如 [快速入門︰SQL Server 中的擴充事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)中所述)。


- 已安裝最新版本的經常更新公用程式 SQL Server Management Studio (SSMS.exe)。 如需詳細資料，請參閱：
    - [下載 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)


- 在 SSMS.exe 中，了解如何使用物件總管以滑鼠右鍵按一下事件工作階段下的目標節點，[輕鬆檢視輸出資料](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)。
    - 事件資料會被擷取成 XML 字串。 但在本文中，資料會顯示在關聯式資料列中。 SSMS 是用來檢視資料，然後將其複製並貼入本文中。
    - [ring_buffer](#h2_target_ring_buffer)一節說明從 XML 產生資料列集的替代 T-SQL 技巧。 它包含 XQuery。



## <a name="parameters-actions-and-fields"></a>參數、動作和欄位


在 Transact-SQL 中， [CREATE EVENT SESSION](~/t-sql/statements/create-event-session-transact-sql.md) 陳述式是擴充事件的重要部分。 若要撰寫陳述式，您通常需要下列項目的清單和說明︰

- 與所選擇事件相關聯的欄位。
- 與所選擇目標相關聯的參數。

在下文的 C 一節中可以複製從系統檢視表傳回這類清單的 SELECT 陳述式：

- [SQL Server 擴充事件系統檢視表中的 SELECT 和 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md)
    - [C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) 事件的 SELECT 欄位。
    - [C.6](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_6_parameters_targets) 目標的 SELECT 參數。
    - [C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT 動作。


您可以在 [這個連結](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_B_2_TSQL_perspective)看到實際 CREATE EVENT SESSION 陳述式的內容中所使用的參數、欄位和動作。



<a name="h2_target_etw_classic_sync_target"></a>

## <a name="etwclassicsynctarget-target"></a>etw_classic_sync_target 目標


SQL Server 擴充事件可以與 Windows 事件追蹤 (ETW) 搭配運作，以監視系統活動。 如需詳細資訊，請參閱：

- [Windows 事件追蹤目標](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)


這個 ETW 目標會「同步」處理所接收到的資料，大部分的目標則會「非同步」處理所接收到的資料。


<a name="h2_target_event_counter"></a>

## <a name="eventcounter-target"></a>event_counter 目標


event_counter 目標只會計算每個所指定事件的發生次數。


與大部分的其他目標不同︰

- event_counter 沒有任何參數。


- 與大部分的目標不同，event_counter 目標會「同步」處理所接收到的資料。
    - 因為 event_counter 所需的處理很少，所以簡單 event_counter 接受同步處理。
    - 資料庫引擎會中斷任何速度太慢的目標，以及因而讓資料庫引擎效能變慢的目標。 這是大多數目標進行「非同步」處理的其中一個原因。


#### <a name="example-output-captured-by-eventcounter"></a>event_counter 所擷取的範例輸出


```
package_name   event_name         count
------------   ----------         -----
sqlserver      checkpoint_begin   4
```


接下來是導致先前結果的 CREATE EVENT SESSION。 針對這個測試，在 EVENT...WHERE 子句上，使用 **package0.counter** 欄位在計數到達 4 之後停止計算。


```tsql
CREATE EVENT SESSION [event_counter_1]
    ON SERVER 
    ADD EVENT sqlserver.checkpoint_begin   -- Test by issuing CHECKPOINT; statements.
    (
        WHERE ([package0].[counter] <= (4))   -- A predicate filter.
    )
    ADD TARGET package0.event_counter
    WITH
    (
        MAX_MEMORY = 4096 KB,
        MAX_DISPATCH_LATENCY = 3 SECONDS
    );
```



<a name="h2_target_event_file"></a>

## <a name="eventfile-target"></a>event_file 目標


**event_file** 目標會將事件工作階段輸出從緩衝區寫入至磁碟檔案︰


- 您可以在 ADD TARGET 子句上指定 *filename=* 參數。
    - **.xel** 必須是檔案的副檔名。


- 系統會使用您選擇的檔案名稱作為附加日期時間型 long 整數的前置詞，並且後接 .xel 副檔名。


#### <a name="create-event-session-with-eventfile-target"></a>含 **event_file** 目標的 CREATE EVENT SESSION


接下來是用來進行測試的 CREATE EVENT SESSION。 其中一個 ADD TARGET 子句指定 event_file。


```tsql
CREATE EVENT SESSION [locks_acq_rel_eventfile_22]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION (sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name=(1),
            collect_resource_description=(1)

        ACTION(sqlserver.sql_text,sqlserver.transaction_id)

        WHERE
        (
            [database_name]=N'InMemTest2'
            AND
            [object_id]=(370100359)
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.event_file
    (
        SET     filename=N'C:\Junk\locks_acq_rel_eventfile_22-.xel'
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=10 SECONDS
    );
```


#### <a name="sysfnxefiletargetreadfile-function"></a>sys.fn_xe_file_target_read_file 函數


event_file 目標會將接收到的資料儲存為人類無法讀取的二進位格式。 Transact-SQL 可以從 [**sys.fn_xe_file_target_read_file**](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md) 函數進行選取，以報告 .xel 檔案的內容。


針對 SQL Server **2016** 和更新版本，下列 T-SQL SELECT 已報告資料。 下者中的 *.xel 尾碼 


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            null, null, null)  AS f;
```


針對 SQL Server **2014**，與下列類似的 SELECT 將會報告資料。 在 SQL Server 2014 之後，不再使用 .xem 檔案。


```
SELECT f.*
        --,CAST(f.event_data AS XML)  AS [Event-Data-Cast-To-XML]  -- Optional
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\junk\locks_acq_rel_eventfile_22-*.xel',
            'C:\junk\metafile.xem',
            null, null)  AS f;
```


當然，您也可以手動使用 SSMS UI 來查看 .xel 資料：


#### <a name="data-stored-in-the-eventfile-target"></a>event_file 目標中所儲存的資料


接下來是 SQL Server 2016 中從 **sys.fn_xe_file_target_read_file**中進行選取的報表。


```
module_guid                            package_guid                           object_name     event_data                                                                                                                                                                                                                                                                                          file_name                                                      file_offset
-----------                            ------------                           -----------     ----------                                                                                                                                                                                                                                                                                          ---------                                                      -----------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_acquired   <event name="lock_acquired" package="sqlserver" timestamp="2016-08-07T20:13:35.827Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   lock_released   <event name="lock_released" package="sqlserver" timestamp="2016-08-07T20:13:35.832Z"><action name="transaction_id" package="sqlserver"><value>39194</value></action><action name="sql_text" package="sqlserver"><value><![CDATA[  select top 1 * from dbo.T_Target;  ]]></value></action></event>   C:\junk\locks_acq_rel_eventfile_22-_0_131150744126230000.xel   11776
```



<a name="h2_target_histogram"></a>

## <a name="histogram-target"></a>histogram 目標


**histogram** 目標比 event_counter 目標更為適合。 histogram 可以執行下列動作：

- 個別計算數個項目的出現次數。
- 計算不同類型之項目的出現次數：
    - 事件欄位。
    - 動作。


**source_type** 參數是控制 histogram 目標的重要項目：

- **source_type=0** - 表示收集「事件欄位」的資料。
- **source_type=1** - 表示收集「動作」的資料。
    - 預設值為 1。


'slots' 參數預設值為 256。 如果您指派另一個值，值會四捨五入至下一個 2 的次方。

- 例如，slots=59 會四捨五入為 =64。


### <a name="action-example-for-histogram"></a>histogram 的「動作」範例


在其 TARGET...SET 子句上，下列 Transact-SQL CREATE EVENT SESSION 陳述式指定 **source_type=1** 的目標參數指派。 1 表示 histogram 目標會追蹤動作。

在目前的範例中，EVENT...ACTION 子句只會提供一個動作供目標進行選擇，名為 **sqlos.system_thread_id**。 在 TARGET...SET 子句上，會看到 **source=N'sqlos.system_thread_id'** 指派。

- 若要追蹤多個來源動作，您可以將第二個 histogram 目標新增至 CREATE EVENT SESSION 陳述式。


```tsql
CREATE EVENT SESSION [histogram_lockacquired]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
        (
        ACTION
            (
            sqlos.system_thread_id
            )
        )
    ADD TARGET package0.histogram
        (
        SET
            filtering_event_name=N'sqlserver.lock_acquired',
            slots=(16),
            source=N'sqlos.system_thread_id',
            source_type=1
        )
    WITH
        (
        <.... (For brevity, numerous parameter assignments generated by SSMS.exe are not shown here.) ....>
        );
```


 下列是所擷取的資料。 **value** 資料行下的值是 system_thread_id 值。 例如，在執行緒 6540 下已取得共 236 個鎖定。


```
value   count
-----   -----
 6540     236
 9308      91
 9668      74
10144      49
 5244      44
 2396      28
```


#### <a name="select-to-discover-available-actions"></a>SELECT 以探索可用的動作


[C.3](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_3_select_all_available_objects) SELECT 陳述式可以找到系統可讓您在 CREATE EVENT SESSION 陳述式上指定的動作。 在 WHERE 子句中，您可以先編輯 **o.name LIKE** 篩選，以符合感興趣的動作。


接下來是 C.3 SELECT 所傳回的範例資料列集。 在第二個資料列中會看到 **system_thread_id** 動作。


```
Package-Name   Action-Name                 Action-Description
------------   -----------                 ------------------
package0       collect_current_thread_id   Collect the current Windows thread ID
sqlos          system_thread_id            Collect current system thread ID
sqlserver      create_dump_all_threads     Create mini dump including all threads
sqlserver      create_dump_single_thread   Create mini dump for the current thread
```


### <a name="event-field-example-for-histogram"></a>histogram 的事件「欄位」範例


下列範例會設定 **source_type=0**。 指派給 **source=** 的值是事件欄位 (不是動作)。



```tsql
CREATE EVENT SESSION [histogram_checkpoint_dbid]
    ON SERVER 
    ADD EVENT  sqlserver.checkpoint_begin
    ADD TARGET package0.histogram
    (
    SET
        filtering_event_name = N'sqlserver.checkpoint_begin',
        source               = N'database_id',
        source_type          = (0)
    )
    WITH
    ( <....> );
```


下列是 histogram 目標所擷取的資料。 資料顯示 ID=5 的資料庫遇到 7 個 checkpoint_begin 事件。


```
value   count
-----   -----
5       7
7       4
6       3
```


#### <a name="select-to-discover-available-fields-on-your-chosen-event"></a>SELECT 以探索所選擇事件上的可用欄位


[C.4](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields) SELECT 陳述式會顯示您可以從中進行選擇的事件欄位。 您會先將 **o.name LIKE** 篩選編輯成所選擇的事件名稱。


下列是 C.4 SELECT 所傳回的資料列集。 資料列集顯示 database_id 是可提供 histogram 目標值之 checkpoint_begin 事件上的唯一欄位。


```
Package-Name   Event-Name         Field-Name   Field-Description
------------   ----------         ----------   -----------------
sqlserver      checkpoint_begin   database_id  NULL
sqlserver      checkpoint_end     database_id  NULL
```


<a name="h2_target_pair_matching"></a>

## <a name="pairmatching-target"></a>pair_matching 目標


pair_matching 目標可讓您偵測沒有對應結束事件的開始事件。 例如，如果發生 lock_acquired 事件，但後面沒有及時跟著相符的 lock_released 事件，則可能會發生問題。


系統不會自動比對開始和結束事件。 相反地，您會說明 CREATE EVENT SESSION 陳述式中系統的比對。 比對開始和結束事件時，會捨棄這組配對，讓每個人都可以專注於不成對的開始事件。


#### <a name="finding-matchable-fields-for-the-start-and-end-event-pair"></a>尋找開始和結束事件配對的可相符欄位


透過使用 [C.4 SELECT](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md#section_C_4_data_fields)，會在下列資料列集中看到 lock_acquired 事件大約有 16 個欄位。 這裡顯示的資料列集已手動進行分割，可顯示與我們的範例相符的欄位。 某些欄位會愚蠢地嘗試進行比對，例如兩個事件的 **duration** 。


```
Package-Name   Event-Name   Field-Name               Field-Description
------------   ----------   ----------               -----------------
sqlserver   lock_acquired   database_name            NULL
sqlserver   lock_acquired   mode                     NULL
sqlserver   lock_acquired   resource_0               The ID of the locked object, when lock_resource_type is OBJECT.
sqlserver   lock_acquired   resource_1               NULL
sqlserver   lock_acquired   resource_2               The ID of the lock partition, when lock_resource_type is OBJECT, and resource_1 is 0.
sqlserver   lock_acquired   transaction_id           NULL

sqlserver   lock_acquired   associated_object_id     The ID of the object that requested the lock that was acquired.
sqlserver   lock_acquired   database_id              NULL
sqlserver   lock_acquired   duration                 The time (in microseconds) between when the lock was requested and when it was canceled.
sqlserver   lock_acquired   lockspace_nest_id        NULL
sqlserver   lock_acquired   lockspace_sub_id         NULL
sqlserver   lock_acquired   lockspace_workspace_id   NULL
sqlserver   lock_acquired   object_id                The ID of the locked object, when lock_resource_type is OBJECT. For other lock resource types it will be 0
sqlserver   lock_acquired   owner_type               NULL
sqlserver   lock_acquired   resource_description     The description of the lock resource. The description depends on the type of lock. This is the same value as the resource_description column in the sys.dm_tran_locks view.
sqlserver   lock_acquired   resource_type            NULL
```


### <a name="example-of-pairmatching"></a>pair_matching 範例


下列 CREATE EVENT SESSION 陳述式指定兩個事件和兩個目標。 pair_matching 目標指定兩組欄位，以讓這些事件成對。 指派給 **begin_matching_columns=** 和 **end_matching_columns=** 的一串逗號分隔欄位必須相同。 雖然可以使用空格，但是逗號分隔值中所提及的欄位之間不允許定位字元或換行字元。

為了縮小結果範圍，我們會先從 sys.objects 進行 SELECT，以尋找測試資料表的 object_id。 我們已將該識別碼的篩選新增至 EVENT...WHERE 子句。


```tsql
CREATE EVENT SESSION [pair_matching_lock_a_r_33]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    ),
    ADD EVENT sqlserver.lock_released
    (
        SET
            collect_database_name = (1),
            collect_resource_description = (1)

        ACTION (sqlserver.transaction_id)

        WHERE
        (
            [database_name] = 'InMemTest2'
            AND
            [object_id] = 370100359
        )
    )
    ADD TARGET package0.event_counter,
    ADD TARGET package0.pair_matching
    (
        SET
            begin_event = N'sqlserver.lock_acquired',
            begin_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            end_event = N'sqlserver.lock_released',
            end_matching_columns =
                N'resource_0, resource_1, resource_2, transaction_id, database_id',

            respond_to_memory_pressure = (1)
    )
    WITH
    (
        MAX_MEMORY = 8192 KB,
        MAX_DISPATCH_LATENCY = 15 SECONDS
    );
```


為了測試事件工作階段，我們刻意避免釋出所取得的鎖定。 做法是使用下列 T-SQL 步驟︰

1. BEGIN TRANSACTION。
2. UPDATE MyTable....
3. 除非在檢查目標之後，否則會刻意不發出 COMMIT TRANSACTION。
4. 稍後，在測試之後，我們已發出 COMMIT TRANSACTION。


簡單 **event_counter** 目標提供下列輸出資料列。 因為 52-50=2，所以檢查成對目標的輸出時，輸出告訴我們應該會看到 2 個不成對的 lock_acquired 事件。


```
package_name   event_name      count
------------   ----------      -----
sqlserver      lock_acquired   52
sqlserver      lock_released   50
```


**pair_matching** 目標提供下列輸出。 如 event_counter 輸出所建議，我們的確會看到 2 個 lock_acquired 資料列。 我們看到這些資料列表示這兩個 lock_acquired 事件未成對。


```
package_name   event_name      timestamp                     database_name   duration   mode   object_id   owner_type   resource_0   resource_1   resource_2   resource_description   resource_type   transaction_id
------------   ----------      ---------                     -------------   --------   ----   ---------   ----------   ----------   ----------   ----------   --------------------   -------------   --------------
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          S      370100359   Transaction  370100359    3            0            [INDEX_OPERATION]      OBJECT          34126
sqlserver      lock_acquired   2016-08-05 12:45:47.9980000   InMemTest2      0          IX     370100359   Transaction  370100359    0            0                                   OBJECT          34126
```


未成對 lock_acquired 事件的資料列可能包括 T-SQL 文字或具有鎖定的 **sqlserver.sql_text**。 但是，我們不想讓顯示過於膨脹。


<a name="h2_target_ring_buffer"></a>

## <a name="ringbuffer-target"></a>ring_buffer 目標


ring_buffer 目標方便進行快速和簡單事件測試。 當您停止事件工作階段時，會捨棄預存的輸出。

在 ring_buffer 這一節中，也會示範如何使用 XQuery 的 Transact-SQL 實作將 ring_buffer 的 XML 內容複製至更容易讀取的關聯式資料列集中。


#### <a name="create-event-session-with-ringbuffer"></a>含 ring_buffer 的 CREATE EVENT SESSION


使用 ring_buffer 目標的這個 CREATE EVENT SESSION 陳述式沒有特別需要注意的部分。


```tsql
CREATE EVENT SESSION [ring_buffer_lock_acquired_4]
    ON SERVER 
    ADD EVENT sqlserver.lock_acquired
    (
        SET collect_resource_description=(1)

        ACTION(sqlserver.database_name)

        WHERE
        (
            [object_id]=(370100359)  -- ID of MyTable
            AND
            sqlserver.database_name='InMemTest2'
        )
    )
    ADD TARGET package0.ring_buffer
    (
        SET max_events_limit=(98)
    )
    WITH
    (
        MAX_MEMORY=4096 KB,
        MAX_DISPATCH_LATENCY=3 SECONDS
    );
```


### <a name="xml-output-received-for-lockacquired-by-ringbuffer"></a>ring_buffer 針對 lock_acquired 所接收到的 XML 輸出


透過 SELECT 陳述式擷取時，內容的格式為 XML 字串。 在測試中，ring_buffer 目標所儲存的 XML 字串顯示如下。 不過，基於下列 XML 顯示的簡潔性，已清除所有項目，但不含 &#x3c;event&#x3e; 這兩個元素。 此外，在每個 &#x3c;event&#x3e; 內，已刪除少數無關的 &#x3c;data&#x3e; 元素。


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="6" eventCount="6" droppedCount="0" memoryUsed="1032">
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:53.987Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111030</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
  <event name="lock_acquired" package="sqlserver" timestamp="2016-08-05T23:59:56.012Z">
    <data name="mode">
      <type name="lock_mode" package="sqlserver"></type>
      <value>1</value>
      <text><![CDATA[SCH_S]]></text>
    </data>
    <data name="transaction_id">
      <type name="int64" package="package0"></type>
      <value>111039</value>
    </data>
    <data name="database_id">
      <type name="uint32" package="package0"></type>
      <value>5</value>
    </data>
    <data name="resource_0">
      <type name="uint32" package="package0"></type>
      <value>370100359</value>
    </data>
    <data name="resource_1">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="resource_2">
      <type name="uint32" package="package0"></type>
      <value>0</value>
    </data>
    <data name="database_name">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[]]></value>
    </data>
    <action name="database_name" package="sqlserver">
      <type name="unicode_string" package="package0"></type>
      <value><![CDATA[InMemTest2]]></value>
    </action>
  </event>
</RingBufferTarget>
```


若要查看前一個 XML，您可以在事件工作階段作用時發出下列 SELECT。 作用中 XML 資料是擷取自系統檢視表 **sys.dm_xe_session_targets**。


```tsql
SELECT
        CAST(LocksAcquired.TargetXml AS XML)  AS RBufXml,
    INTO
        #XmlAsTable
    FROM
        (
        SELECT
                CAST(t.target_data AS XML)  AS TargetXml
            FROM
                     sys.dm_xe_session_targets  AS t
                JOIN sys.dm_xe_sessions         AS s

                    ON s.address = t.event_session_address
            WHERE
                t.target_name = 'ring_buffer'
                AND
                s.name        = 'ring_buffer_lock_acquired_4'
        )
            AS LocksAcquired;


SELECT * FROM #XmlAsTable;
```


### <a name="xquery-to-see-the-xml-as-a-rowset"></a>將 XML 當作資料列集查看的 XQuery


若要將前一個 XML 當作關聯式資料列集查看，請發出下列 T-SQL，以從前一個 SELECT 陳述式繼續。 加上註解的行說明 XQuery 的每次使用。


```tsql
SELECT
         -- (A)
         ObjectLocks.value('(@timestamp)[1]',
            'datetime'     )  AS [OccurredDtTm]

        -- (B)
        ,ObjectLocks.value('(data[@name="mode"]/text)[1]',
            'nvarchar(32)' )  AS [Mode]

        -- (C)
        ,ObjectLocks.value('(data[@name="transaction_id"]/value)[1]',
            'bigint' )  AS [TxnId]

        -- (D)
        ,ObjectLocks.value('(action[@name="database_name" and @package="sqlserver"]/value)[1]',
            'nvarchar(128)')  AS [DatabaseName]
    FROM
        #TableXmlCell
    CROSS APPLY
        -- (E)
        TargetDateAsXml.nodes('/RingBufferTarget/event[@name="lock_acquired"]')  AS T(ObjectLocks);
```


#### <a name="xquery-notes-from-preceding-select"></a>前一個 SELECT 的 XQuery 附註


(A)
- timestamp= 屬性的值，在 &#x3c;event&#x3e; 元素上。
- '(...)[1]' 建構確保每個反覆項目都只會傳回 1 個值，這是 XML 資料類型變數和資料行的 .value() XQuery 方法的必要限制。


(B)
- &#x3c;text&#x3e; 元素內部值，在其 name= 屬性等於 "mode" 的 &#x3c;data&#x3e; 元素內。


(C)
- &#x3c;value&#x3e; 元素內部值，在其 name= 屬性等於 "transaction_id" 的 &#x3c;data&#x3e; 元素內。


(D)
- &#x3c;event&#x3e; 包含 &#x3c;action&#x3e;。
- &#x3c;action&#x3e; 的 name= 屬性等於 "database_name"，而且 package= 屬性等於 "sqlserver" (非 "package0")，可取得 &#x3c;value&#x3e; 元素的內部值。


(E)
- C.A. 會針對其 name= 屬性等於 "lock_acquired" 的每個個別 &#x3c;event&#x3e; 元素，重複進行處理。
- 這適用於前一個 FROM 子句所傳回的 XML。


#### <a name="output-from-xquery-select"></a>XQuery SELECT 的輸出


接下來是前一個包含 XQuery 的 T-SQL 所產生的資料列集。


```
OccurredDtTm              Mode    DatabaseName
------------              ----    ------------
2016-08-05 23:59:53.987   SCH_S   InMemTest2
2016-08-05 23:59:56.013   SCH_S   InMemTest2
```



## <a name="xevent-net-namespaces-and-cx23"></a>XEvent .NET 命名空間和 C&#x23;


Package0 有兩個目標，但是不能用在 Transact-SQL 中：

- compressed_history
- event_stream


我們知道這兩個目標不能用於 T-SQL 的原因，是它們在 *sys.dm_xe_objects.capabilities* 資料行中的非 null 值不包括位元 0x1。


event_stream 目標可以用於 C# 這類語言所撰寫的 .NET 程式。 C# 和其他 .NET 開發人員可以透過 .NET Framework 類別 (例如在 Microsoft.SqlServer.XEvents.Linq 命名空間中) 存取事件資料流。

發生時， **25726** 錯誤表示填入資料速度比用戶端還要快的事件資料流可能會使用資料。 這會讓資料庫引擎中斷與事件資料流的連接，避免降低伺服器的效能。


### <a name="xevent-namespaces"></a>XEvent 命名空間


- [Microsoft.SqlServer.Management.XEvent 命名空間](https://msdn.microsoft.com/library/microsoft.sqlserver.management.xevent.aspx)

- [Microsoft.SqlServer.XEvent.Linq 命名空間](https://msdn.microsoft.com/library/microsoft.sqlserver.xevent.linq.aspx)



