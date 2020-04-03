---
title: 擴充事件系統檢視表中的 SELECT 和 JOIN
description: SQL Server 和 Azure SQL Database 中有擴充事件的系統檢視表。 了解如何以不同的檢視方塊來表示事件工作階段資訊。
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: 04521d7f-588c-4259-abc2-1a2857eb05ec
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3245b4288871e4b92b783aad0f08ca1027b401a0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "79526753"
---
# <a name="selects-and-joins-from-system-views-for-extended-events-in-sql-server"></a>SQL Server 擴充事件系統檢視表中的 SELECT 和 JOIN

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


此文章說明 SQL Server 與 Azure SQL Database 中與擴充事件相關的兩組系統檢視表。 本文說明︰

- 如何「聯結」不同的系統檢視表。
- 如何從系統檢視表 SELECT 特定類型的資訊。
- 各種不同的技術檢視方塊如何表示相同事件的工作階段資訊，這可加強您對每種觀點的了解。


大部分的範例是針對 SQL Server 所寫。 但稍加編輯即可在 SQL Database 上執行。



## <a name="a-foundational-information"></a>A. 基本資訊


擴充事件有兩組系統檢視表︰


#### <a name="catalog-views"></a>目錄檢視：

- 這些檢視會儲存[建立事件工作階段](../../t-sql/statements/create-event-session-transact-sql.md)或 SSMS UI 對等項目所建立之每個事件工作階段「定義」  的相關資訊。 但是這些檢視卻不知道任一工作階段是否已開始執行。
    - 例如，如果 SSMS [物件總管]  未顯示任何定義的事件工作階段，從 *sys.server_event_session_targets* 檢視中 SELECT 就會傳回零個資料列。


- 名稱前置詞為：
    - *sys.server\_event\_session\** 是 SQL Server 上的名稱前置詞。
    - *sys.database\_event\_session\** 是 SQL Database 上的名稱前置詞。


#### <a name="dynamic-management-views-dmvs"></a>動態管理檢視 (DMV)：

- 儲存執行事件工作階段的「目前活動」  相關資訊。 但是這些 DMV 對工作階段定義卻知之甚少。
    - 即使所有的事件工作階段目前皆已停止，因為伺服器啟動時會將各種封裝載入到使用中的記憶體，所以從 *sys.dm_xe_packages* 檢視 SELECT 仍會傳回資料列。
    - 因為同樣的原因，*sys.dm_xe_objects* *sys.dm_xe_object_columns* 也會傳回資料列。


- 擴充事件 DMV 的名稱前置詞是︰
    - *sys.dm\_xe\_\** 是 SQL Server 上的名稱前置詞。
    - *sys.dm\_xe\_database\_\** 通常是 SQL Database 的名稱前置詞。


#### <a name="permissions"></a>權限：


若要從系統檢視表 SELECT，必須有下列權限︰

- Microsoft SQL Server 為 VIEW SERVER STATE。
- Azure SQL Database 為 VIEW DATABASE STATE。


<a name="section_B_catalog_views"></a>

## <a name="b-catalog-views"></a>B. 目錄檢視


本節會比對同一已定義事件工作階段的三種不同技術檢視方塊，並建立其關聯。 工作階段已定義並顯示在 SQL Server Management Studio (SSMS.exe) 的 [物件總管]  中，但此工作階段目前未執行。

最好每個月 [安裝最新的 SSMS 更新](https://msdn.microsoft.com/library/mt238290.aspx)，以避免發生意外的失敗。


擴充事件目錄檢視的相關參考文件位於 [擴充事件目錄檢視 (TRANSACT-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)。


&nbsp;



#### <a name="the-sequence-in-this-section-b"></a>節 B 的順序：


- [B.1 SSMS UI 檢視方塊](#section_B_1_SSMS_UI_perspective)
    - 使用 SSMS UI 建立事件工作階段的定義。 如逐步螢幕擷取畫面所示。


- [B.2 TRANSACT-SQL 檢視方塊](#section_B_2_TSQL_perspective)
    - 使用 SSMS 操作功能表進行已定義的事件工作階段的還原工程，還原為對等的 TRANSACT-SQL **CREATE EVENT SESSION** 陳述式。 T-SQL 會顯示 SSMS 螢幕擷取畫面選項的完全相符項目。


- [B.3 目錄檢視的 SELECT JOIN UNION 檢視方塊](#section_B_3_Catalog_view_S_J_UNION)
    - 從我們事件工作階段的系統目錄檢視發出 T-SQL SELECT 陳述式。 結果符合 **CREATE EVENT SESSION** 陳述式規格。


&nbsp;



<a name="section_B_1_SSMS_UI_perspective"></a>

### <a name="b1-ssms-ui-perspective"></a>B.1 SSMS UI 檢視方塊


在 SSMS 的 [物件總管]  中，您可以啟動 [新增工作階段]  對話方塊：請依序展開 [管理]   > [擴充事件]  ，然後以滑鼠右鍵按一下 [工作階段]   > [新增工作階段]  。

在大型 [新增工作階段]  對話方塊標示為 [一般]  的第一個區段中，我們看到已選取 [在伺服器啟動時啟動事件工作階段]  選項。

![[新增工作階段] > [一般]，[在伺服器啟動時啟動事件工作階段]。](../../relational-databases/extended-events/media/xevents-ssms-ac105-eventname-startup.png)


接下來在 [事件]  區段中，我們看到已選擇 [lock_deadlock]  事件。 我們看到該事件已選取三個 [動作]  。 這表示已按過 [設定]  按鈕，它在按下後會變成灰色。

![[新增工作階段] > [事件]，[全域欄位 (動作)]。](../../relational-databases/extended-events/media/xevents-ssms-ac110-actions-global.png)


<a name="resource_type_PAGE_cat_view"></a>

接下來，仍在 [事件]   > [設定]  區段中，我們看到 [**resource_type** 已設為 [PAGE]  ](#resource_type_dmv_actual_row)。 這表示，只要 **resource_type** 值是 [PAGE]  ，事件資料就會從事件引擎傳送到目標。

我們會看到資料庫名稱和計數器的其他述詞篩選。

![[新增工作階段] > [事件]，[Filter Predicate Fields (Actions) (篩選述詞欄位 (動作))]。](../../relational-databases/extended-events/media/xevents-ssms-ac115-predicate-db.png)


接著在 [資料儲存區]  區段，我們看到 **event_file** 已被選為目標。 而且，我們還看到已選取 [啟用檔案換用]  選項。

![[新增工作階段] > [資料儲存區]，eventfile_enablefilerollover](../../relational-databases/extended-events/media/xevents-ssms-ac120-target-eventfile.png)


最後，在 [進階]  區段看到 [分派延遲上限]  值減少到 4 秒。

![[新增工作階段] > [進階]，[分派延遲上限]](../../relational-databases/extended-events/media/xevents-ssms-ac125-latency4.png)


如此即完成事件工作階段定義的 SSMS UI 檢視方塊。


<a name="section_B_2_TSQL_perspective"></a>

### <a name="b2-transact-sql-perspective"></a>B.2 TRANSACT-SQL 檢視方塊


不論事件工作階段定義是如何建立的，工作階段可從 SSMS UI 進行還原工程，還原為 TRANSACT-SQL 指令碼完全相符。 您可以檢查前面的 [新增工作階段] 螢幕擷取畫面，比較其可見的規格和下列產生 T-SQL **CREATE EVENT SESSION** 指令碼的子句。

若要進行事件工作階段的還原工程，請在 [物件總管]  中以滑鼠右鍵按一下您的工作階段節點，然後選擇 [編寫工作階段的指令碼為]   > [CREATE 至]   > [剪貼簿]  。

下列 T-SQL 指令碼是經由 SSMS 還原工程所建立。 然後，只能以空白字元的策略操作手動美化指令碼。


```sql
CREATE EVENT SESSION [event_session_test3]
    ON SERVER  -- Or, if on Azure SQL Database, ON DATABASE.

    ADD EVENT sqlserver.lock_deadlock
    (
        SET
            collect_database_name = (1)
        ACTION
        (
            package0  .collect_system_time,
            package0  .event_sequence,
            sqlserver .client_hostname
        )
        WHERE
        (
            [database_name]           = N'InMemTest2'
            AND [package0].[counter] <= (16)
            AND [resource_type]       = (6)
        )
    )

    ADD TARGET package0.event_file
    (
        SET
            filename           = N'C:\Junk\event_session_test3_EF.xel',
            max_file_size      = (20),
            max_rollover_files = (2)
    )

    WITH
    (
        MAX_MEMORY            = 4096 KB,
        EVENT_RETENTION_MODE  = ALLOW_SINGLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY  = 4 SECONDS,
        MAX_EVENT_SIZE        = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY       = OFF,
        STARTUP_STATE         = ON
    );
```


如此即完成 T-SQL 檢視方塊。


<a name="section_B_3_Catalog_view_S_J_UNION"></a>

### <a name="b3-catalog-view-select-join-union-perspective"></a>B.3 目錄檢視的 SELECT JOIN UNION 檢視方塊


不要怕！ 下列 T-SQL SELECT 陳述式之所以很長，只是因為它將數個小型的 SELECT UNION 在一起。 任何小型的 SELECT 都可以獨立執行。 小型的 SELECT 顯示各種系統類別目錄檢視應該如何 JOIN 在一起。


```sql
SELECT
        s.name        AS [Session-Name],
        '1_EVENT'     AS [Clause-Type],
        'Event-Name'  AS [Parameter-Name],
        e.name        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name         AS [Session-Name],
        '2_EVENT_SET'  AS [Clause-Type],
        f.name         AS [Parameter-Name],
        f.value        AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '3_EVENT_ACTION'    AS [Clause-Type],

        a.package + '.' + a.name
                            AS [Parameter-Name],

        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_actions  As a

            ON  a.event_session_id = s.event_session_id
            AND a.event_id         = e.event_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                AS [Session-Name],
        '4_EVENT_PREDICATES'  AS [Clause-Type],
        e.predicate           AS [Parameter-Name],
        '(Not_Applicable)'    AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_events   AS e

            ON  e.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name              AS [Session-Name],
        '5_TARGET'          AS [Clause-Type],
        t.name              AS [Parameter-Name],
        '(Not_Applicable)'  AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name          AS [Session-Name],
        '6_TARGET_SET'  AS [Clause-Type],
        f.name          AS [Parameter-Name],
        f.value         AS [Parameter-Value]
    FROM
              sys.server_event_sessions         AS s
        JOIN  sys.server_event_session_targets  AS t

            ON  t.event_session_id = s.event_session_id

        JOIN  sys.server_event_session_fields   As f

            ON  f.event_session_id = s.event_session_id
            AND f.object_id        = t.target_id
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name               AS [Session-Name],
        '7_WITH_MAX_MEMORY'  AS [Clause-Type],
        'max_memory'         AS [Parameter-Name],
        s.max_memory         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

UNION ALL
SELECT
        s.name                  AS [Session-Name],
        '7_WITH_STARTUP_STATE'  AS [Clause-Type],
        'startup_state'         AS [Parameter-Name],
        s.startup_state         AS [Parameter-Value]
    FROM
              sys.server_event_sessions  AS s
    WHERE
        s.name = 'event_session_test3'

ORDER BY
    [Session-Name],
    [Clause-Type],
    [Parameter-Name]
;
```


#### <a name="output"></a>輸出


下表顯示執行前述 SELECT JOIN UNION 的輸出。 輸出參數的名稱和值會對應至清楚顯示在前一個 CREATE EVENT SESSION 陳述式中的內容。

| Session-Name | Clause-Type | Parameter-Name | Parameter-Value |
|---|---|---|---|
|event_session_test3  | 1_EVENT |                Event-Name |                       lock_deadlock |
|event_session_test3  |  2_EVENT_SET |             collect_database_name |            1 |
|event_session_test3  |  3_EVENT_ACTION |          sqlserver.client_hostname |       (不適用) |
|event_session_test3  |  3_EVENT_ACTION |         sqlserver.collect_system_time |   (不適用) |
|event_session_test3  |  3_EVENT_ACTION |         sqlserver.event_sequence |        (不適用) |
|event_session_test3  |  4_EVENT_PREDICATES |     (\[sqlserver\].\[equal_i_sql_unicode_string\]\(\[database_name\],N'InMemTest2'\) AND \[package0\].\[counter\]<=\(16\)\) |   (不適用) |
|event_session_test3  |  5_TARGET |               event_file |                      (不適用) |
|event_session_test3  |  6_TARGET_SET |           filename  |                       C:\Junk\event_session_test3_EF.xel |
|event_session_test3  |  6_TARGET_SET |           max_file_size |                   20 |
|event_session_test3  |  6_TARGET_SET |           max_rollover_files |              2 |
|event_session_test3  |  7_WITH_MAX_MEMORY |      max_memory |                      4096 |
|event_session_test3  |  7_WITH_STARTUP_STATE |   startup_state |                   1 |

如此即完成目錄檢視區段。



<a name="section_C_DMVs"></a>

## <a name="c-dynamic-management-views-dmvs"></a>C. 動態管理檢視 (DMV)


我們現在轉至 DMV。 本節提供數個各有特定實用商業用途的 Transact-SQL SELECT 陳述式。 此外，SELECT 會示範如何將 DMV JOIN 在一起，以取得您想要的任何新用法。


DMV 的參考文件位於 [擴充事件動態管理檢視](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)


在本文中，除非另有指定，否則下列 SELECT 的所有實際輸出資料列皆是出自 SQL Server 2016。


以下是本節 C DMV 的 SELECT 清單：

- [C.1 所有的封裝清單](#section_C_1_list_packages)
- [C.2 每個物件類型的計數](#section_C_2_count_object_type)
- [C.3 SELECT 所有可用的項目依類型排序](#section_C_3_select_all_available_objects)
- [C.4 事件可用的資料欄位](#section_C_4_data_fields)
- [C.5 *sys.dm_xe_map_values* 和事件欄位](#section_C_5_map_values_fields)
- [C.6 目標的參數](#section_C_6_parameters_targets)
- [C.7 DMV SELECT 將 target_data 資料行轉換成 XML](#section_C_7_dmv_select_target_data_column)
- [C.8 函數的 SELECT 從磁碟機擷取 event_file 資料](#section_C_8_select_function_disk)



<a name="section_C_1_list_packages"></a>

### <a name="c1-list-of-all-packages"></a>C.1 所有的封裝清單


所有您可以在擴充事件區域中使用的物件，都來自系統載入的封裝。 本節會列出所有封裝及其說明。


```sql
SELECT  --C.1
        p.name         AS [Package],
        p.description  AS [Package-Description]
    FROM
        sys.dm_xe_packages  AS p
    ORDER BY
        p.name;
```


#### <a name="output"></a>輸出

以下為封裝清單。

| Package        |Package-Description|
|---|---|
|檔案資料流|     SQL Server FILESTREAM 和 FileTable 的擴充事件 |
|package0   |    預設套件。 包含所有標準類型、對應、比較運算子、動作和目標 |
|qds         |   查詢存放區的擴充事件 |
|SecAudit     |  安全性稽核事件 |
|sqlclr        | SQL CLR 的擴充事件 |
|sqlos         | SQL 作業系統的擴充事件 |
|SQLSatellite |  SQL Satellite 的擴充事件 |
|sqlserver   |   Microsoft SQL Server 的擴充事件 |
|sqlserver  |    Microsoft SQL Server 的擴充事件 |
|sqlserver  |    Microsoft SQL Server 的擴充事件 |
|sqlsni     |    Microsoft SQL Server 的擴充事件 |
|ucs        |    整合通訊堆疊的擴充事件 |
|XtpCompile |    XTP 編譯的擴充事件 |
|XtpEngine  |    XTP 引擎的擴充事件 |
|XtpRuntime |    XTP 執行階段的擴充事件 |


*前列縮寫定義︰*

- clr = .NET 的 Common Language Runtime
- qds = 查詢資料存放區 (Query Data Store)
- sni = 伺服器網路介面 (Server Network Interface)
- ucs = 整合通訊堆疊 (Unified Communications Stack)
- xtp = 極端交易處理 (extreme transaction processing)


<a name="section_C_2_count_object_type"></a>

### <a name="c2-count-of-every-object-type"></a>C.2 每個物件類型的計數


本節會告訴我們事件封裝包含的物件類型。 顯示 *sys.dm\_xe\_objects* 所有物件類型的完整清單，以及每種類型的計數。


```sql
SELECT  --C.2
        Count(*)  AS [Count-of-Type],
        o.object_type
    FROM
        sys.dm_xe_objects  AS o
    GROUP BY
        o.object_type
    ORDER BY
        1  DESC;
```


#### <a name="output"></a>輸出

以下是每個物件類型的物件計數。 約有 1915 個物件。

|Count-of-Type |   object_type |
|---|---|
|1303|            event |
|351  |           map |
|84    |          message |
|77     |         pred_compare |
|53     |        動作 |
|46     |         pred_source |
|28     |         type |
|17     |         目標 |

<a name="section_C_3_select_all_available_objects"></a>

### <a name="c3-select-all-available-items-sorted-by-type"></a>C.3 SELECT 所有可用的項目依類型排序


下列的 SELECT 會傳回約 1915 筆資料列，每列一個物件。



```sql
SELECT  --C.3
        o.object_type  AS [Type-of-Item],
        p.name         AS [Package],
        o.name         AS [Item],
        o.description  AS [Item-Description]
    FROM
             sys.dm_xe_objects  AS o
        JOIN sys.dm_xe_packages AS p  ON o.package_guid = p.guid
    WHERE
        o.object_type IN ('action' , 'target' , 'pred_source')
        AND
        (
            (o.capabilities & 1) = 0
            OR
            o.capabilities IS NULL
        )
    ORDER BY
        [Type-of-Item],
        [Package],
        [Item];
```


#### <a name="output"></a>輸出

為了挑起您的興趣，接下來是前述 SELECT 傳回之物件的任意取樣。


|Type-of-Item|   Package|        Item|                          Item-Description|
|---|---|---|---|
|動作|         package0  |     callstack                     |收集目前呼叫堆疊|
|動作 |        package0  |     debug_break                   |中斷預設偵錯工具中的處理序|
|動作 |       sqlos      |    task_time                     |收集目前工作執行時間|
|動作 |        sqlserver |     sql_text                     | 收集 SQL 文字|
|event  |        qds       |     query_store_aprc_regression  | 當查詢存放區偵測到查詢計畫效能低下時引發|
|event  |        SQLSatellite |  connection_accept            | 接受新連線時會發生。 此事件是用來記錄所有的連線嘗試。|
|event  |        XtpCompile  |   cgen                          |在開始產生 C 程式碼時發生。|
|map    |        qds         |   aprc_state                    |查詢存放區自動計畫迴歸修正狀態|
|message |       package0    |   histogram_event_required      |來源類型為 0 時，參數 'filtering_event_name' 必須有值。|
|pred_compare |  package0   |    equal_ansi_string             |兩個 ANSI 字串值之間的等號比較運算子|
|pred_compare |  sqlserver  |    equal_i_sql_ansi_string       |兩個 SQL ANSI 字串值之間的等號比較運算子|
|pred_source |   sqlos      |    task_execution_time           |取得目前工作的執行時間|
|pred_source |   sqlserver  |    client_app_name               |取得目前用戶端應用程式名稱|
|目標 |        package0   |    etw_classic_sync_target       |Windows 事件追蹤 (ETW) 同步目標|
|目標 |        package0   |    event_counter                 |使用 event_counter 目標可計算事件工作階段中每個事件的發生次數。|
|目標  |       package0  |     event_file                    |使用 event_file 目標可將事件資料儲存到 XEL 檔案，之後可以封存起來供未來的分析和檢閱使用。 您可合併多個 XEL 檔案，以檢視來自不同事件工作階段的合併資料。|
|目標  |       package0   |    長條圖                     |使用長條圖目標可根據特定事件資料欄位或事件相關動作來彙總事件資料。 長條圖可供分析整個事件工作階段中事件資料的分佈情形。|
|目標   |      package0  |     pair_matching                 |配對目標|
|目標   |      package0  |     ring_buffer                   |非同步通道緩衝區目標|
|type     |      package0  |     Xml                           |格式正確的 XML 片段|

<a name="section_C_4_data_fields"></a>

### <a name="c4-data-fields-available-for-your-event"></a>C.4 事件可用的資料欄位


下列的 SELECT 會傳回事件類型特有的所有資料欄位。

- 注意 WHERE 子句項目： *column_type = 'data'* 。
- 您也必須編輯 *o.name =* 的 WHERE 子句值。


```sql
SELECT  -- C.4
        p.name         AS [Package],
        c.object_name  AS [Event],
        c.name         AS [Column-for-Predicate-Data],
        c.description  AS [Column-Description]
    FROM
              sys.dm_xe_object_columns  AS c
        JOIN  sys.dm_xe_objects         AS o

            ON  o.name = c.object_name

        JOIN  sys.dm_xe_packages        AS p

            ON  p.guid = o.package_guid
    WHERE
        c.column_type = 'data'
        AND
        o.object_type = 'event'
        AND
        o.name        = '\<EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Event],
        [Column-for-Predicate-Data];
```


#### <a name="output"></a>輸出

以下為前述 SELECT 傳回的資料列 WHERE `o.name = 'lock_deadlock'`：

- 每個資料列都代表 *sqlserver.lock_deadlock* 事件的選用篩選。
- 下列畫面省略 [資料行描述] *\[\]* 資料行。 其值通常為 NULL。
- 這是實際的輸出，但省略的 Description 資料行除外 (通常為 NULL)。
- 這些是 object_type = 'lock_deadlock' 的資料列。

|Package|     事件|           Column-for-Predicate-Data|
|---|---|---|
|sqlserver|   lock_deadlock|   associated_object_id|
|sqlserver|  lock_deadlock |  database_id|
|sqlserver|  lock_deadlock |  database_name|
|sqlserver|   lock_deadlock|   deadlock_id|
|sqlserver|   lock_deadlock|   duration|
|sqlserver|   lock_deadlock|   lockspace_nest_id|
|sqlserver|   lock_deadlock|   lockspace_sub_id|
|sqlserver|   lock_deadlock|   lockspace_workspace_id|
|sqlserver|   lock_deadlock|   mode|
|sqlserver|   lock_deadlock|   object_id|
|sqlserver|   lock_deadlock|   owner_type|
|sqlserver|   lock_deadlock|   resource_0|
|sqlserver|   lock_deadlock|  resource_1|
|sqlserver|   lock_deadlock|   resource_2|
|sqlserver|   lock_deadlock|   resource_description|
|sqlserver|   lock_deadlock|   resource_type|
|sqlserver|   lock_deadlock|   transaction_id|




<a name="section_C_5_map_values_fields"></a>

### <a name="c5-sysdm_xe_map_values-and-event-fields"></a>C.5 *sys.dm_xe_map_values* 和事件欄位


下列 SELECT 包含名為 *sys.dm_xe_map_values*之複雜檢視的 JOIN。

SELECT 旨在顯示您可為事件工作階段選擇的許多欄位。 事件欄位有兩種用法︰

- 選擇會寫入每個發生事件目標的欄位值。
- 篩選會傳送的發生事件與從目標保留的發生事件。


```sql
SELECT  --C.5
        dp.name         AS [Package],
        do.name         AS [Object],
        do.object_type  AS [Object-Type],
        'o--c'     AS [O--C],
        dc.name         AS [Column],
        dc.type_name    AS [Column-Type-Name],
        dc.column_type  AS [Column-Type],
        dc.column_value AS [Column-Value],
        'c--m'     AS [C--M],
        dm.map_value    AS [Map-Value],
        dm.map_key      AS [Map-Key]
    FROM
              sys.dm_xe_objects         AS do
        JOIN  sys.dm_xe_object_columns  AS dc

            ON  dc.object_name = do.name

        JOIN  sys.dm_xe_map_values      AS dm

            ON  dm.name = dc.type_name

        JOIN  sys.dm_xe_packages        AS dp

            ON  dp.guid = do.package_guid
    WHERE
        do.object_type = 'event'
        AND
        do.name        = '\<YOUR-EVENT-NAME-HERE!>'  --'lock_deadlock'
    ORDER BY
        [Package],
        [Object],
        [Column],
        [Map-Value];
```


#### <a name="output"></a>輸出

<a name="resource_type_dmv_actual_row"></a>

接下來是前述 T-SQL SELECT 實際輸出之 153 個資料列的取樣。 **resource_type** 的資料列與本文他處所舉之 [event_session_test3](#resource_type_PAGE_cat_view) 範例使用的述詞篩選 **相關** 。


```
/***  5 sampled rows from the actual 153 rows returned.
    NOTE:  'resource_type' under 'Column'.

Package     Object          Object-Type   O--C   Column          Column-Type-Name     Column-Type   Column-Value   C--M   Map-Value        Map-Key
-------     ------          -----------   ----   ------          ----------------     -----------   ------------   ----   ---------        -------
sqlserver   lock_deadlock   event         o--c   CHANNEL         etw_channel          readonly      2              c--m   Operational      4
sqlserver   lock_deadlock   event         o--c   KEYWORD         keyword_map          readonly      16             c--m   access_methods   1024
sqlserver   lock_deadlock   event         o--c   mode            lock_mode            data          NULL           c--m   IX               8
sqlserver   lock_deadlock   event         o--c   owner_type      lock_owner_type      data          NULL           c--m   Cursor           2
sqlserver   lock_deadlock   event         o--c   resource_type   lock_resource_type   data          NULL           c--m   PAGE             6

Therefore, on your CREATE EVENT SESSION statement, in its ADD EVENT WHERE clause,
you could put:
    WHERE( ... resource_type = 6 ...)  -- Meaning:  6 = PAGE.
***/
```


<a name="section_C_6_parameters_targets"></a>

### <a name="c6-parameters-for-targets"></a>C.6 目標的參數


下列 SELECT 會傳回目標的每個參數。 每個參數都會標記，以指出它是否為強制。 您指派給參數的值會影響目標的行為。

- 注意 WHERE 子句項目︰ *object_type = 'customizable'* 。
- 您也必須編輯 *o.name =* 的 WHERE 子句值。


```sql
SELECT  --C.6
        p.name        AS [Package],
        o.name        AS [Target],
        c.name        AS [Parameter],
        c.type_name   AS [Parameter-Type],

        CASE c.capabilities_desc
            WHEN 'mandatory' THEN 'YES_Mandatory'
            ELSE 'Not_mandatory'
        END  AS [IsMandatoryYN],

        c.description AS [Parameter-Description]
    FROM
              sys.dm_xe_objects   AS o
        JOIN  sys.dm_xe_packages  AS p

            ON  o.package_guid = p.guid

        LEFT OUTER JOIN  sys.dm_xe_object_columns  AS c

            ON  o.name        = c.object_name
            AND c.column_type = 'customizable'  -- !
    WHERE
        o.object_type = 'target'
        AND
        o.name     LIKE '%'    -- Or '\<YOUR-TARGET-NAME-HERE!>'.
    ORDER BY
        [Package],
        [Target],
        [IsMandatoryYN]  DESC,
        [Parameter];
```


#### <a name="output"></a>輸出

以下為 SQL Server 2016 中前述 SELECT 傳回的參數資料列子集。


```
/***  Actual output, all rows, where target name = 'event_file'.
Package    Target       Parameter            Parameter-Type       IsMandatoryYN   Parameter-Description
-------    ------       ---------            --------------       -------------   ---------------------
package0   event_file   filename             unicode_string_ptr   YES_Mandatory   Specifies the location and file name of the log
package0   event_file   increment            uint64               Not_mandatory   Size in MB to grow the file
package0   event_file   lazy_create_blob     boolean              Not_mandatory   Create blob upon publishing of first event buffer, not before.
package0   event_file   max_file_size        uint64               Not_mandatory   Maximum file size in MB
package0   event_file   max_rollover_files   uint32               Not_mandatory   Maximum number of files to retain
package0   event_file   metadatafile         unicode_string_ptr   Not_mandatory   Not used
***/
```


<a name="section_C_7_dmv_select_target_data_column"></a>

### <a name="c7-dmv-select-casting-target_data-column-to-xml"></a>C.7 DMV SELECT 將 target_data 資料行轉換成 XML


這個 DMV SELECT 從作用中事件工作階段的目標傳回資料列。 資料會轉換成 XML，使其傳回的資料格為可按式項目，輕鬆以 SSMS 顯示。

- 如果停止事件工作階段，此 SELECT 就不會傳回資料列。
- 您可能需要編輯 *s.name =* 的 WHERE 子句值。


```sql
SELECT  --C.7
        s.name,
        t.target_name,
        CAST(t.target_data AS XML)  AS [XML-Cast]
    FROM
              sys.dm_xe_session_targets  AS t
        JOIN  sys.dm_xe_sessions         AS s

            ON s.address = t.event_session_address
    WHERE
        s.name = '\<Your-Session-Name-Here!>';
```


#### <a name="output-the-only-row-including-its-xml-cell"></a>輸出：唯一的資料列，包括其 XML 儲存格。

以下是前述 SELECT 輸出的唯一資料列。 資料行「XML 轉換」  包含 SSMS 了解其為 XML 的 XML 字串，。 因此 SSMS 了解應該讓「XML 轉換」資料格成為可按式項目。


為執行此作業︰

- *s.name =* 值已設成 *checkpoint_begin* 事件的事件工作階段。
- 目標是 *ring_buffer*。


```XML
name                              target_name   XML-Cast
----                              -----------   --------
checkpoint_session_ring_buffer2   ring_buffer   <RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104"><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event><event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z"><data name="database_id"><type name="uint32" package="package0" /><value>5</value></data></event></RingBufferTarget>
```


#### <a name="output-xml-displayed-pretty-when-cell-is-clicked"></a>輸出：當資料格為可按式項目時，XML 顯示良好。


當「XML 轉換」資料格是可按式項目時，即會出現下列良好的畫面。


```xml
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="104">
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:23.508Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
  <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T01:28:26.975Z">
    <data name="database_id">
      <type name="uint32" package="package0" />
      <value>5</value>
    </data>
  </event>
</RingBufferTarget>
```


<a name="section_C_8_select_function_disk"></a>

### <a name="c8-select-from-a-function-to-retrieve-event_file-data-from-disk-drive"></a>C.8 函數的 SELECT 從磁碟機擷取 event_file 資料


假設事件工作階段在收集了某些資料後停止。 如果您的工作階段已定義為使用 event_file 目標，您仍然可以呼叫 *sys.fn_xe_target_read_file*函數以擷取資料。

- 您必須先在函數呼叫的參數中編輯路徑和檔案名稱，再執行此 SELECT。
    - 不用理會 SQL 系統在工作階段每次重新啟動時，嵌入到實際 .XEL 檔案名稱中的額外數字。 只要提供標準的根名稱和副檔名即可。


```sql
SELECT  --C.8
        f.module_guid,
        f.package_guid,
        f.object_name,
        f.file_name,
        f.file_offset,
        CAST(f.event_data AS XML)  AS [Event-Data-As-XML]
    FROM
        sys.fn_xe_file_target_read_file(

            '\<YOUR-PATH-FILE-NAME-ROOT-HERE!>*.xel',
            --'C:\Junk\Checkpoint_Begins_ES*.xel',  -- Example.

            NULL, NULL, NULL
        )  AS f;
```


#### <a name="output-rows-returned-by-select-from-the-function"></a>輸出：SELECT FROM 函數傳回的資料列。


接著是前述 SELECT FROM 函數傳回的資料列。 最右邊的 XML 資料行包含專門針對發生事件的資料。


```
module_guid                            package_guid                           object_name        file_name                                                           file_offset   Event-Data-As-XML
-----------                            ------------                           -----------        ---------                                                           -----------   -----------------
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5120          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:14.025Z"><data name="database_id"><value>5</value></data></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_begin   C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:17.704Z"><data name="database_id"><value>5</value></data><action name="session_id" package="sqlserver"><value>60</value></action><action name="database_id" package="sqlserver"><value>5</value></action></event>
D5149520-6282-11DE-8A39-0800200C9A66   03FDA7D0-91BA-45F8-9875-8B6DD0B8E9F2   checkpoint_end     C:\Junk\Checkpoint_Begins_ES_20160615bb-_0_131125086091700000.xel   5632          <event name="checkpoint_end" package="sqlserver" timestamp="2016-07-09T03:30:17.709Z"><data name="database_id"><value>5</value></data></event>
```


#### <a name="output-one-xml-cell"></a>輸出：一個 XML 資料格。


以下是第一個 XML 資料格的內容，來自前述的傳回資料列集。


```xml
<event name="checkpoint_begin" package="sqlserver" timestamp="2016-07-09T03:30:14.023Z">
  <data name="database_id">
    <value>5</value>
  </data>
  <action name="session_id" package="sqlserver">
    <value>60</value>
  </action>
  <action name="database_id" package="sqlserver">
    <value>5</value>
  </action>
</event>
```


