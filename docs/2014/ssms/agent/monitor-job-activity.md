---
title: 監視作業活動 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d6e77a3553e8b56dde7e0138e8ad8072ee00fa33
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43819444"
---
# <a name="monitor-job-activity"></a>監視作業活動
  您可以使用「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業活動監視器」，監視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上所有已定義作業的目前活動。  
  
## <a name="sql-server-agent-sessions"></a>SQL Server Agent 工作階段  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次服務啟動時，Agent 都會建立新的工作階段。 建立新的工作階段時， **msdb** 資料庫中的 **sysjobactivity** 資料表就會填入所有現有的已定義作業。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 重新啟動時，這個資料表會保留作業的上一個活動。 每一個工作階段會記錄從作業開始到完成的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 一般作業活動。 這些工作階段的相關資訊儲存在 **msdb** 資料庫的 **syssessions** 資料表中。  
  
## <a name="job-activity-monitor"></a>作業活動監視器  
 「作業活動監視器」可讓您使用 **檢視** sysjobactivity [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料表。 您可以檢視伺服器上的所有作業，或者您也可以定義篩選，來限制所顯示的作業數目。 您也可以按一下 [代理程式作業活動] 方格中的資料行標題，排序作業資訊。 例如，選取 [上次執行] 資料行標題時，可以按作業上次執行的順序來檢視作業； 再按一下資料行標題，可切換作業依上次執行日期的遞增或遞減順序來顯示。  
  
 使用「作業活動監視器」，您可以執行下列工作：  
  
-   啟動和停止作業。  
  
-   檢視作業屬性。  
  
-   檢視特定作業的記錄。  
  
-   以手動方式重新整理 [代理程式作業活動] 方格中的資訊，或按一下 [檢視重新整理設定] 設定自動重新整理間隔。  
  
 當您想要了解有哪些作業已排程執行、目前工作階段期間已執行作業的最後結果，以及找出哪些作業目前執行中或閒置時，便可使用「作業活動監視器」。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務異常失敗，您可以查看「作業活動監視器」中的先前工作階段，判斷哪些作業原本正在執行中。  
  
 若要開啟「作業活動監視器」，請展開「[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 物件總管」中的 [SQL Server Agent]、以滑鼠右鍵按一下 [作業活動監視器]，然後按一下 [檢視作業活動]。  
  
 您也可以使用預存程序 **sp_help_jobactivity** 來檢視目前工作階段的作業活動。  
  
## <a name="related-tasks"></a>相關工作  
  
|||  
|-|-|  
|**說明**|**主題**|  
|描述如何檢視 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的執行階段狀態。|[View Job Activity](view-job-activity.md)|  
  
## <a name="see-also"></a>另請參閱  
 [檢視作業活動](view-job-activity.md)   
 [dbo.sysjobactivity &#40;Transact SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobactivity-transact-sql)   
 [dbo.syssessions &#40;Transact SQL&#41;](/sql/relational-databases/system-tables/dbo-syssessions-transact-sql)   
 [sp_help_jobactivity &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql)  
  
  
