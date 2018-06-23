---
title: SQL Server 的 Broker Activation 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 641769c00de48f5acadc69816071893fb6594050
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029804"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server 的 Broker Activation 物件
  **SQLServer:BrokerActivation** 效能物件包含效能計數器，可報告預存程序啟用的資訊。 下表列出這個物件包含的計數器。  
  
|SQL Server Broker 啟用計數器|描述|  
|-------------------------------------------|-----------------|  
|**叫用的預存程序/秒**|此計數器會報告在執行個體中所有佇列監視器每秒所叫用的啟用預存程序總數。|  
|**所達到的工作限制**|此計數器會報告佇列監視器已經啟動新工作的總次數，但如果已經執行佇列工作的最大數目就不會報告。|  
|**所達到的工作限制/秒**|此計數器會報告每秒佇列監視器已經啟動新工作的次數，但如果已經為佇列執行工作最大的數目就不會報告。|  
|**已中止的工作/秒**|此計數器會報告啟用預存程序工作，因錯誤而結束或因無法接收訊息而由佇列監視器中止的數目。|  
|**工作執行**|此計數器會報告目前正在執行的啟用預存程序的數目。|  
|**已啟動的工作/秒**|此計數器會報告在執行個體中所有佇列監視器每秒所啟動的啟用預存程序數目。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_broker_activated_tasks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql)   
 [監視資源使用狀況 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)  
  
  
