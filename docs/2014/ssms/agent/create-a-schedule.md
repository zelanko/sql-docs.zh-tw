---
title: 建立排程 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
- schedules [SQL Server], jobs
ms.assetid: 8c7ef3b3-c06d-4a27-802d-ed329dc86ef3
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d95cf8a8be2f61a08e8773e8233b840c89aa743c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808344"
---
# <a name="create-a-schedule"></a>Create a Schedule
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中建立 [!INCLUDE[tsql](../../includes/tsql-md.md)]Agent 作業的排程。  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目建立排程：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-schedule"></a>建立排程  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**、以滑鼠右鍵按一下 **[作業]**，然後選取 **[管理排程]**。  
  
3.  在 **[管理排程]** 對話方塊中，按一下 **[新增]**。  
  
4.  在 **[名稱]** 方塊中，輸入新排程的名稱。  
  
5.  如果您不想要讓排程在建立之後立即生效，請清除 **[已啟用]** 核取方塊。  
  
6.  針對 **[排程類型]**，選取下列其中一項：  
  
    -   若要在 CPU 達到閒置條件時啟動此作業，請按一下 **[只要 CPU 閒置就啟動]**。  
  
    -   如果您想要重複執行排程，按一下 **[重複執行]**。 若要設定重複執行的排程，請完成對話方塊上的 **[頻率]**、 **[每日頻率]** 和 **[持續時間]** 群組。  
  
    -   如果您想要讓排程只執行一次，請按一下 **[執行一次]**。 若要設定 **[執行一次]** 排程，請完成對話方塊上的 **[僅發生一次]** 群組。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-schedule"></a>建立排程  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- creates a schedule named RunOnce.   
    -- The schedule runs one time, at 23:30 on the day that the schedule is created.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_add_schedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **建立排程**  
  
 使用`JobSchedule`藉由使用您選擇，例如 Visual Basic、 Visual C# 或 PowerShell 的程式語言的類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
