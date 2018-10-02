---
title: SQL Server 的 Broker Activation 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da3301e99c06d4eda52814f03150065036006971
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851471"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server 的 Broker Activation 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:BrokerActivation** 效能物件包含效能計數器，可報告預存程序啟用的資訊。 下表列出這個物件包含的計數器。  
  
|SQL Server Broker 啟用計數器|Description|  
|-------------------------------------------|-----------------|  
|**叫用的預存程序/秒**|此計數器會報告在執行個體中所有佇列監視器每秒所叫用的啟用預存程序總數。|  
|**所達到的工作限制**|此計數器會報告佇列監視器已經啟動新工作的總次數，但如果已經執行佇列工作的最大數目就不會報告。|  
|**所達到的工作限制/秒**|此計數器會報告每秒佇列監視器已經啟動新工作的次數，但如果已經為佇列執行工作最大的數目就不會報告。|  
|**已中止的工作/秒**|此計數器會報告啟用預存程序工作，因錯誤而結束或因無法接收訊息而由佇列監視器中止的數目。|  
|**工作執行**|此計數器會報告目前正在執行的啟用預存程序的數目。|  
|**已啟動的工作/秒**|此計數器會報告在執行個體中所有佇列監視器每秒所啟動的啟用預存程序數目。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_broker_activated_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql.md)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
