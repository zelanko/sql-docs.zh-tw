---
title: SQL Server、 訊息代理程式和 DBM Transport 物件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0347c7f7e19ae5500f8c5be100ef2d0dc663784
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748230"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>SQL Server 的 Broker 和 DBM Transport 物件
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
|**訊息片段傳送大小平均**|此計數器會報告透過網路傳送訊息片段的平均大小。|  
|**Message Fragment Sends/sec**|此計數器會報告每秒透過網路傳送所有優先順序訊息片段的數目。|  
|**接收的訊息片段/sec**|此計數器會報告每秒透過網路接收訊息片段的數目。|  
|**Msg Fragment Recv Size Avg**|此計數器會報告透過網路接收訊息片段的平均大小。|  
|**Open Connection Count**|此計數器會報告 Service Broker 目前已開啟的網路連接數目。|  
|**Pending Bytes for Recv I/O**|此計數器會報告已從網路接收，但尚未放到佇列中或尚未捨棄的訊息片段之位元組數目。|  
|**Pending Bytes for Send I/O**|此計數器會報告準備透過網路傳送訊息片段的位元組總數目。|  
|**Pending Msg Frags for Recv I/O**|此計數器會報告已從網路接收，但尚未放到佇列中或尚未捨棄的訊息片段數目。|  
|**Pending Msg Frags for Send I/O**|此計數器會報告準備透過網路傳送訊息片段的總數目。|  
|**Receive I/O Bytes Total**|此計數器會報告 Service Broker 端點與「資料庫鏡像」端點透過網路接收的位元組總數目。|  
|**Receive I/O bytes/sec**|此計數器會報告 Service Broker 端點與「資料庫鏡像」端點透過網路每秒接收的位元組數目。|  
|**Receive I/O Len Avg**|此計數器會報告傳輸接收作業的平均位元組數目。|  
|**接收 i/o 數目/秒**|此計數器會報告 Service Broker / DBM 傳輸層每秒已完成的傳輸接收 I/O 作業數目。 請注意傳輸接收作業可能包含一個以上的訊息片段。|  
|**Send I/O Bytes Total**|這個計數器會報告 Service Broker 端點和資料庫鏡像端點透過網路傳送的位元組總數。|  
|**Send I/O bytes/sec**|這個計數器會報告 Service Broker 端點和資料庫鏡像端點透過網路每秒傳送的位元組數目。|  
|**Send I/O Len Avg**|此計數器會報告每個傳輸傳送作業的平均位元組大小。 請注意傳輸傳送作業可能包含一個以上的訊息片段。|  
|**Send I/Os/sec**|此計數器會報告每秒已完成的傳輸傳送 I/O 作業數目。 請注意傳輸傳送作業可能包含一個以上的訊息片段。|  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
