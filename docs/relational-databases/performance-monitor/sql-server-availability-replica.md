---
title: SQL Server、可用性複本 | Microsoft Docs
description: 了解 SQLServer:Availability Replica 效能物件，其包含有關 Always On 可用性群組內可用性複本的效能計數器。
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: cb04f9a626c63e5e65f73b3de0810a2869ee9841
ms.sourcegitcommit: 2bf83972036bdbe6a039fb2d1fc7b5f9ca9589d3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674150"
---
# <a name="sql-server-availability-replica"></a>SQL Server、可用性複本

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SQLServer:Availability Replica** 效能物件含有效能計數器，會報告有關 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中 AlwaysOn 可用性群組內可用性複本的資訊。 所有可用性複本效能計數器皆適用於主要複本和次要複本，並附有可以反映本機複本的傳送/接收計數器。 在大部分情況下，主要複本會傳送大部分資料，而次要複本會接收資料。 但次要複本會將 ACK 及一些其他背景流量傳送至主要複本。 請注意，在給定可用性複本上，有些計數器會顯示零值，這取決於本機複本目前的角色 (主要或次要) 而定。  
  
|計數器名稱|描述|  
|------------------|-----------------|  
|**Bytes Received from Replica/sec**|**SQL Server 2012 和 2014：** 每秒從可用性複本 (同步或非同步) 接收到的實際位元組數目 (已壓縮)。 Ping 和狀態更新將會產生網路流量，即使在沒有使用者更新的資料庫上亦然。 <BR/> <BR/> **SQL Server 2016 及更新版本：** 每秒從可用性複本接收到的實際位元組數目 (非同步壓縮、同步未壓縮)。|  
|**Bytes Sent to Replica/sec**|**SQL Server 2012 和 2014：** 每秒透過網路傳送至遠端可用性複本 (同步或非同步) 的實際位元組數目 (已壓縮)。 根據預設，同步和非同步複本都會啟用壓縮。 <BR/> <BR/> **SQL Server 2016 和更新版本：** 每秒傳送至遠端可用性複本的位元組數目。 壓縮非同步複本之前。 (未壓縮的同步複本實際位元組數目)|  
|**Bytes Sent to Transport/sec**|**SQL Server 2012 和 2014：** 每秒透過網路傳送至遠端可用性複本 (同步或非同步) 的實際位元組數目 (已壓縮)。 根據預設，同步和非同步複本都會啟用壓縮。 <BR/> <BR/> **SQL Server 2016 和更新版本：** 壓縮非同步複本之前，每秒傳送至遠端可用性複本的位元組數目。 (未壓縮的同步複本實際位元組數目)|  
|**Flow Control Time (ms/sec)**|上一秒記錄資料流訊息等候傳送流量控制的時間 (以毫秒為單位)。|  
|**Flow Control/sec**|上一秒起始的流量控制次數。 **Flow Control Time (ms/sec)** 除以 **Flow Control/sec** 是每次等待的平均時間。|  
|**Receives from Replica/sec**|每秒從複本接收到的 AlwaysOn 訊息數目。|  
|**Resent Messages/sec**|上一秒重新傳送的 AlwaysOn 訊息數目。|  
|**Sends to Replica/sec**|每秒傳送至此可用性複本的 AlwaysOn 訊息數目。|  
|**Sends to Transport/sec**|每秒透過網路傳送至遠端可用性複本的實際 AlwaysOn 訊息數目。 在主要複本上，這是傳送至次要複本的訊息數目。 在次要複本上，這是傳送至主要複本的訊息數目。|  
  
## <a name="see-also"></a>另請參閱 
 
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、資料庫複本](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Always On 可用性群組 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
