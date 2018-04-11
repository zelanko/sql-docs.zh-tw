---
title: 快速入門︰SQL Server 中的擴充事件 | Microsoft Docs
ms.custom: ''
ms.date: 09/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7bb78b25-3433-4edb-a2ec-c8b2fa58dea1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ac73b7d77058a6586f82cba15fd3d36df11e6c05
ms.sourcegitcommit: 094c46e7fa6de44735ed0040c65a40ec3d951b75
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="quick-start-extended-events-in-sql-server"></a>快速入門︰SQL Server 中的擴充事件
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


本文旨在協助剛接觸擴充事件，而且想要在幾分鐘內建立事件工作階段的 SQL 開發人員。 藉由使用擴充事件，您可以查看 SQL 系統及您的應用程式內部作業的詳細資訊。 當您建立擴充事件工作階段時，您會告訴系統：

- 您感興趣的項目。
- 系統要如何回報資料給您。


本文會執行下列各項：

- 使用螢幕擷取畫面來描述如何在 SSMS.exe 中點選以建立事件工作階段。
- 將螢幕擷取畫面相互關聯至對等的 Transact-SQL 陳述式。
- 詳細說明這些點選及事件工作階段之 T-SQL 背後的詞彙與概念。
- 示範如何測試您的事件工作階段。
- 描述與結果相關的選項：
  - 結果的存放區擷取。
  - 已處理的結果與未經處理的結果比較。
  - 以不同的方式及不同的時間間隔檢視結果的工具。
- 示範如何搜尋及探索所有可用的事件。
- 提供擴充事件的動態管理檢視 (DMV) 之間隱含的主索引鍵與外部索引鍵關聯性。
- 描述可從相關文章了解的其他內容。


部落格及其他非正式交談有時會以縮寫 *xevents*來指稱擴充事件。


> [!NOTE]
> 如需 Microsoft SQL Server 與 Azure SQL Database 之間擴充事件差異的相關資訊，請參閱 [SQL Database 中的擴充事件](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)。


## <a name="preparations-before-demo"></a>示範前的準備工作


您必須完成下列準備工作，才能實際執行後續的示範。

1. [下載 SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx)
  - 您應該每個月安裝 SSMS 的最新每月更新。
2. 登入 Microsoft SQL Server 2014 或更新版本，或是 Azure SQL Database 資料庫 (其中的 `SELECT @@version` 會傳回其第一個節點為 12 或更高的值)。
3. 確定您的帳戶具有 [伺服器權限](../../t-sql/statements/grant-server-permissions-transact-sql.md) ： **ALTER ANY EVENT SESSION**。
  - 如有興趣，本文結尾的 [附錄](#appendix1)將提供可用擴充事件之相關安全性和權限的詳細資訊。




## <a name="demo-of-ssms-integration"></a>SSMS 整合的示範


SSMS.exe 為擴充事件提供絕佳的使用者介面 (UI)。 此 UI 很理想，許多使用者並不需要使用 Transact-SQL 或以擴充事件為目標的動態管理檢視 (DMV)，就能與擴充事件互動。

在本節中，您會看到建立擴充事件的 UI 步驟，以及它所報告的資料。 在這些步驟之後，您可以閱讀步驟的相關概念，以更深入了解。


### <a name="steps-of-demo"></a>示範的步驟


即使您決定不要執行這些步驟，還是可以加以了解。 此示範會啟動 [新增工作階段] 對話方塊。 我們會處理其四個頁面：

- 一般
- 事件
- 資料儲存
- 進階


SSMS UI 經年累月的調整結果，可能會造成文字和支援的螢幕擷取畫面有些不正確。 但如有不一致的情況或只是稍微不正確，這些螢幕擷取畫面還是能夠有效地用於說明。


1. 連接到 SSMS。

2. 在物件總管中，按一下 [管理] > [擴充事件] > [新增工作階段]。 使用 [新增工作階段] 對話方塊會比使用 [新增工作階段精靈] 更合適，不過這兩者彼此類似。

3. 按一下左上方的 [一般] 頁面。 然後在 [工作階段名稱] 文字方塊中，輸入「您的工作階段」或任何您想要的名稱。 還「不要」按下 [確定] 按鈕，只有示範結束時才需要。

    ![[新增工作階段] > [一般] > [工作階段名稱]](../../relational-databases/extended-events/media/xevents-session-newsessions-10-general-ssms-yoursessionnode.png)

4. 按一下左上方的 [事件] 頁面，然後按一下 [選取] 按鈕。

    ![[新增工作階段] > [事件] > [選取] > [事件程式庫]、[選取的事件]](../../relational-databases/extended-events/media/xevents-session-newsessions-14-events-ssms-rightclick-not-wizard.png)

5. 在 [事件程式庫] 區域的下拉式清單中，選擇 [僅限事件名稱]。
    - 在文字方塊中，輸入 **sql**，這會使用 *contains* 運算子來篩選並縮短很長的可用事件清單。
    - 捲動並按一下名為 **sql_statement_completed** 的事件。
    - 按一下向右箭號按鈕 [>]，將事件移至 [選取的事件] 方塊。

6. 在 [事件] 頁面上，按一下最右邊的 [設定] 按鈕。
    - 為了更佳顯示，已截斷左側；在下列螢幕擷取畫面中，您會看到 [事件組態選項] 區域。

    ![[新增工作階段] > [事件] > [設定] > [篩選 (述詞)] > [欄位]](../../relational-databases/extended-events/media/xevents-session-newsessions-20b-events-ssms-yoursessionnode.png)

7. 按一下 [篩選 (述詞)] 索引標籤。接著，按一下 [請按這裡加入子句]，以擷取具有 HAVING 子句的所有 SQL SELECT 陳述式。

8. 在 [欄位] 下拉式清單中，選擇 **sqlserver.sql_text**。
   - 針對 [運算子]，選擇 LIKE 運算子。
   - 針對 [值]，輸入 **%SELECT%HAVING%**。

    > [!NOTE]
    > 在這個兩部分名稱中，*sqlserver* 是封裝名稱，而 *sql_text* 是欄位名稱。 我們稍早所選擇的事件 *sql_statement_completed* ，必須與所選擇的欄位在相同的封裝中。

9. 按一下左上方的 [資料存放區] 頁面。

10. 在 [目標] 區域中，按一下 [按一下此處以加入目標]。
    - 在 [類型] 下拉式清單中，選擇 **event_file**。
    - 這表示事件資料將會儲存在我們可以檢視的檔案中。

    ![[新增工作階段] > [資料存放區] > [目標] > [類型] > event_file](../../relational-databases/extended-events/media/xevents-session-newsessions-30-datastorage-ssms-yoursessionnode.png)

11. 在 [屬性] 區域的 [伺服器上的檔案名稱] 文字方塊中，輸入完整路徑和檔案名稱。
    - 副檔名必須是 *.xel*。
    - 我們的小型測試需要不到 1 MB 的檔案大小。

    ![[新增工作階段] > [進階] > [分派延遲上限] > [確定]](../../relational-databases/extended-events/media/xevents-session-newsessions-40-advanced-ssms-yoursessionnode.png)

12. 按一下左上方的 [進階] 頁面。
    - 將 [分派延遲上限] 減少為 3 秒。
    - 最後，按一下底部的 [確定] 按鈕。

13. 回到物件總管，展開 [管理] > [工作階段]，即會顯示新節點 [您的工作階段]。

    ![物件總管中的 [管理] > [擴充事件] > [工作階段] 下，名為「您的工作階段」的新「事件工作階段」節點](../../relational-databases/extended-events/media/xevents-session-newsessions-50-objectexplorer-ssms-yoursessionnode.png)


#### <a name="edit-your-event-session"></a>編輯事件工作階段


在 SSMS 物件總管中，您可以編輯事件工作階段，方法是以滑鼠右鍵按一下其節點，然後按一下 [屬性]。 這會顯示相同的多頁對話方塊。


### <a name="corresponding-t-sql-for-your-event-session"></a>您的事件工作階段的對應 T-SQL


您可以使用 SSMS UI，來產生建立事件工作階段的 T-SQL 指令碼。 產生的指令碼如下所示：

- 以滑鼠右鍵按一下您的工作階段節點，然後按一下 [編寫工作階段的指令碼為] > [CREATE to (CREATE 至)] > [剪貼簿]。
- 貼到任何文字編輯器中。


以下是您在 UI 中點選後，針對 [您的工作階段] 所產生的 T-SQL CREATE EVENT SESSION 陳述式：


```sql
CREATE EVENT SESSION [YourSession]
    ON SERVER 
    ADD EVENT sqlserver.sql_statement_completed
    (
        ACTION(sqlserver.sql_text)
        WHERE
        ( [sqlserver].[like_i_sql_unicode_string]([sqlserver].[sql_text], N'%SELECT%HAVING%')
        )
    )
    ADD TARGET package0.event_file
    (SET
        filename = N'C:\Junk\YourSession_Target.xel',
        max_file_size = (2),
        max_rollover_files = (2)
    )
    WITH (
        MAX_MEMORY = 2048 KB,
        EVENT_RETENTION_MODE = ALLOW_MULTIPLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY = 3 SECONDS,
        MAX_EVENT_SIZE = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY = OFF,
        STARTUP_STATE = OFF
    );
GO
```


> [!NOTE]
> 若為 Azure SQL Database，上述 CREATE EVENT SESSION 陳述式中的 ON SERVER 子句會改為 ON DATABASE。
> 
> 如需 Microsoft SQL Server 與 Azure SQL Database 之間擴充事件差異的詳細資訊，請參閱 [SQL Database 中的擴充事件](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)。


#### <a name="pre-drop-of-the-event-session"></a>DROP 事件工作階段之前


在 CREATE EVENT SESSION 陳述式之前，您可能想要有條件地發出 DROP EVENT SESSION，以免名稱已經存在。


```sql
IF EXISTS (SELECT *
      FROM sys.server_event_sessions    -- If Microsoft SQL Server.
    --FROM sys.database_event_sessions  -- If Azure SQL Database in the cloud.
      WHERE name = 'YourSession')
BEGIN
    DROP EVENT SESSION YourSession
          ON SERVER;    -- If Microsoft SQL Server.
        --ON DATABASE;  -- If Azure SQL Database.
END
go
```


#### <a name="alter-to-start-and-stop-the-event-session"></a>ALTER 以開始和停止事件工作階段


當您建立事件工作階段時，預設為無法自動開始執行。 您可以使用下列 T-SQL ALTER EVENT SESSION 陳述式，隨時開始或停止事件工作階段。


```sql
ALTER EVENT SESSION [YourSession]
      ON SERVER
    --ON DATABASE
    STATE = START;   -- STOP;
```


啟動 SQL Server 執行個體之後，您可以選擇指示事件工作階段自動開始。 請參閱 CREATE EVENT SESSION 上的 **STARTUP STATE = ON** 關鍵字。

- SSMS UI 在 [新增工作階段] > [一般] 頁面上，提供對應的核取方塊。


## <a name="test-your-event-session"></a>測試您的事件工作階段


利用下列簡單步驟來測試您的事件工作階段：

1. 在 SSMS 物件總管中，以滑鼠右鍵按一下您的事件工作階段節點，然後按一下 [開始工作階段]。
2. 執行下列 `SELECT...HAVING` 陳述式兩次。
    - 在理想情況下，您可能會變更兩次執行之間的 `HAVING Count` 值，在 2 和 3 之間切換。 這可讓您查看不同的結果。
3. 以滑鼠右鍵按一下您的工作階段節點，然後按一下 [停止工作階段]。
4. 閱讀下一小節有關[如何 SELECT 並檢視結果](#select-the-full-results-xml-37)的相關資訊。



```sql
SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o
    
            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) >= 3   --2     -- Try both values during session.
    ORDER BY
        c.name;
```


為完整顯示，以下是上述 SELECT...HAVING 中的近似輸出。


```
/*** Approximate output, 6 rows, all HAVING Count >= 3:
name                   Count-Per-Column-Repeated-Name
---------------------  ------------------------------
event_group_type       4
event_group_type_desc  4
event_session_address  5
event_session_id       5
is_trigger_event       4
trace_event_id         3
***/
```



<a name="select-the-full-results-xml-37"/>

### <a name="select-the-full-results-as-xml"></a>以 XML 形式 SELECT 完整的結果


在 SSMS 中，執行下列 T-SQL SELECT 以傳回結果，其中每個資料列會提供一個事件項目的相關資料。 CAST AS XML 可讓您輕鬆地檢視結果。


> [!NOTE]
> 此事件系統一律會在您指定的 *.xel* event_file 檔案名稱前面附加長數字。 您必須複製系統指定的完整名稱並貼到 SELECT 中，才能從檔案執行下列 SELECT。


```sql
SELECT
        object_name,
        file_name,
        file_offset,
        event_data,
        'CLICK_NEXT_CELL_TO_BROWSE_XML RESULTS!'
                AS [CLICK_NEXT_CELL_TO_BROWSE_XML_RESULTS],
    
        CAST(event_data AS XML) AS [event_data_XML]
                -- TODO: In ssms.exe results grid, double-click this xml cell!
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\Junk\YourSession_Target_0_131085363367310000.xel',
            null, null, null
        );
```


上述 SELECT 提供兩種方式，讓您檢視任何指定事件資料列的完整結果：

- 在 SSMS 中執行 SELECT，然後按一下 **event_data_XML** 資料行中的資料格。 這非常好用。
- 從 [event_data] 資料行中的資料格，複製很長的 XML 字串。 貼到任何純文字編輯器中 (例如 Notepad.exe)，並將字串儲存在副檔名為 .XML 的檔案。 然後使用瀏覽器開啟 .XML 檔案。


#### <a name="display-of-results-for-one-event"></a>顯示一個事件的結果


接下來，我們將看到以 XML 格式表示的部分結果。 為縮短顯示畫面，此處的 XML 已經過編輯。 請注意， `<data name="row_count">` 顯示值為 `6`，符合稍早所顯示的 6 個結果資料列。 此外，我們也會看到整個 SELECT 陳述式。


```xml
<event name="sql_statement_completed" package="sqlserver" timestamp="2016-05-24T04:06:08.997Z">
  <data name="duration">
    <value>111021</value>
  </data>
  <data name="cpu_time">
    <value>109000</value>
  </data>
  <data name="physical_reads">
    <value>0</value>
  </data>
  <data name="last_row_count">
    <value>6</value>
  </data>
  <data name="offset">
    <value>0</value>
  </data>
  <data name="offset_end">
    <value>584</value>
  </data>
  <data name="statement">
    <value>SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o

            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) &gt;= 3   --2     -- Try both values during session.
    ORDER BY
        c.name</value>
  </data>
</event>
```


## <a name="ssms-to-display-results"></a>使用 SSMS 顯示結果


您可以使用 SSMS UI 中的幾項進階功能，來檢視擷取自擴充事件的資料。 詳情請參閱：

- [Advanced Viewing of Target Data from Extended Events in SQL Server (進階檢視 SQL Server 中擴充事件的目標資料)](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)


此基本概念會從標示為 [View Target Data (檢視目標資料)] 和 [Watch Live Data (觀看即時資料)] 的操作功能表選項開始。


### <a name="view-target-data"></a>檢視目標資料


在 SSMS 物件總管中，以滑鼠右鍵按一下您的事件工作階段節點下的目標節點。 在操作功能表中，按一下 [View Target Data (檢視目標資料)]。 SSMS 會隨即顯示資料。

當事件報告新資料時，此顯示畫面不會更新。 但您可以再按一次 [View Target Data (檢視目標資料)]。


![在 SSMS 中的 [管理] > [擴充事件] > [工作階段] > [您的工作階段] > package0.event_file，按一下滑鼠右鍵所顯示的 [View Target Data (檢視目標資料)]](../../relational-databases/extended-events/media/xevents-viewtargetdata-ssms-targetnode-61.png)


### <a name="watch-live-data"></a>觀看即時資料


在 SSMS 物件總管中，以滑鼠右鍵按一下您的事件工作階段節點。 在操作功能表中，按一下 [Watch Live Data (觀看即時資料)]。 SSMS 會即時顯示持續送達的內送資料。


![在 SSMS 中的 [管理] > [擴充事件] > [工作階段] > [您的工作階段]，按一下滑鼠右鍵所顯示的 [Watch Live Data (觀看即時資料)]](../../relational-databases/extended-events/media/xevents-watchlivedata-ssms-yoursessionnode-63.png)


## <a name="scenarios"></a>案例


有無數個有效使用擴充事件的案例。 下列文章提供有關查詢期間取得鎖定的範例案例。


這些特定的事件工作階段案例旨在評估下列文章中所述的鎖定。 這些文章也會示範一些進階技術，例如使用 **@dbid**，以及使用動態 `EXECUTE (@YourSqlString)`：

- [尋找持有最多鎖定的物件](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)
  - 此案例使用目標 package0.histogram，它會處理未經處理的事件資料，再向您顯示。
- [判斷哪些查詢持有鎖定](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)
  - 此案例使用 [目標 package0.pair_matching](http://msdn.microsoft.com/library/3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3)，其中的事件配對為 sqlserver.lock_acquire 和 lock_release。


## <a name="terms-and-concepts-in-extended-events"></a>擴充事件的詞彙和概念


下表列出用於擴充事件的詞彙，並說明其意義。


| 詞彙 | 描述 |
| :--- | :---------- |
| 事件工作階段 | 目標為以一或多項事件為主的建構，加上支援的項目 (例如動作)。 CREATE EVENT SESSION 陳述式會建構每個事件工作階段。 您可以隨意 ALTER 事件工作階段，以開始和停止工作階段。 <br/> <br/> 如果內容釐清其表示「事件工作階段」，事件工作階段有時簡稱為「工作階段」。 <br/> <br/> 如需事件工作階段的進一步詳細資訊，請參閱︰[SQL Server 擴充事件工作階段](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)。 |
| event | 使用中的事件工作階段在系統中監看的特定項目。 <br/> <br/> 例如， *sql_statement_completed* 事件代表任何指定 T-SQL 陳述式完成的時間點。 此事件會報告其持續時間和其他資料。 |
| 目標 | 從所擷取的事件接收輸出資料的項目。 此目標會向您顯示資料。 <br/> <br/> 範例包括 *event_file*，以及其好用的輕量型類似項目 *ring_buffer* 記憶體。 較複雜的「長條圖」目標會對您的資料先執行一些處理，再向您顯示。 <br/> <br/> 任何目標都可以用於任何事件工作階段。 如需詳細資訊，請參閱 [Targets for Extended Events in SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md)(SQL Server 的擴充事件目標)。 |
| action | 事件已知的欄位。 此欄位中的資料會傳送至目標。 [動作] 欄位與「述詞篩選條件」密切相關。 |
| 述詞篩選條件 | 事件欄位中的資料測試，以此方式使用時，只會將相關事件項目子集傳送至目標。 <br/> <br/> 例如，篩選可以只包含 *sql_statement_completed* 事件項目，其中 T-SQL 陳述式內含字串 *HAVING*。 |
| 封裝 | 附加至一組項目中每個項目的名稱限定詞，此限定詞是以事件核心為主。 <br/> <br/> 例如，封裝可能會有 T SQL 文字的相關事件。 一個事件可以與 GO 分隔批次中的所有 T-SQL 相關。 同時有另一個範圍較小的事件與個別 T-SQL 陳述式相關。 此外，任何一個 T-SQL 陳述式都會有開始和完成的事件。 <br/> <br/> 事件的適當欄位也會與事件一起封裝。 大多數目標會在 *package0* 中，並可搭配許多其他封裝中的事件使用。 |


## <a name="how-to-discover-the-available-events-in-packages"></a>如何探索封裝中可用的事件


下列 T-SQL SELECT 會針對每個可用的事件傳回一個資料列，其名稱包含三個字元字串 'sql'。 當然，您可以編輯 LIKE 值來搜尋不同的事件名稱。 這些資料列也會命名包含事件的封裝。


```sql
SELECT   -- Find an event you want.
        p.name         AS [Package-Name],
        o.object_type,
        o.name         AS [Object-Name],
        o.description  AS [Object-Descr],
        p.guid         AS [Package-Guid]
    FROM
              sys.dm_xe_packages  AS p
        JOIN  sys.dm_xe_objects   AS o
    
                ON  p.guid = o.package_guid
    WHERE
        o.object_type = 'event'   --'action'  --'target'
        AND
        p.name LIKE '%'
        AND
        o.name LIKE '%sql%'
    ORDER BY
        p.name, o.object_type, o.name;
```


下列畫面顯示傳回的資料列，在此處已經過編輯，使用「資料行名稱 = 值」格式。 此資料來自上述範例步驟中所使用的 *sql statement_completed* 事件。 Object-Descr 資料行的句子特別有用。


```  
Package-Name = sqlserver
object_type  = event
Object-Name  = sql_statement_completed
Object-Descr = Occurs when a Transact-SQL statement has completed.
Package-Guid = 655FD93F-3364-40D5-B2BA-330F7FFB6491
```


#### <a name="ssms-ui-for-search"></a>使用 SSMS UI 進行搜尋


另一個搜尋選項是使用 SSMS UI 中的 [新增工作階段] > [事件] > [事件程式庫] 對話方塊，如上述螢幕擷取畫面所示。



#### <a name="sql-trace-event-classes-with-extended-events"></a>SQL 追蹤事件類別與擴充事件


如需搭配 SQL 追蹤事件類別和資料行使用擴充事件的說明，請參閱︰ [檢視同等於 SQL 追蹤事件類別的擴充事件項目](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)



#### <a name="event-tracing-for-windows-etw-with-extended-events"></a>Windows 事件追蹤 (ETW) 與擴充事件


如需搭配 Windows 事件追蹤 (ETW) 使用擴充事件的說明，請參閱：

- [Windows 事件追蹤目標](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [使用擴充事件監視系統活動](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)



ETW 事件不適用於 Azure SQL Database 上的擴充事件。



## <a name="additional-items"></a>其他項目


本節簡短提到一些其他項目。


### <a name="event-sessions-installed-with-sql-server"></a>SQL Server 隨附安裝的事件工作階段


SQL Server 中已建立一些擴充事件。 所有事件都已設定為在啟動 SQL 系統時開始。 這些事件工作階段所收集的資料可在發生系統錯誤時提供協助。 如同所有擴充事件，這些事件只會取用極少的資源，因此 Microsoft 建議保持執行這些事件。

您會在 SSMS 物件總管中的 [管理] > [擴充事件] > [工作階段] 下，看到這些事件工作階段。  自 2016年 6 月起，這些已安裝的事件工作階段清單如下：

- AlwaysOn_health
- system_health
- telemetry_events



### <a name="powershell-provider-for-extended-events"></a>擴充事件的 PowerShell 提供者


您可以使用 SQL Server PowerShell 提供者來管理 SQL Server 擴充事件。 詳情請參閱： [針對擴充事件使用 PowerShell 提供者](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)


### <a name="system-views-for-extended-events"></a>擴充事件的系統檢視表


擴充事件的系統檢視表包括：

- 目錄檢視：了解有關 CREATE EVENT SESSION 所定義之事件工作階段的相關資訊。

- 動態管理檢視 (DMV)：了解有關目前執行中之事件工作階段的相關資訊。


[SQL Server 擴充事件系統檢視表中的 SELECT 和 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) - 提供下列相關資訊：


- 如何彼此聯結檢視。


- 檢視中幾個實用的 SELECT。


- 下列項目之間的相互關聯：
    - 檢視資料行。
    - CREATE EVENT SESSION 子句。
    - SSMS UI 控制項。


<a name="appendix1"></a>
## <a name="appendix-selects-to-ascertain-permission-owner-in-advance"></a>附錄︰使用 SELECT 事先確認權限擁有者


本文中提到的權限包括：

- ALTER ANY EVENT SESSION
- VIEW SERVER STATE
- CONTROL SERVER

下列 Transact-SQL SELECT 陳述式可報告哪些人員具有這些權限。


#### <a name="union-direct-permissions-plus-role-derived-permissions"></a>UNION 直接權限，加上角色衍生的權限


下列 SELECT...UNION ALL 陳述式會傳回資料列，顯示哪些人員具有建立事件工作階段，以及查詢系統目錄檢視中的擴充事件時所需的權限。


```sql
-- Ascertain who has the permissions listed in the ON clause.
-- 'CONTROL SERVER' permission includes the permissions
-- 'ALTER ANY EVENT SESSION' and 'VIEW SERVER STATE'.
SELECT
        'Owner-is-Principal'  AS [Type-That-Owns-Permission],
        NULL                  AS [Role-Name],
        prin.name             AS [Owner-Name],

        perm.permission_name
            COLLATE Latin1_General_CI_AS_KS_WS
            AS [Permission-Name]
    FROM
             sys.server_permissions  AS perm
        JOIN sys.server_principals   AS prin

            ON prin.principal_id = perm.grantee_principal_id
    WHERE
        perm.permission_name IN
            ('ALTER ANY EVENT SESSION',
            'VIEW SERVER STATE',
            'CONTROL SERVER')
UNION ALL

-- Plus check for members of the 'sysadmin' fixed server role,
-- because 'sysadmin' includes the 'CONTROL SERVER' permission.
SELECT
        'Owner-is-Role',
        prin.name,  -- [Role-Name]

        CAST( (IsNull(pri2.name, N'No members'))
            AS nvarchar(128)),

        NULL
    FROM
                         sys.server_role_members  AS rolm
        RIGHT OUTER JOIN sys.server_principals    AS prin

            ON prin.principal_id = rolm.role_principal_id

        LEFT OUTER JOIN sys.server_principals     AS pri2

            ON rolm.member_principal_id = pri2.principal_id
    WHERE
        prin.name = 'sysadmin'
    ORDER BY
        1,2,3,4;
```


#### <a name="haspermsbyname-function"></a>HAS_PERMS_BY_NAME 函數


下列 SELECT 會報告您的權限。 它需要內建函數 [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md)。

此外，如果您有權暫時「模擬」其他帳戶，您可以取消註解 [EXECUTE AS LOGIN](../../t-sql/statements/execute-as-transact-sql.md) 及 REVERT 陳述式，以查詢其他帳戶。


```sql
--EXECUTE AS LOGIN = 'AccountNameHere';
SELECT HAS_PERMS_BY_NAME(
    null, null,
    'ALTER ANY EVENT SESSION'
    );
--REVERT;
```


#### <a name="security-links"></a>安全性連結

以下是與這些 SELECT 和權限相關的文件連結：

- 內建函數 [HAS_PERMS_BY_NAME (TRANSACT-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)的詳細資料
- [sys.fn_my_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
- [GRANT 伺服器權限 (Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)
- [sys.server_principals (Transact-SQL)](http://msdn.microsoft.com/library/ms188786.aspx)
- [sys.database_principals (Transact-SQL)](http://msdn.microsoft.com/library/ms187328.aspx)(特別針對 Azure SQL Database)
- 部落格︰ [Effective Database Engine Permissions](http://social.technet.microsoft.com/wiki/contents/articles/15180.effective-database-engine-permissions.aspx)(有效的 Database Engine 權限)
- 可縮放的 PDF 格式 [海報](https://aka.ms/sql-permissions-poster)，顯示所有 SQL Server 權限的階層。



## <a name="links-to-supporting-information"></a>支援資訊的連結


- [sys.fn_xe_file_target_read_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)


