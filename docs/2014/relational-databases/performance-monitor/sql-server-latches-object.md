---
title: SQL Server 的 Latches 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Latches object
- SQLServer:Latches
ms.assetid: 2393ea1c-2bf3-41c3-9f37-b9761144eeca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d0d9249a5cfb801e07a85132060bb4d1781346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63251094"
---
# <a name="sql-server-latches-object"></a>SQL Server 的 Latches 物件
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的**SQLServer：閂鎖**物件提供計數器，可[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]監視稱為閂鎖的內部資源鎖定。 監視閂鎖來判斷使用者活動和資源使用狀況，可協助您找出效能的瓶頸。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Latches** 計數器。  
  
|SQL Server 的 Latches 計數器|描述|  
|---------------------------------|-----------------|  
|**平均閂鎖等候時間（毫秒）**|必須等候之閂鎖要求的平均閂鎖等候時間 (以毫秒為單位)。|  
|**閂鎖等待/秒**|無法立即授權的閂鎖要求次數。|  
|**Superlatch 數目數目**|目前為 SuperLatch 的閂鎖數目。|  
|**SuperLatch 降級/秒**|在上一秒內已降級為一般閂鎖的 SuperLatch 數目。|  
|**SuperLatch 升級/秒**|在上一秒內已升級為 SuperLatch 的閂鎖數目。|  
|**閂鎖等候時間總計（毫秒）**|最後一秒內的鎖定總等候時間 (以毫秒為單位)。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
