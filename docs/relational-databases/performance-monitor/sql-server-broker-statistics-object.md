---
title: SQL Server 的 Broker Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 77a6174931924c30b8d482c0bd5d3f4a358f4a10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987019"
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server 的 Broker Statistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQLServer:Broker Statistics 效能物件包含可針對 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 執行個體報告一般 [!INCLUDE[ssDE](../../includes/ssde-md.md)]資訊的效能計數器。 下表列出這個物件包含的計數器：  
  
|SQL Server 的 Broker Statistics 計數器|Description|  
|-------------------------------------------|-----------------|  
|**Activation Errors Total**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 啟用預存程序已結束並發生錯誤的次數。|  
|**Broker Transaction Rollbacks**|包含與 [!INCLUDE[ssSB](../../includes/sssb-md.md)]相關之 DML 陳述式 (例如 SEND 和 RECEIVE) 的回復交易數目。|  
|**Corrupted Messages Total**|執行個體收到的損毀訊息數目。|  
|**Dequeued Transmission Msgs/sec**|每秒從 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 傳輸佇列中移除的訊息數目。|  
|**Dialog timer event count**|在對話通訊協定層中使用中的計時器數目。 此數目與使用中對話的數目一致。|  
|**Dropped Messages Total**|執行個體收到但是無法傳遞至佇列的訊息數目。|  
|**Enqueued Local Messages Total**|在執行個體的佇列中已放置的訊息數目，但只計數透過網路傳送而未到達的訊息。|  
|**Enqueued Local Messages/sec**|在執行個體的佇列中每秒所放置的訊息數目，但只計數透過網路傳送而未到達的訊息。|  
|**Enqueued Messages Total**|在執行個體的佇列中已放置的訊息總數。|  
|**Enqueued Messages/sec**|在執行個體的佇列中每秒所放置的訊息數目。 這包括所有優先順序層級的訊息。|  
|**Enqueued P1 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 1 訊息數目。|  
|**Enqueued P2 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 2 訊息數目。|  
|**Enqueued P3 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 3 訊息數目。|  
|**Enqueued P4 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 4 訊息數目。|  
|**Enqueued P5 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 5 訊息數目。|  
|**Enqueued P6 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 6 訊息數目。|  
|**Enqueued P7 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 7 訊息數目。|  
|**Enqueued P8 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 8 訊息數目。|  
|**Enqueued P9 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 9 訊息數目。|  
|**Enqueued P10 Msgs/sec**|在執行個體的佇列中每秒所放置的優先順序 10 訊息數目。|  
|**Enqueued Transmission Msgs/sec**|每秒在 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 傳輸佇列中放置的訊息數目。|  
|**Enqueued Transport Msg Frag Tot**|在執行個體的佇列中已放置的訊息片段數目，但只計數透過網路傳送已到達的訊息。|  
|**Enqueued Transport Msg Frags/sec**|在執行個體的佇列中每秒所放置的訊息片段數目。|  
|**Enqueued Transport Msgs Total**|在執行個體的佇列中已放置的訊息數目，但只計數透過網路傳送已到達的訊息。|  
|**Enqueued Transport Msgs/sec**|在執行個體的佇列中每秒所放置的訊息數目，但只計數透過網路傳送已到達的訊息。|  
|**Forwarded Messages Total**|此電腦所轉寄的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 訊息總數。|  
|**Forwarded Messages/sec**|此電腦每秒所轉寄的訊息數目。|  
|**Forwarded Msg Byte Total**|此電腦所轉寄的訊息總大小 (位元組)。|  
|**Forwarded Msg Bytes/sec**|此電腦每秒所轉寄的訊息大小 (位元組)。|  
|**Forwarded Msg Discarded Total**|此電腦接收要轉寄的訊息數目，但並未成功轉寄。|  
|**Forwarded Msg Discarded/sec**|此電腦每秒接收要轉寄的訊息數目，但並未成功轉寄。|  
|**Forwarded Pending Msg Bytes**|目前保留要轉寄的訊息總大小。|  
|**Forwarded Pending Msg Count**|目前保留要轉寄的訊息總數目。|  
|**SQL RECEIVE Total**|已處理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 陳述式總數。|  
|**SQL RECEIVEs/sec**|每秒已處理的 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 陳述式數目。|  
|**SQL SEND Total**|已執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 陳述式總數。|  
|**SQL SENDs/sec**|每秒已執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 陳述式數目。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
