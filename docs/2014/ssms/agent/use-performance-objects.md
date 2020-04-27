---
title: 使用效能物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ccba43aa28cadef1995fab001f66e1f4bebacde
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245844"
---
# <a name="use-performance-objects"></a>使用效能物件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 包含效能物件及計數器，可用來監視服務執行的狀況。 這些效能物件可讓您使用「效能監視器」(一種 Windows 工具)，來識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務在背景執行哪些工作。 例如，您可以識別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務目前正在執行多少使用中的作業，以找出被封鎖的作業。  
  
 針對電腦上所安裝的每一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，都有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件及計數器存在。 效能物件是依據每項物件所代表的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體來命名的。  
  
 下表顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務效能物件的命名方式：  
  
|執行個體類型|物件名稱|  
|-------------------|-----------------|  
|預設|**SQLAgent:** *object*:*counter*|  
|已命名|**SQLAgent$**<br /> ***instance_name* ：** *object*：*計數器*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的下列效能物件。  
  
|物件名稱|描述|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|有關已啟動作業、成功率及目前狀態的效能資訊|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|作業步驟的狀態資訊|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警示及通知數的相關資訊|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|一般效能資訊|  
  
## <a name="see-also"></a>另請參閱  
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [啟動系統監視器 &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
