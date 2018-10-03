---
title: SQL Server 的 Latches 物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b840a05c741b91064f435663a9a423eb9b035283
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821076"
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
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
