---
title: 使用查詢編輯器建立擴充事件會話 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a541c86029be9a438492a851c0eb16d18120f75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065024"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>使用查詢編輯器建立擴充事件工作階段
  您可以使用查詢編輯器來建立擴充事件工作階段，也可以在物件總管中建立工作階段。 在物件總管中，擴充事件提供兩個使用者介面，您可以用來建立、修改及查看事件會話資料，此嚮導會引導您完成事件會話的建立程式，以及提供更多更先進設定選項的新會話 UI。 您可以建立擴充事件工作階段來診斷 SQL Server 追蹤，以便解決下列問題：  
  
-   尋找最費時的查詢  
  
-   尋找導致閂鎖競爭的根本原因  
  
-   尋找封鎖其他查詢的查詢  
  
-   疑難排解因重新編譯查詢所致的過度使用 CPU 的問題  
  
-   疑難排解死結  
  
 如需如何使用 [新增工作階段精靈] 建立擴充事件工作階段的相關資訊，請參閱[使用精靈建立擴充事件工作階段 &#40;物件總管&#41;](../ssms/object/object-explorer.md)。 如需如何使用 [新增工作階段] UI 建立擴充事件工作階段的相關資訊，請參閱 [Quick Start: Extended events in SQL Server](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md) (快速入門：SQL Server擴充事件)。  
  
##  <a name="BeforeYouBegin"></a> 權限  
 若要建立「擴充事件」工作階段，您必須擁有 ALTER ANY EVENT SESSION 權限。  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>使用查詢編輯器建立擴充事件工作階段  
  
#### <a name="to-create-an-extended-events-session"></a>若要建立擴充事件工作階段  
  
1.  下列程序示範如何在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中使用查詢編輯器來建立「擴充事件」工作階段。  
  
     決定您想要在工作階段中使用的事件。 若要查看所有可用的事件，連同關鍵字與通道，請使用下列查詢：  
  
    > [!NOTE]  
    >  如需關鍵字和通道的相關資訊，請參閱 [SQL Server 擴充事件封裝](../relational-databases/extended-events/sql-server-extended-events-packages.md)。  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  在新的查詢視窗中，加入下列陳述式來建立事件工作階段，以您想要使用的工作階段名稱來取代 *session_name* 。  
  
    > [!IMPORTANT]  
    >  這個程序的步驟 2 到 6 會描述事件工作階段定義的每個區段。 在執行之前，您會將所有陳述式加入到單一查詢視窗。 如需完整範例，請參閱本主題的＜範例＞一節。  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  使用以下格式加入您想要監視的事件： *package_name*.*event_name*。 針對每個事件，加入與下列相似的一行：  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     例如：  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (選擇性) 加入事件之後，您可以加入要採取的動作。 您也可以加入述詞。 述詞是用來建立目標何時應該耗用事件資訊的準則。 動作是使用 ACTION 子句加入，而述詞則是使用 WHERE 子句加入。 例如，若要加入動作和述詞，其中 [!INCLUDE[tsql](../includes/tsql-md.md)] 文字是針對 sqlserver.file_read_completed 事件所擷取，且檔案識別碼等於 1，您可以包含下列陳述式：  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   若要檢視有哪些動作可用，請使用下列查詢：  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   若要檢視哪些述詞可供事件使用，請使用下列查詢，以您想要加入述詞的事件名稱取代 *event_name* ：  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         例如：  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         請注意，您也可以加入全域述詞來源。 全域述詞來源可在任何述詞運算式中使用。 若要檢視有哪些全域述詞來源可用，請使用下列查詢：  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         例如，您可以使用下列述詞運算式指定，在某個事件發生前五次時，才應該收集此事件的資料。  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  加入所要的目標，其中將會處理及耗用事件資料。 請使用下列格式：  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     下列範例會加入非同步檔案目標：  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     若要檢視可用目標的清單，請使用下列查詢：  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  如需不同目標類型的相關資訊，請參閱 [SQL Server 擴充的事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)。  
  
6.  檢閱並加入任何其他組態選項。 例如，您可以設定選項，例如事件保留模式、事件在記憶體中緩衝處理多久，或是當 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 啟動時事件工作階段是否應該自動啟動。 
  [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql) 主題會描述這些選項。 請注意，如果未指定這些選項，就會指派預設值。  
  
7.  啟動工作階段。  
  
    > [!NOTE]  
    >  如需有關如何檢視工作階段結果的詳細資訊，請參閱您在《線上叢書》的 [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md) (SQL Server 擴充事件目標) 節點中所使用之目標類型的對應主題。  
  
 下列範例會建立名為 IOActivity 的「擴充事件」工作階段來擷取下列資訊：  
  
-   已完成檔案讀取的事件資料，包括檔案讀取的相關 [!INCLUDE[tsql](../includes/tsql-md.md)] 文字，其中檔案識別碼等於 1。  
  
-   已完成檔案寫入的事件資料。  
  
-   當資料從記錄檔快取寫入實體記錄檔時的事件資料。  
  
 工作階段會將輸出傳送到檔案目標。  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [SQL Server 擴充的事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [SQL Server 擴充的事件套件](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
