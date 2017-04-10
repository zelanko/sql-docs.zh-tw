---
title: "SQL Server Agent、Alerts 物件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Alerts 物件"
  - "SQLAgent:Alerts"
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
caps.latest.revision: 24
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 24
---
# SQL Server Agent、Alerts 物件
  SQL Server Agent 的「 **警示** 」效能物件包含效能計數器，用來報告 SQL Server Agent 警示的詳細資訊。 下表列出這個物件包含的計數器。  
  
 下表包含 **SQLAgent:Alerts** 計數器。  
  
|名稱|描述|  
|----------|-----------------|  
|**Activated alerts**|這個計數器報告自從 SQL Server Agent 上次重新啟動後，SQL Server Agent 已啟動的警示總數。|  
|**Alerts activated/minute**|這個計數器報告 SQL Server Agent 在前一分鐘內所啟動的警示數目。|  
  
> [!NOTE]  
>  若要使用此 SQL Server Agent 物件，使用者必須是**系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## 另請參閱  
 [警示](../../ssms/agent/alerts.md)   
 [使用效能物件](../../ssms/agent/use-performance-objects.md)   
 [監視資源使用狀況 &#40;系統監視器&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  