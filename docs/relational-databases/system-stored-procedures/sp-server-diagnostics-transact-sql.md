---
title: (transact-sql) |Microsoft 文件
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_server_diagnostics
- sp_server_diagnostics_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_diagnostics
ms.assetid: 62658017-d089-459c-9492-c51e28f60efe
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a3bd7cf97a37e2e01cb1d593ee1370c3d5430162
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spserverdiagnostics-transact-sql"></a>sp_server_diagnostics (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

擷取有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的診斷資料和健全狀況資訊，以偵測潛在的失敗。 此程序會以重複模式執行，並定期傳送結果。 它可以從一般或 DAC 連接來叫用。  
  
**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_server_diagnostics [@repeat_interval =] 'repeat_interval_in_seconds'   
```  
  
## <a name="arguments"></a>引數  
 [ **@repeat_interval** =] **'***repeat_interval_in_seconds***'**  
 表示預存程序會重複執行以傳送健全狀況資訊的時間間隔。  
  
 *repeat_interval_in_seconds*是**int**與預設值是 0。 有效的參數值是 0，或等於或大於 5 的任何值。 預存程序必須至少執行 5 秒，才能傳回完整資料。 預存程序以重複模式執行的最小值為 5 秒。  
  
 如果沒有指定這個參數，或指定的值是 0，預存程序就會傳回資料一次並結束。  
  
 如果指定的值小於最小值，將會引發錯誤，而不傳回任何項目。  
  
 如果指定的值等於或大於 5，預存程序會重複執行以傳回健全狀態，直到手動取消為止。  
  
## <a name="return-code-values"></a>傳回碼值  
0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
**sp_server_diagnostics**會傳回下列資訊  
  
|資料行|資料類型|Description|  
|------------|---------------|-----------------|  
|**creation_time**|**datetime**|表示資料列建立的時間戳記。 單一資料列集的每個資料列都有相同的時間戳記。|  
|**component_type**|**sysname**|指出資料列是否包含資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體層級元件或 Alwayson 可用性群組：<br /><br /> 執行個體<br /><br /> Alwayson: AvailabilityGroup|  
|**元件 _ 名稱**|**sysname**|指出元件的名稱或可用性群組的名稱：<br /><br /> 系統<br /><br /> resource<br /><br /> query_processing<br /><br /> io_subsystem<br /><br /> 事件<br /><br /> *\<可用性群組的名稱 >*|  
|**狀態**|**int**|指出元件的健全狀態：<br /><br /> 0<br /><br /> 1<br /><br /> 2<br /><br /> 3|  
|**state_desc**|**sysname**|描述狀態資料行。 對應至狀態資料行值的描述如下：<br /><br /> 0： 未知<br /><br /> 1： 初始狀態<br /><br /> 2： 警告<br /><br /> 3： 錯誤|  
|**data**|**varchar (max)**|指定元件的相關資料。|  
  
 以下是五種元件的說明：  
  
-   **系統**： 從系統觀點來收集有關單一執行緒存取鎖、 嚴重處理條件、 沒有產量的工作、 分頁錯誤及 CPU 使用量資料。 這項資訊產生整體的健全狀態建議。  
  
-   **資源**： 從資源觀點來收集有關實體和虛擬記憶體，緩衝集區、 頁面、 快取和其他記憶體物件資料。 這項資訊產生整體的健全狀態建議。  
  
-   **query_processing**： 收集資料，從查詢處理觀點來看，在背景工作執行緒、 工作、 等候類型、 CPU 密集工作階段和封鎖的工作。 這項資訊產生整體的健全狀態建議。  
  
-   **io_subsystem**： 在 IO 上收集資料。 除了診斷資料之外，這個元件只產生 IO 子系統的乾淨良好或警告的健全狀態。  
  
-   **事件**： 收集資料並透過預存程序的介面上的錯誤和伺服器，包括有關信號緩衝區例外狀況詳細資料所記錄的感興趣的事件的信號緩衝區事件，以及有關記憶體 broker、 排程器監視器、 記憶體不足緩衝集區中，單一執行緒存取鎖、 安全性和連接。 事件永遠會顯示狀態 0。  
  
-   **\<可用性群組的名稱 >**： 收集指定的可用性群組的資料 (如果 component_type ="永遠上： AvailabilityGroup")。  
  
## <a name="remarks"></a>備註  
從失敗觀點來看，系統、資源和 query_processing 元件將會用於失敗偵測，而 io_subsystem 和事件元件只供診斷之用。  
  
下表將元件對應到其相關聯的健全狀態。  
  
|Components|乾淨 (1)|警告 (2)|錯誤 (3)|未知 (0) |  
|----------------|-----------------|-------------------|-----------------|--------------------|  
|系統|x|x|x||  
|resource|x|x|x||  
|query_processing|x|x|x||  
|io_subsystem|x|x|||  
|事件||||x|  
  
每個資料列中的 (x) 表示元件的有效健全狀態。 例如，io_subsystem 會顯示為乾淨或警告。 它不會顯示錯誤狀態。  
 
> [!NOTE]
> Sp_server_diagnostics 內部程序的執行是高優先順序的先佔式執行緒上實作。
  
## <a name="permissions"></a>Permissions  
需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="examples"></a>範例  
最佳作法是使用擴充的工作階段來擷取健全狀況資訊，並將它儲存到位於 SQL Server 之外的檔案。 因此，如果發生失敗，您仍然可以存取它。 下列範例會將事件工作階段的輸出儲存至檔案：  
```sql  
CREATE EVENT SESSION [diag]  
ON SERVER  
           ADD EVENT [sp_server_diagnostics_component_result] (set collect_data=1)  
           ADD TARGET [asynchronous_file_target] (set filename='c:\temp\diag.xel');  
GO  
ALTER EVENT SESSION [diag]  
      ON SERVER STATE = start;  
GO  
```  
  
以下的範例查詢會讀取擴充工作階段記錄檔：  
```sql  
SELECT  
    xml_data.value('(/event/@name)[1]','varchar(max)') AS Name  
  , xml_data.value('(/event/@package)[1]', 'varchar(max)') AS Package  
  , xml_data.value('(/event/@timestamp)[1]', 'datetime') AS 'Time'  
  , xml_data.value('(/event/data[@name=''component_type'']/value)[1]','sysname') AS Sysname  
  , xml_data.value('(/event/data[@name=''component_name'']/value)[1]','sysname') AS Component  
  , xml_data.value('(/event/data[@name=''state'']/value)[1]','int') AS State  
  , xml_data.value('(/event/data[@name=''state_desc'']/value)[1]','sysname') AS State_desc  
  , xml_data.query('(/event/data[@name="data"]/value/*)') AS Data  
FROM   
(  
      SELECT  
                        object_name as event  
                        ,CONVERT(xml, event_data) as xml_data  
       FROM    
      sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\*.xel', NULL, NULL, NULL)  
)   
AS XEventData  
ORDER BY time;  
```  
  
下列範例會以非重複模式將 sp_server_diagnostics 的輸出擷取至資料表：  
```sql  
CREATE TABLE SpServerDiagnosticsResult  
(  
      create_time DateTime,  
      component_type sysname,  
      component_name sysname,  
      state int,  
      state_desc sysname,  
      data xml  
);  
INSERT INTO SpServerDiagnosticsResult  
EXEC sp_server_diagnostics; 
```  

以下的範例查詢會從資料表讀取摘要輸出：  
```sql  
SELECT create_time,
       component_name,
       state_desc 
FROM SpServerDiagnosticsResult;  
``` 

以下的範例查詢會從資料表中的每個元件讀取某些詳細輸出：  
```sql  
-- system
select data.value('(/system/@systemCpuUtilization)[1]','bigint') as 'System_CPU',
   data.value('(/system/@sqlCpuUtilization)[1]','bigint') as 'SQL_CPU',
   data.value('(/system/@nonYieldingTasksReported)[1]','bigint') as 'NonYielding_Tasks',
   data.value('(/system/@pageFaults)[1]','bigint') as 'Page_Faults',
   data.value('(/system/@latchWarnings)[1]','bigint') as 'Latch_Warnings',
   data.value('(/system/@BadPagesDetected)[1]','bigint') as 'BadPages_Detected',
   data.value('(/system/@BadPagesFixed)[1]','bigint') as 'BadPages_Fixed'
from SpServerDiagnosticsResult 
where component_name like 'system'
go

-- Resource Monitor
select data.value('(./Record/ResourceMonitor/Notification)[1]', 'VARCHAR(max)') AS [Notification],
    data.value('(/resource/memoryReport/entry[@description=''Working Set'']/@value)[1]', 'bigint')/1024 AS [SQL_Mem_in_use_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Paging File'']/@value)[1]', 'bigint')/1024 AS [Avail_Pagefile_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Physical Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_Physical_Mem_MB],
    data.value('(/resource/memoryReport/entry[@description=''Available Virtual Memory'']/@value)[1]', 'bigint')/1024 AS [Avail_VAS_MB],
    data.value('(/resource/@lastNotification)[1]','varchar(100)') as 'LastNotification',
    data.value('(/resource/@outOfMemoryExceptions)[1]','bigint') as 'OOM_Exceptions'
from SpServerDiagnosticsResult 
where component_name like 'resource'
go

-- Nonpreemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/nonPreemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- Preemptive waits
select waits.evt.value('(@waitType)','varchar(100)') as 'Wait_Type',
   waits.evt.value('(@waits)','bigint') as 'Waits',
   waits.evt.value('(@averageWaitTime)','bigint') as 'Avg_Wait_Time',
   waits.evt.value('(@maxWaitTime)','bigint') as 'Max_Wait_Time'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/topWaits/preemptive/byDuration/wait') AS waits(evt)
where component_name like 'query_processing'
go

-- CPU intensive requests
select cpureq.evt.value('(@sessionId)','bigint') as 'SessionID',
   cpureq.evt.value('(@command)','varchar(100)') as 'Command',
   cpureq.evt.value('(@cpuUtilization)','bigint') as 'CPU_Utilization',
   cpureq.evt.value('(@cpuTimeMs)','bigint') as 'CPU_Time_ms'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/cpuIntensiveRequests/request') AS cpureq(evt)
where component_name like 'query_processing'
go

-- Blocked Process Report
select blk.evt.query('.') as 'Blocked_Process_Report_XML'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/queryProcessing/blockingTasks/blocked-process-report') AS blk(evt)
where component_name like 'query_processing'
go

-- IO
select data.value('(/ioSubsystem/@ioLatchTimeouts)[1]','bigint') as 'Latch_Timeouts',
   data.value('(/ioSubsystem/@totalLongIos)[1]','bigint') as 'Total_Long_IOs'
from SpServerDiagnosticsResult 
where component_name like 'io_subsystem'
go

-- Event information
select xevts.evt.value('(@name)','varchar(100)') as 'xEvent_Name',
   xevts.evt.value('(@package)','varchar(100)') as 'Package',
   xevts.evt.value('(@timestamp)','datetime') as 'xEvent_Time',
   xevts.evt.query('.') as 'Event Data'
from SpServerDiagnosticsResult 
    CROSS APPLY data.nodes('/events/session/RingBufferTarget/event') AS xevts(evt)
where component_name like 'events'
go  
``` 
  
## <a name="see-also"></a>另請參閱  
 [容錯移轉叢集執行個體的容錯移轉原則](../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
