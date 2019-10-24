---
title: 刪除作業步驟記錄檔 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server Agent]
- deleting job step logs
- logs [SQL Server], jobs
- removing job step logs
ms.assetid: ee20c6cd-0258-4550-bdb0-71e86a0fb330
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cd6cefd41ea223b91445042ff3cee9090074feeb
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783187"
---
# <a name="delete-a-job-step-log"></a>Delete a Job Step Log
  本主題描述如何刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業步驟記錄。  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目刪除 SQL Server Agent 作業步驟記錄：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 刪除作業步驟時，會自動刪除其輸出記錄檔。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> Permissions  
 除非您是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員，否則您只能修改您所擁有的作業。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>若要刪除 SQL Server Agent 作業步驟記錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 [SQL Server Agent]，展開 [作業]，以滑鼠右鍵按一下要修改的作業，然後按一下 [屬性]。  
  
3.  在 **[作業屬性]** 對話方塊中，刪除選取的作業步驟。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-job-step-log"></a>若要刪除 SQL Server Agent 作業步驟記錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]** 。  
  
    ```sql
    -- removes the job step log for step 2 in the job Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_jobsteplog  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 2;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_delete_jobsteplog &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql)。  
  
##  <a name="SMO"></a>使用 SQL Server 管理物件  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `DeleteJobStepLogs` 類別的 `Job` 方法。 如需詳細資訊，請參閱[SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
```powershell
# Delete all job step log files that have ID values larger than 5.  
$srv = New-Object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = $srv.JobServer.Jobs["Test Job"]  
$jb.DeleteJobStepLogs(5)  
```
