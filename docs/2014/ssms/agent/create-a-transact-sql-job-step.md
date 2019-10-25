---
title: 建立 Transact-SQL 作業步驟 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: 69c571a7-debe-4063-9d38-e4b6a1e8e84c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 488e07e86ba5a7febcb0675611136a1e0d792007
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798255"
---
# <a name="create-a-transact-sql-job-step"></a>Create a Transact-SQL Job Step
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟。  
  
 這些作業步驟指令碼可呼叫預存程序及擴充預存程序。 單一 [!INCLUDE[tsql](../../includes/tsql-md.md)] 作業步驟可包含多個批次和內嵌 GO 命令。 如需建立作業的詳細資訊，請參閱＜ [建立作業](create-jobs.md)＞。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目建立 Transact-SQL 作業步驟：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> Security  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-transact-sql-job-step"></a>若要建立 Transact-SQL 作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]** ，建立新作業或以滑鼠右鍵按一下現有作業，然後按一下 **[屬性]** 。  
  
3.  在 **[作業屬性]** 方塊中，按一下 **[步驟]** 頁面，然後按一下 **[新增]** 。  
  
4.  在 **[新增作業步驟]** 對話方塊中，輸入一個作業 **步驟名稱**。  
  
5.  在 [類型] 清單中，按一下 [Transact-SQL 指令碼 (TSQL)]。  
  
6.  在 **[命令]** 方塊中，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令批次，或按一下 **[開啟舊檔]** 來選取要作為命令使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 檔。  
  
7.  按一下 **[剖析]** 來檢查語法。  
  
8.  當語法正確時，會顯示「剖析成功」的訊息。 如果出現錯誤訊息，請修正語法後再繼續。  
  
9. 按一下 **[進階]** 頁面來設定作業步驟選項，例如：作業步驟成功或失敗時要採取的動作、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 應嘗試執行作業步驟的次數，以及可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 寫入作業步驟輸出的檔案或資料表。 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，可以將作業步驟輸出寫入作業系統檔案。 所有 SQL Server Agent 使用者都可以將輸出記錄到資料表中。  
  
10. 如果您是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，而您想以不同的 SQL 登入執行這個作業步驟，請從 **[指定執行時的身分]** 清單中選取 SQL 登入。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-transact-sql-job-step"></a>若要建立 Transact-SQL 作業步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- creates a job step that uses Transact-SQL  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)。  
  
##  <a name="SMO"></a>使用 SQL Server 管理物件  
 **若要建立 Transact-SQL 作業步驟**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `JobStep` 類別。  
