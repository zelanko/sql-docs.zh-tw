---
title: SQL Server 的 Locks 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Locks object
- SQLServer:Locks
ms.assetid: ace04f0d-3993-4444-8317-ca39d7087e49
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cd7773177f6ec9d02df9d3d669abf561919ffe0b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250605"
---
# <a name="sql-server-locks-object"></a>SQL Server 的 Locks 物件
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 **SQLServer:Locks** 物件會提供有關個別資源類型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 鎖定資訊。 鎖定發生於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源上，例如交易期間讀取或修改的資料列，以避免不同交易同時使用資源。 例如，若某個交易將資料表內的資料列獨佔 (X) 鎖定，就沒有其他交易可修改該資料列，直到鎖定解除為止。 將鎖定減至最少可增加並行 (Concurrency)，以改善效能。 您可同時監視 **Locks** 物件的多個執行個體，每個執行個體都代表一種資源類型的鎖定。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 計數器。  
  
|SQL Server Locks 計數器|描述|  
|-------------------------------|-----------------|  
|**Average Wait Time (ms)**|造成等候的各個鎖定要求之平均等候時間 (以毫秒為單位)。|  
|**Lock Requests/sec**|鎖定系統管理員每秒要求的新鎖定和鎖定轉換數。|  
|**Lock Timeouts (timeout > 0)/sec**|已逾時的每秒鎖定要求數，但不包括 NOWAIT 鎖定的要求。|  
|**Lock Timeouts/sec**|已逾時的每秒鎖定要求數，包括 NOWAIT 鎖定的要求。|  
|**Lock Wait Time (ms)**|最後一秒內的鎖定總等候時間 (以毫秒為單位)。|  
|**Lock Waits/sec**|每秒需要呼叫者等候的鎖定要求次數。|  
|**Number of Deadlocks/sec**|造成死結的每秒鎖定要求數。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可鎖定這些資源。  
  
|項目|描述|  
|----------|-----------------|  
|**_Total**|所有鎖定的資訊。|  
|**AllocUnit**|配置單位的鎖定。|  
|**應用程式**|應用程式指定資源的鎖定。|  
|**[資料庫備份]**|資料庫的鎖定，包括資料庫中的所有物件。|  
|**Extent**|八頁連續群組的鎖定。|  
|**檔案**|資料庫檔案的鎖定。|  
|**Heap/BTree**|堆積或 BTree (HOBT)。 資料頁堆積的鎖定，或是索引之 BTree 結構的鎖定。|  
|**索引鍵**|索引中之資料列的鎖定。|  
|**中繼資料**|一項目錄資訊 (亦稱為中繼資料) 的鎖定。|  
|**物件**|資料表、預存程序、檢視等 (包括所有資料和索引) 的鎖定。 物件可以是在 **sys.all_objects**中擁有項目的任何東西。|  
|**頁面**|資料庫中 8 KB 分頁的鎖定。|  
|**RID**|資料庫識別碼。 堆積中單一資料列的鎖定。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
