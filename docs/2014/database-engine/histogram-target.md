---
title: 長條圖目標 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bucketing target [SQL Server extended events]
- event bucketing target
- targets [SQL Server extended events], bucketing
ms.assetid: 2ea39141-7eb0-4c74-abf8-114c2c106a19
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: acb124ef949849561a6bca0ba4016b40c1343384
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932839"
---
# <a name="histogram-target"></a>長條圖目標
  長條圖目標會根據事件資料來分組特定事件類型的發生。 事件的群組會根據指定的事件資料行或動作來計算。 您可以使用長條圖目標來排除效能問題。 藉由識別哪些事件最常發生，您可以尋找「作用點」來指出效能問題的可能原因。  
  
 下表說明可用來設定長條圖目標的選項。  
  
|選項|允許的值|描述|  
|------------|--------------------|-----------------|  
|slots|任何整數值。 這是選擇性的值。|使用者指定的值，指示要保留的群組數目上限。 當到達這個值時，會忽略不屬於現有群組的新事件。<br /><br /> 請注意，為了提升效能，插槽編號會進位到下一個 2 的乘冪。|  
|filtering_event_name|擴充的事件工作階段中所存在的任何事件。 這是選擇性的值。|使用者指定的值，用來識別事件類別。 只有指定之事件的執行個體才會儲存起來， 所有其他事件則會忽略。<br /><br /> 如果您指定這個值，您必須使用 *package_name*.*event_name*格式，例如 `'sqlserver.checkpoint_end'`。 您可以使用下列查詢來識別封裝名稱：<br /><br /> 選取 [p.name]、[se] event_name<br />從 sys. dm_xe_session_events se<br />加入 sys.databases dm_xe_packages p<br />在 se_event_package_guid = p. guid<br />ORDER BY p.name，se. event_name<br /><br /> <br /><br /> 如果您未指定 filtering_event_name 值，source_type 必須設定為 1 (預設值)。|  
|source_type|值區所根據的物件類型。 這個值是選用的值，而且如果未指定它，它的預設值為 1。|可以具有下列其中一個值：<br /><br /> 0 代表事件。<br /><br /> 1 代表動作。|  
|source|事件資料行或動作名稱。|當做資料來源使用的事件資料行或動作名稱。<br /><br /> 當您為來源指定事件資料行時，您必須從用於 filtering_event_name 值的事件來指定資料行。 您可以使用下列查詢來識別可能的資料行：<br /><br /> 從 sys.databases 選取 [名稱] dm_xe_object_columns<br />其中 object_name = ' \<eventname> '<br />和 column_type！ = ' readonly '<br /><br /> 當您為來源指定事件資料行時，您不必在來源值中包含封裝名稱。<br /><br /> 當您為來源指定動作名稱時，您必須在正在使用此目標的事件工作階段中，使用針對集合所設定的其中一個動作。 若要尋找動作名稱的可能值，您可以查詢 sys.dm_xe_sesssion_event_actions 檢視表的 action_name 資料行。<br /><br /> 如果您將動作名稱當作資料來源使用，您必須使用 *package_name*.*action_name*格式來指定來源值。|  
  
 下列範例將以高層級的方式說明長條圖目標如何收集資料。 在此範例中，您想要使用長條圖目標來計算所發生之每一個等候類型的等候次數。 若要這樣做，當您定義長條圖目標時，您會指定下列選項：  
  
-   filtering_event_name = 'wait_info'  
  
-   source = 'wait_type'  
  
-   source_type = 0 (因為 wait_type 為事件資料行)  
  
 在此案例中，將會針對 wait_type 來源記錄以下資料。  
  
|篩選事件名稱|來源資料行值|  
|--------------------------|-------------------------|  
|wait_info|file_io|  
|wait_info|file_io|  
|wait_info|network|  
|wait_info|network|  
|wait_info|sleep|  
  
 等候類型值會分成三個位置，值和位置計數如下：  
  
|值|位置計數|  
|-----------|----------------|  
|file_io|2|  
|network|2|  
|sleep|1|  
  
 長條圖目標只會保留指定之來源的事件資料。 在某些情況下，事件資料可能會太大而無法完整保留，此時資料會遭到截斷。 當事件資料遭到截斷時，位元組數目會記錄下來並顯示為 XML 輸出。  
  
## <a name="adding-the-target-to-a-session"></a>將目標加入至工作階段  
 若要將長條圖目標加入至擴充事件工作階段，您必須在建立或改變事件工作階段時，根據所需的目標類型加入下列其中一個陳述式：  
  
```  
ADD TARGET package0.histogram  
```  
  
 您可以使用 SET 陳述式來設定各種選項。 下列範例將示範如何加入長條圖目標，以便收集 sqlserver.checkpoint_end 事件的資料。  
  
```  
ADD TARGET package0.histogram  
(SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id')  
```  
  
 如需詳細資訊，請參閱 [尋找持有最多鎖定的物件](../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)和 [使用擴充事件監視系統活動](../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)。  
  
## <a name="reviewing-the-target-output"></a>檢閱目標輸出  
 長條圖目標會將資料序列化成 XML 格式的呼叫程式或程序。 目標輸出不符合任何結構描述。  
  
 若要檢閱長條圖目標的輸出，您可以使用下列查詢，並將 *session_name* 取代成事件工作階段的名稱。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下列範例說明長條圖目標輸出格式。  
  
```  
<Slots truncated = "0" buckets=[count]>  
    <Slot count=[count] trunc=[truncated bytes]>  
        <value>  
        </value>  
    </Slot>  
</Slots>  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [dm_xe_session_targets &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [&#40;Transact-sql&#41;建立事件會話](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
