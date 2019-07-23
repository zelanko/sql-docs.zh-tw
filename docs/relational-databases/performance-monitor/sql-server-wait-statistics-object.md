---
title: SQL Server 的 Wait Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c690c2cd19acae2fb3a6bde8b2dcd6d72b3acf18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947880"
---
# <a name="sql-server-wait-statistics-object"></a>SQL Server 的 Wait Statistics 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Wait Statistics** 效能物件包含效能計數器，可報告等候狀態的詳細資訊。  
  
 下表列出 Wait Statistics 物件包含的計數器。  
  
|SQL Server Wait Statistics 計數器|Description|  
|-----------------------------------------|-----------------|  
|**Lock waits**|正在等候鎖定的處理序統計資料。|  
|**Log buffer waits**|等候記錄緩衝區變為可用的處理序統計資料。|  
|**Log write waits**|等候寫入記錄緩衝區的處理序統計資料。|  
|**Memory grant queue waits**|等候記憶體授權變為可用的處理序統計資料。|  
|**Network IO waits**|有關等候網路 I/O 的統計資料。|  
|**Non-Page latch waits**|有關非頁面閂鎖的統計資料。|  
|**Page IO latch waits**|有關頁面 I/O 閂鎖的統計資料。|  
|**Page latch waits**|有關頁面閂鎖的統計資料，不包括 I/O 閂鎖。|  
|**Thread-safe memory objects waits**|等候安全執行緒記憶體配置器的處理序統計資料。|  
|**Transaction ownership waits**|有關同步存取交易的處理序統計資料。|  
|**Wait for the worker**|有關等候工作者變為可用的處理序統計資料。|  
|**Workspace synchronization waits**|有關同步存取工作空間的處理序統計資料。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|項目|Description|  
|----------|-----------------|  
|**Average wait time (ms)**|所選取等候類型的平均等候時間。|  
|**Cumulative wait time (ms) per second**|所選取等候類型的每秒彙總等候時間。|  
|**Waits in progress**|目前正在等候其下類型的處理序數目。|  
|**Waits started per second**|所選取等候類型的每秒開始等候數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
