---
title: SQL Server 的 Broker TO Statistics 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Broker Transmission Object object
- 'SQL Server: Broker Transmission Object'
ms.assetid: b5bc5dde-e540-4848-8aa3-5735c51df2fb
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 404c16baf92fb1f10adbbfd5c04ce3cdc05c3247
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37203078"
---
# <a name="sql-server-broker-to-statistics-object"></a>SQL Server 的 Broker TO Statistics 物件
  SQLServer:Broker TO Statistics 效能物件會報告 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話要求傳輸物件的次數以及傳輸物件寫入 **tempdb** 之頻率的相關資訊。  
  
 傳輸物件會記錄 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話之訊息傳輸的狀態。 這些會儲存在記憶體中。 為了釋出記憶體， [!INCLUDE[ssSB](../../includes/sssb-md.md)] 會定期將非使用中傳輸物件的批次寫入 **tempdb**中的工作資料表。  
  
 下表列出這個物件包含的計數器。  
  
|SQL Server Broker TO Statistics 計數器|描述|  
|----------------------------------------------|-----------------|  
|**平均Length of Batched Writes**|儲存於批次中的傳輸物件平均數目。|  
|**平均Time To Write Batch (ms)**|儲存傳輸物件批次所需的平均毫秒數。|  
|**平均Time Between Batches (ms)**|傳輸物件批次寫入之間的平均毫秒數。|  
|**Tran Object Gets/sec**|對話每秒鐘要求傳輸物件的次數。|  
|**Tran Objects Marked Dirty/sec**|傳輸物件每秒鐘標示為中途的次數。 造成記憶體內部複本與儲存於 **tempdb**中的複本不同的第一次修改將傳輸物件標示為中途。 當 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 必須記錄對話之訊息傳輸的狀態變更時，會修改傳輸物件。|  
|**Tran Object Writes/sec**|傳輸物件批次每秒鐘寫入 **tempdb** 工作資料表的次數。 寫入次數很多時，可能表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記憶體的負荷很大。|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 Access Methods 物件](sql-server-access-methods-object.md)   
 [SQL Server 的 Memory Manager 物件](sql-server-memory-manager-object.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](monitor-resource-usage-system-monitor.md)  
  
  
