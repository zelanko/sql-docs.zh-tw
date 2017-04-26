---
title: "調整作業記錄大小 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 82aede2ce0a0f0a0271e73361292628049f97875
ms.lasthandoff: 04/11/2017

---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
此主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame_md.md)]，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中設定 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] Agent 作業記錄的大小限制。  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目設定作業記錄的大小限制：**  
  
    [Transact-SQL](#SSMS)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>若要根據原始大小調整作業記錄大小  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後按一下 [屬性]。  
  
3.  選取 [記錄] 頁面，然後確認已選取 [限制作業記錄大小]。  
  
4.  在 **[最大作業記錄大小]** 方塊中，輸入作業記錄所允許的最大資料列數。  
  
5.  在 **[每項作業的作業記錄最大資料列數]** 方塊中，輸入作業所允許的最大作業記錄資料列數。  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>若要根據時間調整作業記錄大小  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後按一下 [屬性]。  
  
3.  選取 **[記錄]** 頁面，然後按一下 **[自動移除代理程式記錄]**。  
  
4.  選取適當的 [天]、[週] 或 [月] 數。  
  

