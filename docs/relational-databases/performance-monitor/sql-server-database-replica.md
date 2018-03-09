---
title: "SQL Server、資料庫複本 | Microsoft Docs"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cea5ae007fde8634631ca223e5d98367dae56717
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-database-replica"></a>SQL Server、資料庫複本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **SQLServer:Database Replica** 效能物件包含的效能計數器會報告有關 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中 AlwaysOn 可用性群組之次要資料庫的報表資訊。 這個物件只有在裝載次要複本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上才有效。  
  
|計數器名稱|描述|檢視位置…|  
|------------------|-----------------|--------------|  
|**File Bytes Received/sec**|次要資料庫的次要複本在上一秒所收到的 FILESTREAM 資料量。|次要複本|  
|**Log Apply Pending Queue**|備妥且待套用至資料庫複本的記錄區塊數。|次要複本|
|**Log Apply Ready Queue**|備妥且待套用至資料庫複本的記錄區塊數。|次要複本| 
|**Log Bytes Received/sec**|資料庫的次要複本在上一秒所收到的記錄檔記錄數量。|次要複本|  
|**Log remaining for undo**|完成復原階段所剩餘的記錄檔數量 (以 KB 為單位)。|次要複本|  
|**Log Send Queue**|主要資料庫記錄檔中尚未傳送至次要複本的記錄檔記錄數量 (以 KB 為單位)。 這個值是從主要複本傳送至次要複本。 佇列大小不包括傳送到次要複本的 FILESTREAM 檔案。|次要複本|  
|**Mirrored Write Transaction/sec**|在上一秒中，已寫入主要資料庫，然後在傳送至次要資料庫之前等候認可的交易數目。|主要複本|  
|**Recovery Queue**|次要複本記錄檔中尚未重做的記錄檔記錄數量。|次要複本|  
|**Redo blocked/sec**|資料庫的讀取者鎖定重做執行緒的次數。|次要複本|  
|**Redo Bytes Remaining**|完成還原階段所要重做的剩餘記錄檔數量 (以 KB 為單位)。|次要複本|  
|**Redone Bytes/sec**|次要資料庫在上一秒重做的記錄檔記錄數量。|次要複本|  
|**Total Log requiring undo**|必須復原之記錄檔的總 KB 數。|次要複本|  
|**Transaction Delay**|等候未終止之認可收條的延遲時間 (以毫秒為單位)。|主要複本|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、可用性複本](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server、Databases 物件](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [AlwaysOn 可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
