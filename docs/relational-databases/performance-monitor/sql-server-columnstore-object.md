---
title: "SQL Server 的 Columnstore 物件 | Microsoft Docs"
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 041279879116916b0d603e8c1f9a81f8ad180f70
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-columnstore-object"></a>SQL Server, Columnstore 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  **SQLServer:Columnstore** 物件提供用來監視在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行資料行存放區索引的計數器。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** 計數器。  
  
|Columnstore 計數器|描述|  
|--------------------------|-----------------|  
|**Delta Rowgroups Closed**|已關閉的差異資料列群組數目。|  
|**Delta Rowgroups Compressed**|已壓縮的差異資料列群組數目。|  
|**Delta Rowgroups Created**|已建立的差異資料列群組數目。|  
|**Segment Cache Hit Raio**|在資料行存放區集區中，找到不需從磁碟讀取的資料行區段百分比。|  
|**Segment Cache Hit Ratio Base**|僅供內部使用。|
|**Segment Reads/Sec**|發出的實體區段讀取數目。|  
|**Total Delete Buffers Migrated**|Tuple Mover 清除刪除緩衝區的次數。|  
|**Total Merge Policy Evaluations**|資料行存放區的合併原則評估次數。|  
|**Total Rowgroups Compressed**|已壓縮的資料列群組總數。|  
|**Total Rowgroups Fit For Merge**|自從啟動 SQL Server 以來，符合 MERGE 的來源資料列群組數目。|  
|**Total Rowgroups Merge Compressed**|自從啟動 SQL Server 以來，已使用 MERGE 建立的壓縮目標資料列群組數目。|  
|**Total Source Rowgroups Merged**|自從啟動 SQL Server 以來，已合併的來源資料列群組數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
