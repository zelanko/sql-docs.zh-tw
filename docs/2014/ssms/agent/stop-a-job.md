---
title: 停止作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2f2d7a8e7ae1e8e6972f98f50eb52a1b31a7ab70
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057480"
---
# <a name="stop-a-job"></a>停止作業
  此主題描述如何停止 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。 作業是 SQL Server Agent 執行的一系列指定動作。  
  
-   **開始之前：**   
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目停止作業：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果作業目前正在執行 **CmdExec** 或 **PowerShell**類型的步驟，則會強制提前結束執行中的處理序 (如 MyProgram.exe)。 提前結束可能造成無法預期的行為，例如，由維持開啟狀態的處理序所使用的檔案。  
  
-   對於多伺服器作業，作業的 STOP 指令會發佈到作業的所有目標伺服器。  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，再展開 **[作業]**，以滑鼠右鍵按一下要停止的作業，然後按一下 **[停止作業]**。  
  
3.  若要停止多個作業，請以滑鼠右鍵按一下 **[作業活動監視器]**，然後按一下 **[檢視作業活動]**。 在「作業活動監視器」中，選取要停止的作業，以滑鼠右鍵按一下選取範圍，然後按一下 **[停止作業]**。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_stop_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-stop-job-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要停止作業**  
  
 使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 `Stop` 類別的 `Job` 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
