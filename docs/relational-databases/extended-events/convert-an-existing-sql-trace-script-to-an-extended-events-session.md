---
title: 將現有的 SQL 追蹤指令碼轉換為擴充事件工作階段 | Microsoft 文件
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace, convert script to extended events
- extended events [SQL Server], convert SQL Trace script
ms.assetid: 4c8f29e6-0a37-490f-88b3-33493871b3f9
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 894818a0311d9a7f85c8991702bb924e12a67276
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32938183"
---
# <a name="convert-an-existing-sql-trace-script-to-an-extended-events-session"></a>將現有的 SQL 追蹤指令碼轉換為擴充事件工作階段
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  如果您有現有的 SQL 追蹤指令碼想要轉換成「擴充事件」工作階段，您可以使用本主題的程序建立同等的「擴充事件」工作階段。 您可以藉由使用 trace_xe_action_map 和 trace_xe_event_map 系統資料表中的資訊來收集執行轉換所必須擁有的資訊。  
  
 這些步驟包含以下內容：  
  
1.  執行現有的指令碼來建立 SQL 追蹤工作階段，然後取得追蹤的識別碼。  
  
2.  執行使用 fn_trace_geteventinfo 函數的查詢，以便在同等的「擴充事件」事件和動作中，找出每一個「SQL 追蹤」事件類別以及其關聯的資料行。  
  
3.  使用 fn_trace_getfilterinfo 函數可列出要使用的篩選以及同等的「擴充事件」動作。  
  
4.  使用同等的「擴充事件」事件、動作和述詞 (篩選器) 手動建立「擴充事件」工作階段。  
  
## <a name="to-obtain-the-trace-id"></a>若要取得追蹤識別碼  
  
1.  在查詢編輯器中開啟 SQL 追蹤指令碼，並執行此指令碼來建立追蹤工作階段。 請注意，不需要執行追蹤工作階段也可完成此程序。  
  
2.  取得追蹤的識別碼。 若要這樣做，請使用下列查詢：  
  
    ```  
    SELECT * FROM sys.traces;  
    GO  
    ```  
  
    > [!NOTE]  
    >  追蹤識別碼 1 通常表示預設追蹤。  
  
## <a name="to-determine-the-extended-events-equivalents"></a>若要判斷擴充事件同等項目  
  
1.  若要判斷同等的「擴充事件」事件和動作，請執行下列查詢，其中 *trace_id* 設定為您在上一個程序中取得之追蹤識別碼的值。  
  
    > [!NOTE]  
    >  在這個範例中，將會使用預設追蹤的追蹤識別碼 (1)。  
  
    ```  
    USE MASTER;  
    GO  
    DECLARE @trace_id int;  
    SET @trace_id = 1;  
    SELECT DISTINCT el.eventid, em.package_name, em.xe_event_name AS 'event'  
       , el.columnid, ec.xe_action_name AS 'action'  
    FROM (sys.fn_trace_geteventinfo(@trace_id) AS el  
       LEFT OUTER JOIN sys.trace_xe_event_map AS em  
          ON el.eventid = em.trace_event_id)  
    LEFT OUTER JOIN sys.trace_xe_action_map AS ec  
       ON el.columnid = ec.trace_column_id  
    WHERE em.xe_event_name IS NOT NULL AND ec.xe_action_name IS NOT NULL;  
    ```  
  
     將會傳回同等的「擴充事件」事件識別碼、封裝名稱、事件名稱、資料行識別碼和動作名稱。 您將會在本主題稍後的＜若要建立擴充事件工作階段＞程序中使用這個輸出。  
  
     在某些情況下，篩選的資料行會對應到事件資料欄位，預設會將此欄位併入「擴充事件」事件內。 因此，"Extended_Events_action_name" 資料行將會是 NULL。 如果發生這種情況，您必須執行下列動作，以判斷哪一個資料欄位相當於篩選的資料行：  
  
    1.  如果是傳回 NULL 的動作，請識別指令碼中有哪一個 SQL 追蹤事件類別包含正在篩選的資料行。  
  
         例如，您可能已經使用 SP:StmtCompleted 事件類別，並在 Duration 追蹤資料行名稱 (SQL 追蹤事件類別識別碼 45 和 SQL 追蹤資料行識別碼 13) 上指定篩選。 在此情況下，動作名稱會以 NULL 形式出現在查詢結果中。  
  
    2.  針對您在上一個步驟所識別的每個 SQL 追蹤事件類別，尋找同等的「擴充事件」事件名稱 (如果您不確定同等的事件名稱，請使用 [檢視同等於 SQL 追蹤事件類別的擴充事件項目](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)主題中的查詢)。  
  
    3.  使用下列查詢來識別正確的資料欄位，這些欄位用於您在上一個步驟所識別的事件。 此查詢會在 "event_field" 資料行中顯示「擴充事件」資料欄位。 在此查詢中，使用您在上一個步驟所指定的事件名稱來取代 <事件名稱>。  
  
        ```  
        SELECT xp.name package_name, xe.name event_name  
           ,xc.name event_field, xc.description  
        FROM sys.trace_xe_event_map AS em  
        INNER JOIN sys.dm_xe_objects AS xe  
           ON em.xe_event_name = xe.name  
        INNER JOIN sys.dm_xe_packages AS xp  
           ON xe.package_guid = xp.guid AND em.package_name = xp.name  
        INNER JOIN sys.dm_xe_object_columns AS xc  
           ON xe.name = xc.object_name  
        WHERE xe.object_type = 'event' AND xc.column_type <> 'readonly'  
           AND em.xe_event_name = '<event_name>';  
        ```  
  
         例如，SP:StmtCompleted 事件類別會對應到 sp_statement_completed「擴充事件」事件。 如果您指定 sp_statement_completed 當作查詢中的事件名稱，則 "event_field" 資料行會顯示預設隨附在事件中的欄位。 查看欄位時，可以看到「持續時間」欄位。 若要在同等的「擴充事件」工作階段中建立篩選器，您可加入類似 "WHERE duration > 0" 的述詞。 如需範例，請參閱本主題的＜若要建立擴充事件工作階段＞程序。  
  
## <a name="to-create-the-extended-events-session"></a>若要建立擴充事件工作階段  
 使用查詢編輯器建立「擴充事件」工作階段，並將輸出寫入檔案目標。 下列步驟說明單一查詢，連同示範如何建立查詢的說明。 如需完整查詢範例，請參閱本主題的＜範例＞一節。  
  
1.  加入陳述式來建立事件工作階段，使用您想要用於「擴充事件」工作階段的名稱來取代*session_name* 。  
  
    ```  
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [Session_Name] ON SERVER;  
    CREATE EVENT SESSION [Session_Name]  
    ON SERVER;  
    ```  
  
2.  加入在＜若要判斷擴充事件同等項目＞程序中當做輸出傳回的「擴充事件」事件和動作，並加入您在＜若要判斷指令碼中所使用的篩選器＞程序中所識別的述詞 (篩選器)。  
  
     下列範例會使用 SQL 追蹤指令碼，其中包含 SQL:StmtStarting 和 SP:StmtCompleted 事件類別，連同工作階段識別碼和持續時間的篩選器。 ＜若要判斷擴充事件同等項目＞程序中的查詢範例輸出傳回下列結果集：  
  
    ```  
    Eventid  package_name  event                   columnid  action  
    44       sqlserver     sp_statement_starting   6         nt_username  
    44       sqlserver     sp_statement_starting   9         client_pid  
    44       sqlserver     sp_statement_starting   10        client_app_name  
    44       sqlserver     sp_statement_starting   11        server_principal_name  
    44       sqlserver     sp_statement_starting   12        session_id  
    45       sqlserver     sp_statement_completed  6         nt_username  
    45       sqlserver     sp_statement_completed  9         client_pid  
    45       sqlserver     sp_statement_completed  10        client_app_name  
    45       sqlserver     sp_statement_completed  11        server_principal_name  
    45       sqlserver     sp_statement_completed  12        session_id  
    ```  
  
     若要將這個項目轉換成「擴充事件」同等項目，則會加入 sqlserver.sp_statement_starting 和 sqlserver.sp_statement_completed 事件，連同動作清單。 包含述詞陳述式當做 WHERE 子句。  
  
    ```  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
          (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
          )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       )  
    ```  
  
3.  新增非同步檔案目標，使用您想要儲存輸出的位置來取代檔案路徑。 當您指定檔案目標時，您必須包含記錄檔和中繼資料檔案路徑檔案。  
  
    ```  
    ADD TARGET package0.asynchronous_file_target(  
       SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="to-view-the-results"></a>若要檢視結果  
  
1.  您可以使用 sys.fn_xe_file_target_read_file 函數來檢視輸出。 若要這樣做，請執行下列查詢，使用您指定的路徑來取代檔案路徑：  
  
    ```  
    SELECT *, CAST(event_data as XML) AS 'event_data_XML'  
    FROM sys.fn_xe_file_target_read_file('c:\temp\ExtendedEventsStoredProcs*.xel', 'c:\temp\ExtendedEventsStoredProcs*.xem', NULL, NULL);  
  
    ```  
  
    > [!NOTE]  
    >  將事件資料轉換為 XML 是選擇性的動作。  
  
     如需 sys.fn_xe_file_target_read_file 函數的詳細資訊，請參閱 [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)。  
  
    ```  
    IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
       DROP EVENT SESSION [session_name] ON SERVER;  
    CREATE EVENT SESSION [session_name]  
    ON SERVER  
  
    ADD EVENT sqlserver.sp_statement_starting  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59   
       ),  
  
    ADD EVENT sqlserver.sp_statement_completed  
       (ACTION  
       (  
          sqlserver.nt_username,  
          sqlserver.client_pid,  
          sqlserver.client_app_name,  
          sqlserver.server_principal_name,  
          sqlserver.session_id  
       )  
       WHERE sqlserver.session_id = 59 AND duration > 0  
       );  
  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
    ```  
  
## <a name="example"></a>範例  
  
```  
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='session_name')  
   DROP EVENT SESSION [session_name] ON SERVER;  
CREATE EVENT SESSION [session_name]  
ON SERVER  
  
ADD EVENT sqlserver.sp_statement_starting  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59   
   ),  
  
ADD EVENT sqlserver.sp_statement_completed  
   (ACTION  
   (  
      sqlserver.nt_username,  
      sqlserver.client_pid,  
      sqlserver.client_app_name,  
      sqlserver.server_principal_name,  
      sqlserver.session_id  
   )  
   WHERE sqlserver.session_id = 59 AND duration > 0  
   )  
  
ADD TARGET package0.asynchronous_file_target  
   (SET filename='c:\temp\ExtendedEventsStoredProcs.xel', metadatafile='c:\temp\ExtendedEventsStoredProcs.xem');  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視同等於 SQL 追蹤事件類別的擴充事件項目](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)  
  
  
