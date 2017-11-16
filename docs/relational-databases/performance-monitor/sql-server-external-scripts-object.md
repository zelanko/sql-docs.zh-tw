---
title: "SQL Server 的 External Scripts 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- External Scripts object
- SQLServer:External Scripts
ms.assetid: 8a75ccce-b174-4937-bc92-8e413b55afe1
caps.latest.revision: "7"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e5510df60aeff35597da1954fd97c9fc0eb8e86
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-external-scripts-object"></a>SQL Server, 外部指令碼物件
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

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
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.resource_governor_external_resource_pools &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-resource-governor-external-resource-pools-transact-sql.md)   
 [sys.dm_resource_governor_external_resource_pool_affinity &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
