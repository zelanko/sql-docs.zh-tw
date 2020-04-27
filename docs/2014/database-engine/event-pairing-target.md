---
title: 事件配對目標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- pairing target [SQL Server extended events]
- event pairing target
- targets [SQL Server extended events], pairing target
ms.assetid: 3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39e444077c3dbe27ae243e4292b7a047e21de2b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064852"
---
# <a name="event-pairing-target"></a>事件配對目標
  事件配對目標會使用每個事件中存在之一個或多個資料行來比對兩個事件。 許多事件都是以成對的形式出現，例如鎖定取得和鎖定釋放。 當事件序列配對之後，會捨棄這兩個事件。 捨棄相符的事件組可讓您輕鬆偵測尚未釋放的鎖定取得。  
  
 藉由使用事件層級的篩選，配對目標可以只用來擷取不符合預設準則的事件。  
  
 當您使用事件配對目標時，可以選擇將要比對的兩個事件，以及比對作業執行所在的資料行序列。 此序列中的所有資料行都必須有相同的類型。  
  
 下表說明用來設定事件配對的可用選項。  
  
|選項|允許的值|描述|  
|------------|--------------------|-----------------|  
|begin_event|存在於目前工作階段中的任何事件名稱。|指定配對序列中之開頭事件的事件名稱。|  
|end_event|存在於目前工作階段中的任何事件名稱。|指定配對序列中之結尾事件的事件名稱。|  
|begin_matching_columns|以逗號分隔且排序的資料行名稱清單。|要執行比對的資料行。|  
|end_matching_columns|以逗號分隔且排序的資料行名稱清單。|要執行比對的資料行。|  
|begin_matching_actions|以逗號分隔且排序的動作清單。|要執行比對的動作。|  
|end_matching_actions|以逗號分隔且排序的動作清單。|要執行比對的動作。|  
|respond_to_memory_pressure|下列其中一個值：<br /><br /> 0 = 不回應。<br /><br /> 1 = 當有記憶體不足的壓力時，停止將新的遺棄項目加入清單中。|對記憶體事件的目標回應。 如果設定為 1，而且伺服器的記憶體很少，則會移除正在維護且未成對的資訊。|  
|max_orphans||指定目標中將收集的未配對事件總數。 一旦達到此限制，就會根據先入先出 (FIFO) 移除未配對的事件。 預設值 = 10,000。|  
  
 所有與事件有關的資料都會擷取，並儲存起來供將來配對。 此外，也會收集動作所加入的資料。 收集的事件資料會儲存在記憶體中，因此會有有限度的限制。 這個限制是以系統容量和活動為根據。 所使用的記憶體數量將會根據可用的系統資源而定，而不會將最大記憶體數量當做參數使用。 當無法使用這些項目時，將會卸除已經保留且未配對的事件。 如果事件尚未配對且遭到卸除，則相符的事件將會以未配對事件的形式出現。  
  
 配對目標會將未配對的事件序列化成 XML 格式， 這個格式不符合任何結構描述。 此格式只包含兩個元素類型。 不** \<成對的>** 元素是根，後面接著一個。 目前正在追蹤之每一個未配對事件的事件>元素。 ** \< ** Event>元素包含一個屬性，其中包含未配對事件的名稱。 ** \< **  
  
## <a name="adding-the-target-to-a-session"></a>將目標加入至工作階段  
 若要將配對比對目標加入至擴充事件工作階段，您必須在建立或更改事件工作階段時，加入下列陳述式：  
  
```  
ADD TARGET package0.pair_matching   
```  
  
 之後，您會使用 SET 陳述式，以便定義開始和結束事件，以及要比對的動作或資料行。 下例顯示配對比對 sqlserver.lock_acquired 和 sqlserver.lock_released 事件的範例語法。  
  
```  
   ( SET begin_event = 'sqlserver.lock_acquired',  
      begin_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
      end_event = 'sqlserver.lock_released',  
      end_matching_columns = 'database_id, resource_0, resource_1, resource_2, transaction_id, mode',  
   respond_to_memory_pressure = 1)  
```  
  
 如需詳細資訊，請參閱 [判斷哪些查詢持有鎖定](../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)。  
  
## <a name="reviewing-the-target-output"></a>檢閱目標輸出  
 若要檢閱配對比對目標的輸出，您可以使用下列查詢，並將 *session_name* 取代成事件工作階段的名稱。  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下列範例顯示配對目標輸出格式。  
  
```  
<unpaired truncated = "0" matchedCount = "[matched count]" memoryPressureDroppedCount = " [lost count]">  
    <event name  = "[event name]" package = "[package]" id= "[event ID value]" version = "[event version]">  
    <data name = "[column name]">   
    <type name = "[column type]" package = "[type package]" />   
    <value>[column value]</value>  
    <text value>[text value]</text>>  
        </data>  
    </event>  
</unpaired>  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [dm_xe_session_targets &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [&#40;Transact-sql&#41;建立事件會話](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
