---
title: "SQL Server、可用性複本 | Microsoft Docs"
ms.custom: 
ms.date: 08/25/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 327b70f445a9f794152073a39059165f75fd3cad
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-availability-replica"></a>SQL Server、可用性複本
  **SQLServer:Availability Replica** 效能物件含有效能計數器，會報告有關 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中 AlwaysOn 可用性群組內可用性複本的資訊。 所有可用性複本效能計數器皆適用於主要複本和次要複本，並附有可以反映本機複本的傳送/接收計數器。 在大部分情況下，主要複本會傳送大部分資料，而次要複本會接收資料。 但次要複本會將 ACK 及一些其他背景流量傳送至主要複本。 請注意，在給定可用性複本上，有些計數器會顯示零值，這取決於本機複本目前的角色 (主要或次要) 而定。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Bytes Received from Replica/sec**|每秒從可用性複本所接收的位元組數目。 Ping 和狀態更新將會產生網路流量，即使在沒有使用者更新的資料庫上亦然。|  
|**Bytes Sent to Replica/sec**|每秒傳送至遠端可用性複本的位元組數目。 在主要複本上，這是傳送至次要複本的位元組數目。 在次要複本上，這是傳送至主要複本的位元組數目。|  
|**Bytes Sent to Transport/sec**|每秒透過網路傳送至遠端可用性複本的實際位元組數目。 在主要複本上，這是傳送至次要複本的位元組數目。 在次要複本上，這是傳送至主要複本的位元組數目。|  
|**Flow Control Time (ms/sec)**|上一秒記錄資料流訊息等候傳送流量控制的時間 (以毫秒為單位)。|  
|**Flow Control/sec**|上一秒起始的流量控制次數。 **Flow Control Time (ms/sec)** 除以 **Flow Control/sec** 是每次等待的平均時間。|  
|**Receives from Replica/sec**|每秒從複本所接收的 AlwaysOn 訊息數目。|  
|**Resent Messages/sec**|上一秒重新傳送的 AlwaysOn 訊息數目。|  
|**Sends to Replica/sec**|每秒傳送至此可用性複本的 AlwaysOn 訊息數目。|  
|**Sends to Transport/sec**|每秒透過網路傳送至遠端可用性複本的實際 AlwaysOn 訊息數目。 在主要複本上，這是傳送至次要複本的訊息數目。 在次要複本上，這是傳送至主要複本的訊息數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、資料庫複本](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [AlwaysOn 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)  
  
  

