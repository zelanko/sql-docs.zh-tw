---
title: "SQL Server 的 SQL Errors 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a61338c9ea2ba16e88d2b71bacedbd382a7bf49
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="sql-server-sql-errors-object"></a>SQL Server 的 SQL Errors 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的 **SQLServer:SQL Errors** 物件，提供用來監視 **SQL Errors** 的計數器。  
  
 下表描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **SQL Errors** 計數器。  
  
|SQL Server SQL Errors 計數器|描述|  
|------------------------------------|-----------------|  
|**Errors/sec**|每秒的錯誤數目。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|項目|定義|  
|----------|----------------|  
|**_Total**|所有錯誤的相關資訊。|  
|**DB Offline Errors**|追蹤導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 讓目前資料庫離線的嚴重錯誤。|  
|**Info Errors**|針對僅提供資訊給使用者而不會導致錯誤的錯誤訊息，提供其相關資訊。|  
|**Kill Connection Errors**|追蹤導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 清除目前連接的嚴重錯誤。|  
|**User Errors**|使用者錯誤的相關資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
