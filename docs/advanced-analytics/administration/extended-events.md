---
title: 使用擴充事件監視指令碼
description: 了解如何使用擴充事件來監視與 SQL Server 機器學習服務、SQL Server Launchpad 和 Python 或 R 作業外部指令碼相關的操作及針對其進行疑難排解。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/04/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cf0253788e19061fe54b8e2b0b8dfd3142856472
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78335734"
---
# <a name="monitor-python-and-r-scripts-with-extended-events-in-sql-server-machine-learning-services"></a>使用 SQL Server 機器學習服務中的擴充事件來監視 Python 與 R 指令碼
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

了解如何使用擴充事件來監視與 SQL Server 機器學習服務、SQL Server Launchpad 和 Python 或 R 作業外部指令碼相關的操作及針對其進行疑難排解。

## <a name="extended-events-for-sql-server-machine-learning-services"></a>SQL Server 機器學習服務的擴充事件

若要檢視與 SQL Server 機器學習服務相關的事件清單，請從 Azure Data Studio 或 SQL Server Management Studio 執行下列查詢。

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

如需有關如何使用擴充事件的詳細資訊，請參閱[擴充事件工具](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools)。

## <a name="additional-events-specific-to-machine-learning-services"></a>機器學習服務的特定額外事件

額外擴充事件可供與 SQL Server 機器學習服務相關並由其使用的元件 (例如 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]、BXLServer，以及啟動 Python 或 R 執行階段的附屬處理序) 使用。 這些額外擴充事件是從外部處理序引發的；因此，您必須使用外部公用程式來加以擷取。

如需有關如何執行此動作的詳細資訊，請參閱[從外部處理序收集事件](#bkmk_externalevents)一節。

<a name="bkmk_xeventtable"></a> 

## <a name="table-of-extended-events"></a>擴充事件表

|事件|描述|注意|  
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
|satellite_data_send_start|在資料傳輸開始時引發。| 在資料傳輸開始時 (在傳送第一個資料區塊前) 引發。|  
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

<a name="bkmk_externalevents"></a>

### <a name="collecting-events-from-external-processes"></a>從外部處理序收集事件

SQL Server 機器學習服務會啟動一些在 SQL Server 處理序外執行的服務。 若要擷取這些外部處理序的相關事件，您必須建立事件追蹤組態檔，並將該檔案放在處理序可執行檔所在的相同目錄中。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!IMPORTANT]
> 從 SQL Server 2019 開始，隔離機制已經變更。 因此您必須授與事件追蹤設定檔所在目錄的適當權限。 如需有關如何設定這些權限的詳細資訊，請參閱 [Windows 上 SQL Server 2019 中的檔案權限區段：機器學習服務的隔離變更](../install/sql-server-machine-learning-services-2019.md#file-permissions)
::: moniker-end

+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    若要擷取與 Launchpad 相關的事件，請將 *.xml* 檔案放在 SQL Server 執行個體的 Binn 目錄中。 在預設的安裝中，這會是：

    第 1 課：建立 Windows Azure 儲存體物件`C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`。  
  
+ **BXLServer** 是支援 SQL 擴充性搭配外部指令碼語言 (例如 R 或 Python) 的附屬處理序。 會針對每個外部語言執行個體啟動個別的 BxlServer 執行個體。
  
    若要擷取與 BXLServer 相關的事件，請將 *.xml* 檔案放在 R 或 Python 安裝目錄中。 在預設的安裝中，這會是：
     
    **R：** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`。  

    **Python：** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`。

組態檔必須以 "[名稱].xevents.xml" 格式命名為和可執行檔相同的名稱。 也就是說，檔案必須用以下的格式命名︰

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

組態檔本身的格式如下：

```xml
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

+ 若要設定追蹤，請編輯 *session name* 預留位置、檔案名稱的預留位置 (`[SessionName].xel`)，以及您想要擷取之事件的名稱 (例如 `[XEvent Name 1]`、`[XEvent Name 1]`)。  
+ 可出現任意數目的 <event package> 標籤，而且只要 name 屬性正確就會進行收集。

### <a name="example-capturing-launchpad-events"></a>範例：擷取 Launchpad 事件

下列範例說明 Launchpad 服務之事件追蹤的定義：

```xml
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

+ 將 *.xml* 檔案放在 SQL Server 執行個體的 Binn 目錄中。
+ 此檔案必須命名為 `Launchpad.xevents.xml`。

### <a name="example-capturing-bxlserver-events"></a>範例：擷取 BXLServer 事件  

以下範例顯示 BXLServer 可執行檔的事件追蹤。
  
```xml
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

+ 將 *.xml* 檔案放在 BXLServer 可執行檔所在的相同目錄中。
+ 此檔案必須命名為 `bxlserver.xevents.xml`。

## <a name="next-steps"></a>後續步驟

- [使用 SQL Server Management Studio 中的自訂報表監視 Python 與 R 指令碼執行](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [使用動態管理檢視 (DMV) 監視 SQL Server 機器學習服務](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
