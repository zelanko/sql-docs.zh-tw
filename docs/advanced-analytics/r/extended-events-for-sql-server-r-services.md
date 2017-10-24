---
title: "SQL Server R Services 的擴充事件 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4e90e057-aacb-4adc-8da6-64861f4e87df
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 814dacf2dbc7f3be05ad163c8c7162acf53fe404
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="extended-events-for-sql-server-r-services"></a>SQL Server R 服務的擴充事件
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 提供一組擴充事件，以供在與 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 或傳送至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之 R 作業相關的疑難排解操作中使用。  
  
 若要檢視 SQL Server 相關事件的清單，請從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行以下查詢。  
  
```  
select o.name as event_name, o.description  
  from sys.dm_xe_objects o  
  join sys.dm_xe_packages p  
    on o.package_guid = p.guid  
 where o.object_type = 'event'  
   and p.name = 'SQLSatellite';  
```  
  
 不過，某些額外的 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 擴充事件只會從外部處理序引發，像是 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]和 BXLServer (啟動 R 執行階段的附屬處理序)。 如需有關如何擷取這些事件的詳細資訊，請參閱 [Collecting Events from External Processes](#bkmk_externalevents)。  
  
 如需有關使用擴充事件的一般資訊，請參閱 [SQL Server Extended Events Sessions](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)。  

  
##  <a name="bkmk_xeventtable"></a> 擴充事件列表  
  
|事件|描述|使用|  
|-----------|-----------------|---------|  
|connection_accept|接受新連線時會發生。 此事件是用來記錄所有的連線嘗試。||  
|failed_launching|啟動失敗。|表示發生錯誤。|  
|satellite_abort_connection|中止連接記錄||  
|satellite_abort_received|透過附屬連線收到中止訊息時引發。||  
|satellite_abort_sent|透過附屬連線傳送中止訊息時引發。||  
|satellite_authentication_completion|完成透過 TCP 或 Namedpipe 連線的驗證時引發。||  
|satellite_authorization_completion|完成透過 TCP 或 Namedpipe 連線的授權時引發。||  
|satellite_cleanup|清除附屬呼叫時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_data_chunk_sent|附屬連線完成傳送單一資料區塊時引發。|事件會回報已傳送的資料列數、資料行數、已使用的 SNI 封包數，以及傳送區塊時所經過的時間 (以毫秒為單位)。 此資訊可協助您了解傳送不同類型的資料花費多少時間，以及使用多少封包。|  
|satellite_data_receive_completion|透過附屬連線收到查詢要求的所有資料時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_data_send_completion|透過附屬連線傳送工作階段要求的所有資料時引發。||  
|satellite_data_send_start|開始資料傳輸時 (在傳送第一個資料區塊前) 引發。||  
|satellite_error|用來追蹤 SQL 附屬錯誤||  
|satellite_invalid_sized_message|訊息的大小無效||  
|satellite_message_coalesced|用來追蹤網路層的訊息聯合||  
|satellite_message_ring_buffer_record|訊息信號緩衝區記錄||  
|satellite_message_summary|訊息傳遞的相關摘要資訊||  
|satellite_message_version_mismatch|訊息的版本欄位不相符||  
|satellite_messaging|用來追蹤訊息事件 (繫結、解除繫結等)||  
|satellite_partial_message|用來追蹤網路層的部分訊息||  
|satellite_schema_received|在 SQL 收到並讀取結構描述訊息時引發。||  
|satellite_schema_sent|透過附屬處理序傳送結構描述訊息時引發。|只會從外部處理序引發。 檢視從外部處理序收集事件的指示。|  
|satellite_service_start_posted|在服務啟動訊息張貼到啟動控制板時引發。|這會通知啟動控制板啟動外部處理序，且其中包含新工作階段的識別碼。|  
|satellite_unexpected_message_received|收到非預期的訊息時引發。|表示發生錯誤。|  
|stack_trace|在要求處理序的記憶體傾印時發生。|表示發生錯誤。|  
|trace_event|用來進行追蹤|這些事件可以包含 SQL Server、啟動控制板和外部處理序追蹤訊息。 包含從 R 輸出至 stdout 和 stderr。|  
|launchpad_launch_start|啟動板開始啟動附屬處理序時引發。|只能從啟動控制板引發。 檢視從 launchpad.exe 收集事件的指示。|  
|launchpad_resume_sent|啟動控制板啟動附屬處理序並將繼續訊息傳送至 SQL Server 時引發。|只能從啟動控制板引發。 檢視從 launchpad.exe 收集事件的指示。|  
|satellite_data_chunk_sent|附屬連線完成傳送單一資料區塊時引發。|包含有關資料行數目、資料列數目、封包數目及傳送區塊所經過之時間的資訊。|  
|satellite_sessionId_mismatch|非預期的訊息工作階段識別碼||  
  
###  <a name="bkmk_externalevents"></a> Collecting Events from External Processes  
 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 會啟動一些在 SQL Server 處理序外執行的服務。 若要擷取這些外部處理序的相關事件，您必須建立事件追蹤組態檔，並將該檔案放在處理序可執行檔所在的相同目錄中。  
  
-   **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
     若要擷取與 Launchpad 相關的事件，請將 *.config* 檔案放在 SQL Server 執行個體的 Binn 目錄中。  在預設的安裝中，這會是：`C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`。  
  
-   **BXLServer** 是支援 SQL 搭配 R 及其他外部指令碼語言之擴充性的附屬處理序。  
  
     若要擷取與 BXLServer 相關的事件，請將 *.config* 檔案放在 R 安裝目錄中。  在預設的安裝中，這會是：`C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`。  
  
> [!IMPORTANT]
>   組態檔必須以此格式 “[名稱].xevents.xml” 命名為和可執行檔相同的名稱。 也就是說，檔案必須用以下的格式命名︰  
>   
> - Launchpad.xevents.xml  
> - bxlserver.xevents.xml  
  
 組態檔本身的格式如下：  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   若要設定追蹤，請編輯 *session name* 預留位置、檔案名稱的預留位置 (`[SessionName].xel`)，以及您想要擷取之事件的名稱 (例如 `[XEvent Name 1]`、`[XEvent Name 1]`)。  
  
-   可以出現任意數量的 `event package` 標籤，而只要 name 屬性正確就會進行收集。  
  
### <a name="example-capturing-launchpad-events"></a>範例：擷取啟動控制板事件  
 以下範例說明啟動控制板服務之事件追蹤的定義。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   將 *.config* 檔案放在 SQL Server 執行個體的 Binn 目錄中。  
  
-   這個檔案必須命名為 *Launchpad.xevents.xml*。  
  
### <a name="example-capturing-bxlserver-events"></a>範例：擷取 BXLServer 事件  
 以下範例顯示 BXLServer 可執行檔的事件追蹤。  
  
```  
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
  
```  
  
 **注意：**  
  
-   將 *.config* 檔案放在 BXLServer 可執行檔所在的相同目錄中。  
  
-   這個檔案必須命名為 *bxlserver.xevents.xml*。  
  
## <a name="see-also"></a>另請參閱
[自訂 R Services 的 Management Studio 報表](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [管理和監視 R 方案](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md)  
  
  

