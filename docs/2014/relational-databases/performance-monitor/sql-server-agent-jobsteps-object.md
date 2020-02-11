---
title: SQL Server Agent、JobSteps 物件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 323bf0c943d12a2d05e5fde80194d35d9ab733cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206558"
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server Agent、JobSteps 物件
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **JobSteps**效能物件包含效能計數器，可報告 Agent 作業[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]步驟的相關資訊。 下表列出這個物件包含的計數器。  
  
 下表包含 **SQLAgent:JobSteps** 計數器。  
  
|名稱|描述|  
|----------|-----------------|  
|**活動步驟**|此計數器會報告目前在執行中的作業步驟數目。|  
|**排入佇列的步驟**|此計數器會報告準備供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行，但尚未開始執行的作業步驟數目。|  
|**總步驟重試次數**|此計數器會報告自從上次伺服器重新開機[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之後，重試作業步驟的總次數。|  
  
 物件中的每個計數器均包含下列執行個體：  
  
|執行個體|描述|  
|--------------|-----------------|  
|**_Total**|所有作業步驟的資訊。|  
|**ActiveScripting**|使用 **ActiveScripting** 子系統之作業步驟的資訊。|  
|**ANALYSISCOMMAND**|使用 ANALYSISCOMMAND 子系統之作業步驟的資訊。|  
|**ANALYSISQUERY**|使用 ANALYSISQUERY 子系統之作業步驟的資訊。|  
|**CmdExec**|使用 **CmdExec** 子系統之作業步驟的資訊。|  
|**散發**|使用 **Distribution** 子系統之作業步驟的資訊。|  
|**Dt**|使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 子系統之作業步驟的資訊。|  
|**讀取**|使用 **LogReader** 子系統之作業步驟的資訊。|  
|**合併式**|使用 **Merge** 子系統之作業步驟的資訊。|  
|**PowerShell**|使用 **PowerShell** 子系統之作業步驟的資訊。|  
|**QueueReader**|使用 **QueueReader** 子系統之作業步驟的資訊。|  
|**快照式**|使用 **Snapshot** 子系統之作業步驟的資訊。|  
|**T Q**|執行 [!INCLUDE[tsql](../../includes/tsql-md.md)]之作業步驟的資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [管理作業步驟](../../ssms/agent/manage-job-steps.md)   
 [使用效能物件](../../ssms/agent/use-performance-objects.md)   
 [監視資源使用狀況 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)  
  
  
