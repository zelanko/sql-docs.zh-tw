---
title: SQL Server 的 Columnstore 物件 | Microsoft Docs
description: 了解 SQLServer:Columnstore 物件，其所提供計數器可監視 SQL Server 中的資料行存放區索引執行。
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 61f950b5322270ce1b72b1734b92474dfb18b2bb
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505784"
---
# <a name="sql-server-columnstore-object"></a>SQL Server, Columnstore 物件
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
 [監視資源使用狀況 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
