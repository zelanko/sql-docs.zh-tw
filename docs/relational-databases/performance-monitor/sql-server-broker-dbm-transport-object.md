---
title: "SQL Server 的 Broker - DBM Transport 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0bad82d13370dfba9e1067986d1f1789ecf006ec
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-broker---dbm-transport-object"></a>SQL Server 的 Broker─DBM Transport 物件
  **Broker / DBM Transport** 效能物件包含效能計數器，以報告 Service Broker 和資料庫鏡像的網路資訊。 下表列出這個物件包含的計數器。  
  
|SQL Server Broker / DBM Transport 計數器|描述|  
|------------------------------------------------|-----------------|  
|**Current Bytes for Recv I/O**|此計數器會報告目前執行傳輸接收作業所讀取的位元組數目。|  
|**Current Bytes for Send I/O**|此計數器會報告目前正在透過網路傳送訊息片段的位元組數目。|  
|**Current Msg Frags for Send I/O**|此計數器會報告目前正在透過網路傳送訊息片段的總數目。|  
|**Message Fragment P1 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 1 訊息片段的數目。|  
|**Message Fragment P2 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 2 訊息片段的數目。|  
|**Message Fragment P3 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 3 訊息片段的數目。|  
|**Message Fragment P4 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 4 訊息片段的數目。|  
|**Message Fragment P5 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 5 訊息片段的數目。|  
|**Message Fragment P6 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 6 訊息片段的數目。|  
|**Message Fragment P7 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 7 訊息片段的數目。|  
|**Message Fragment P8 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 8 訊息片段的數目。|  
|**Message Fragment P9 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 9 訊息片段的數目。|  
|**Message Fragment P10 Sends/sec**|此計數器會報告每秒透過網路傳送優先順序 10 訊息片段的數目。|  
|**Message Fragment Receives/sec**|此計數器會報告每秒透過網路接收訊息片段的數目。|   
|**Message Fragment Sends/sec**|此計數器會報告每秒透過網路傳送所有優先順序訊息片段的數目。|  
|**Msg Fragment Recv Size Avg**|此計數器會報告透過網路接收訊息片段的平均大小。|  
|**Msg Fragment Recv Size Avg Base**|僅供內部使用。| 
|**Msg Fragment Send Size Avg**|此計數器會報告透過網路傳送訊息片段的平均大小。|  
|**Msg Fragment Send Size Avg Base**|僅供內部使用。|
|**Open Connection Count**|此計數器會報告 Service Broker 目前已開啟的網路連接數目。|  
|**Pending Bytes for Recv I/O**|此計數器會報告已從網路接收，但尚未放到佇列中或尚未捨棄的訊息片段之位元組數目。|  
|**Pending Bytes for Send I/O**|此計數器會報告準備透過網路傳送訊息片段的位元組總數目。|  
|**Pending Msg Frags for Recv I/O**|此計數器會報告已從網路接收，但尚未放到佇列中或尚未捨棄的訊息片段數目。|  
|**Pending Msg Frags for Send I/O**|此計數器會報告準備透過網路傳送訊息片段的總數目。|  
|**Receive I/O bytes/sec**|此計數器會報告 Service Broker 端點與「資料庫鏡像」端點透過網路每秒接收的位元組數目。|  
|**Receive I/O Bytes Total**|此計數器會報告 Service Broker 端點與「資料庫鏡像」端點透過網路接收的位元組總數目。|  
|**Receive I/O Len Avg**|此計數器會報告傳輸接收作業的平均位元組數目。|  
|**Receive I/O Len Avg Base**|僅供內部使用。|
|**Receive I/Os/sec**|此計數器會報告 Service Broker / DBM 傳輸層每秒已完成的傳輸接收 I/O 作業數目。 請注意傳輸接收作業可能包含一個以上的訊息片段。|  
|**Recv I/O Buffer Copies bytes/sec**|傳輸接收 I/O 作業必須將緩衝區片段移入記憶體的速率。|
|**Recv I/O Buffer Copies Count**|當傳輸接收 I/O 作業必須將緩衝區片段移入記憶體時的次數。| 
|**Send I/O bytes/sec**|這個計數器會報告 Service Broker 端點和資料庫鏡像端點透過網路每秒傳送的位元組數目。|   
|**Send I/O Bytes Total**|這個計數器會報告 Service Broker 端點和資料庫鏡像端點透過網路傳送的位元組總數。| 
|**Send I/O Len Avg**|此計數器會報告每個傳輸傳送作業的平均位元組大小。 請注意傳輸傳送作業可能包含一個以上的訊息片段。|  
|**Send I/O Len Avg Base**|僅供內部使用。|
|**Send I/Os/sec**|此計數器會報告每秒已完成的傳輸傳送 I/O 作業數目。 請注意傳輸傳送作業可能包含一個以上的訊息片段。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
