---
title: "停止作業 | Microsoft Docs"
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
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d27aed059ea689f726b6feaf25e22989da0639e7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="stop-a-job"></a>停止作業
此主題描述如何停止 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業。 作業是 SQL Server Agent 執行的一系列指定動作。  
  
-   **開始之前：**   
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目停止作業：**  
  
    [Transact-SQL](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   如果作業目前正在執行 **CmdExec** 或 **PowerShell**類型的步驟，則會強制提前結束執行中的處理序 (如 MyProgram.exe)。 提前結束可能造成無法預期的行為，例如，由維持開啟狀態的處理序所使用的檔案。  
  
-   對於多伺服器作業，作業的 STOP 指令會發佈到作業的所有目標伺服器。  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，再展開 **[作業]**，以滑鼠右鍵按一下要停止的作業，然後按一下 **[停止作業]**。  
  
3.  若要停止多個作業，請以滑鼠右鍵按一下 **[作業活動監視器]**，然後按一下 **[檢視作業活動]**。 在「作業活動監視器」中，選取要停止的作業，以滑鼠右鍵按一下選取範圍，然後按一下 **[停止作業]**。  
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-stop-a-job"></a>若要停止作業  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] 。  
  
    ```  
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_stop_job (Transact-SQL)](http://msdn.microsoft.com/en-us/64b4cc75-99a0-421e-b418-94e37595bbb0)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要停止作業**  
  
使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 **Job** 類別的 **Stop** 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  

