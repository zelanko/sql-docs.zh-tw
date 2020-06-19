---
title: 建立 SQL Server Agent 主要作業 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], master jobs
- jobs [SQL Server Agent], creating
- master SQL Server Agent job [SQL Server]
ms.assetid: c12ab23f-d7ee-43a5-8cd2-0a9121292bcd
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8a6503caec3f153878e360ee29ce09a5c099ade5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064527"
---
# <a name="create-a-sql-server-agent-master-job"></a>建立 SQL Server Agent 主要作業
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，在中建立主要代理程式作業 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 主要作業的變更必須傳播至所有相關的目標伺服器。 因為目標伺服器最初並未下載作業，直到指定這些目標後才下載，所以 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您先完成特定作業的所有作業步驟和作業排程，再指定任何目標伺服器。 否則，您必須執行 **sp_post_msx_operation** 預存程序或使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]修改作業，手動要求目標伺服器重新下載已修改的作業。 如需詳細資訊，請參閱[sp_post_msx_operation &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)或[修改作業](modify-a-job.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 具有與 Proxy 相關聯之步驟的散發式作業，而該 Proxy 是在目標伺服器上的 Proxy 帳戶內容下執行 。 請確保符合以下條件，否則與 Proxy 相關聯之作業步驟將不會從主要伺服器下載至目標：  
  
-   登錄子機碼**\ HKEY_LOCAL_MACHINE \software\microsoft\microsoft SQL Server \\ < *instance_name*> \sql 伺服器 Agent\AllowDownloadedJobsToMatchProxyName** （REG_DWORD）已設定為1（true）。 依預設，這個子機碼設為 0 (False)。  
  
-   存在於目標伺服器上的 Proxy 帳戶，而該帳戶名稱與執行作業步驟之主要伺服器上的 Proxy 帳戶名稱相同。  
  
 如果使用 Proxy 帳戶的作業步驟在從主要伺服器下載 Proxy 帳戶至目標伺服器時失敗，您可以在 **msdb** 資料庫的 **sysdownloadlist** 資料表中，檢查 **error_message** 資料行，以了解下列錯誤訊息：  
  
-   「作業步驟需要 Proxy 帳戶，不過目標伺服器上已停用 Proxy 比對。」 若要解決這個錯誤，請將 **AllowDownloadedJobsToMatchProxyName** 登錄子機碼設為 1。  
  
-   「找不到 Proxy。」 若要解決這個錯誤，請確定目標伺服器上有 Proxy 帳戶，且帳戶名稱與執行該作業步驟的主要伺服器 Proxy 帳戶相同。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>若要建立 SQL Server Agent 的主要作業  
  
1.  在 **[物件總管]** 中，按一下加號展開要建立 SQL Server Agent 作業的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [作業]**** 資料夾，然後選取 [新增作業...]****。  
  
4.  在 **[新增作業]** 對話方塊的 **[一般]** 頁面中，修改作業的一般屬性。 如需有關此頁面上可用選項的詳細資訊，請參閱[作業屬性和新增作業 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
5.  在 **[步驟]** 頁面上，組織作業步驟。 如需有關此頁面上可用選項的詳細資訊，請參閱[作業屬性：新增作業 &#40;步驟頁面&#41;](job-properties-new-job-steps-page.md)  
  
6.  在 **[排程]** 頁面上，組織作業的排程。 如需有關此頁面上可用選項的詳細資訊，請參閱[作業屬性：新增作業 &#40;排程頁面&#41;](job-properties-new-job-schedules-page.md)  
  
7.  在 **[警示]** 頁面上，組織作業的警示。 如需有關此頁面上可用選項的詳細資訊，請參閱[作業屬性：新增作業 &#40;警示頁面&#41;](job-properties-new-job-alerts-page.md)  
  
8.  在 [通知]**** 頁面上設定當作業完成時，[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行的動作。 如需有關此頁面上可用選項的詳細資訊，請參閱[作業屬性：新增作業 &#40;通知頁面&#41;](job-properties-new-job-notifications-page.md)。  
  
9. 在 **[目標]** 頁面上，管理作業的目標伺服器。 如需有關此頁面上可用選項的詳細資訊，請參閱[工作屬性：新增作業 &#40;目標頁面&#41;](job-properties-new-job-targets-page.md)。  
  
10. 完成時按一下 **[確定]**。  
  

  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-master-sql-server-agent-job"></a>若要建立 SQL Server Agent 的主要作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE msdb ;  
    GO  
    -- Adds a new job executed by the SQLServerAgent service called 'Weekly Sales Data Backup'  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    -- Adds a step (operation) to the 'Weekly Sales Data Backup' job.  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    -- Creates a schedule called RunOnce  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    -- Sets the 'RunOnce' schedule to the "Weekly Sales Data Backup' Job  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2  
    -- assumes that SEATTLE2 is registered as a target server for the current instance.  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱  
  
-   [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_add_jobserver &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  

  
  
