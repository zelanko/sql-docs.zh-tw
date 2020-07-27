---
title: SQL Server 的 Latches 物件 | Microsoft Docs
description: 了解 SQLServer:Latches 物件，其所提供計數器可監視稱為閂鎖的內部 SQL Server 資源鎖定。
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
ms.openlocfilehash: d57998b2bbc83a231cd82ceef8846ef21902eccb
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458810"
---
# <a name="sql-server-latches-object"></a>SQL Server 的 Latches 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Microsoft **的** SQLServer:Latches [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件提供計數器，可監視稱為閂鎖的內部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源鎖定。 監視閂鎖來判斷使用者活動和資源使用狀況，可協助您找出效能的瓶頸。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Latches** 計數器。  
  
|SQL Server 的 Latches 計數器|描述|  
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
  
  
