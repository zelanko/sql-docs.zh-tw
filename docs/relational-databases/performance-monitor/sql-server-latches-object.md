---
title: SQL Server 的 Latches 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 3cd5db61a2a64f02f0e34b8c2d8fec9dd0c1fa9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62649587"
---
# <a name="sql-server-latches-object"></a>SQL Server 的 Latches 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft **的** SQLServer:Latches [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件提供計數器，可監視稱為閂鎖的內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源鎖定。 監視閂鎖來判斷使用者活動和資源使用狀況，可協助您找出效能的瓶頸。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Latches** 計數器。  
  
|SQL Server 的 Latches 計數器|Description|  
|---------------------------------|-----------------|  
|**Average Latch Wait Time (ms)**|必須等候之閂鎖要求的平均閂鎖等候時間 (以毫秒為單位)。|  
|**Average Latch Wait Time Base**|僅供內部使用。| 
|**Latch Waits/sec**|無法立即授權的閂鎖要求次數。|  
|**SuperLatch 數目**|目前為 SuperLatch 的閂鎖數目。|  
|**SuperLatch Demotions/sec**|在上一秒內已降級為一般閂鎖的 SuperLatch 數目。|  
|**SuperLatch Promotions/sec**|在上一秒內已升級為 SuperLatch 的閂鎖數目。|  
|**Total Latch Wait Time (ms)**|最後一秒內的鎖定總等候時間 (以毫秒為單位)。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
