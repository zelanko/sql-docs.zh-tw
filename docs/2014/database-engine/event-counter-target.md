---
title: 事件計數器目標 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- synchronous event counter target [SQL Server extended events]
- targets [SQL Server extended events], synchronous event counter target
ms.assetid: 342e08d1-dcca-4a71-ae64-cb61b55b85bc
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddf153da7af2906fe7167c8cb2b77d9100d1154f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064923"
---
# <a name="event-counter-target"></a>事件計數器目標
  事件計數器目標會計算在擴充事件工作階段期間發生的所有事件。 您可以使用事件計數器目標來取得有關工作負載特性的資訊，而不會增加完整事件收集的負擔。 此目標沒有任何可自訂的參數。  
  
## <a name="adding-the-target-to-a-session"></a>將目標加入至工作階段  
 若要將事件計數器目標加入至擴充事件工作階段，您必須在建立或改變事件工作階段時，加入下列陳述式：  
  
```  
ADD TARGET package0.event_counter  
```  
  
## <a name="reviewing-the-target-output"></a>檢閱目標輸出  
 若要檢閱事件計數器目標的輸出，您可以使用下列查詢，並將 *session_name* 取代成事件工作階段的名稱：  
  
```  
SELECT name, target_name, CAST(xet.target_data AS xml)  
FROM sys.dm_xe_session_targets AS xet  
JOIN sys.dm_xe_sessions AS xe  
   ON (xe.address = xet.event_session_address)  
WHERE xe.name = 'session_name'  
```  
  
 下列範例顯示事件計數器目標輸出格式。  
  
```  
<CounterTarget truncated = "0">  
  <Packages>  
    <Package name = "[package name]">  
      <Event name = "[event name]" count = "[number]" />  
    </Package>  
  </Packages>  
</CounterTarget>  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 擴充事件目標](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [dm_xe_session_targets &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [&#40;Transact-sql&#41;建立事件會話](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
