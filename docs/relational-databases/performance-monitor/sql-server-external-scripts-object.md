---
title: "SQL Server 的 External Scripts 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: "7"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa53d84e29b23d73f73c93641306b11a328fc2e1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, 外部指令碼物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 **SQLServer:External Scripts** 物件可提供計數器來監視與執行外部指令碼相關聯的動作。 如需執行外部指令碼的相關資訊，請參閱 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **外部指令碼**計數器。  
  
|SQL Server 外部指令碼計數器|描述|  
|------------------------------------------|-----------------|  
|**執行錯誤**|執行外部指令碼時的錯誤數目。|  
|**Implied Auth.Logins**|來自使用隱含驗證進行驗證之附屬程序的登入次數。|  
|**平行執行**|使用 @parallel = 1 執行的外部指令碼數目。|  
|**SQL CC 執行**|使用 SQL 計算內容執行的外部指令碼數目。|  
|**串流執行**|使用 @r_rowsPerRead 參數執行的外部指令碼數目。|  
|**執行時間總計 (毫秒)**|花在執行外部指令碼的時間總計。|  
|**執行總計**|執行的外部指令碼數目。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用量 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
