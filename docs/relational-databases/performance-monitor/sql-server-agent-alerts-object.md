---
title: "SQL Server Agent、Alerts 物件 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e3ea50bd513ac40995ac4ff0fc9d7eea906b0a9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server Agent、Alerts 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] SQL Server Agent 的 **Alerts** 效能物件包含效能計數器，用來報告 SQL Server Agent 警示的相關資訊。 下表列出這個物件包含的計數器。  
  
 下表包含 **SQLAgent:Alerts** 計數器。  
  
|名稱|描述|  
|----------|-----------------|  
|**Activated alerts**|這個計數器報告自從 SQL Server Agent 上次重新啟動後，SQL Server Agent 已啟動的警示總數。|  
|**Alerts activated/minute**|這個計數器報告 SQL Server Agent 在前一分鐘內所啟動的警示數目。|  
  
> [!NOTE]  
>  若要使用此 SQL Server Agent 物件，使用者必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [警示](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef)   
 [使用效能物件](http://msdn.microsoft.com/library/830b843a-6b2a-4620-a51b-98358e9fc54b)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
