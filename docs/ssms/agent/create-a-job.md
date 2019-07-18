---
title: 建立作業 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: b35af2b6-6594-40d1-9861-4d5dd906048c
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b9cbe3418e783a936893d40974cae013daa41cce
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2019
ms.locfileid: "67682447"
---
# <a name="create-a-job"></a>建立作業
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 SQL Server 管理物件 (SMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中建立 SQL Server Agent 作業。  
  
若要加入作業步驟、排程、警示以及可傳送給操作員的通知，請參閱＜請參閱＞一節中的主題連結。  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [安全性](#Security)  
  
-   **若要使用下列項目建立作業：**  
  
    [SQL Server Management Studio](#SSMSProcedure)、  
  
    [Transact-SQL](#TsqlProcedure)  
  
    [SQL Server 管理物件](#SMOProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   若要建立作業，使用者必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 只有作業擁有者或隸屬 **sysadmin** 角色的成員可以編輯作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
-   將作業指派給另一個登入並不保證新的擁有者具有充分之使用權限能夠成功執行作業。  
  
-   本機作業會由本機的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 快取。 因此，任何修改會隱含地強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 重新快取作業。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會等到呼叫 **sp_add_jobserver** 時才快取作業，所以最後再呼叫 **sp_add_jobserver** 會更有效率。  
  
### <a name="Security"></a>安全性  
  
-   您必須是系統管理員，才能夠變更作業的擁有者。  
  
-   基於安全考量，只有作業擁有者或隸屬 **sysadmin** 角色的成員可以變更作業的定義。 只有 **sysadmin** (系統管理員) 固定伺服器角色的成員可以將作業擁有權指定給其他使用者，而且無論作業擁有者是誰，都可以執行任何作業。  
  
    > [!NOTE]  
    > 如果將作業擁有權變更給非 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者，而且作業正在執行要求 Proxy 帳戶的作業步驟 (例如， [!INCLUDE[ssIS](../../includes/ssis_md.md)] 套件執行)，請確定使用者擁有該 Proxy 帳戶的存取權，否則作業將會失敗。  
  
#### <a name="Permissions"></a>Permissions  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-a-sql-server-agent-job"></a>若要建立 SQL Server Agent 作業  
  
1.  在 **[物件總管]** 中，按一下加號展開要建立 SQL Server Agent 作業的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  以滑鼠右鍵按一下 [作業]  資料夾，然後選取 [新增作業...]  。  
  
4.  在 **[新增作業]** 對話方塊的 **[一般]** 頁面中，修改作業的一般屬性。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;一般頁面&#41;](../../ssms/agent/job-properties-new-job-general-page.md)  
  
5.  在 **[步驟]** 頁面上，組織作業步驟。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;步驟頁面&#41;](../../ssms/agent/job-properties-new-job-steps-page.md)  
  
6.  在 **[排程]** 頁面上，組織作業的排程。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;排程頁面&#41;](../../ssms/agent/job-properties-new-job-schedules-page.md)  
  
7.  在 **[警示]** 頁面上，組織作業的警示。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;警示頁面&#41;](../../ssms/agent/job-properties-new-job-alerts-page.md)  
  
8.  在 **[通知]** 頁面上，設定當作業完成時， [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要執行的動作。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;通知頁面&#41;](../../ssms/agent/job-properties-new-job-notifications-page.md)。  
  
9. 在 **[目標]** 頁面上，管理作業的目標伺服器。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;目標頁面&#41;](../../ssms/agent/job-properties-new-job-targets-page.md)。  
  
10. 完成後，請按一下 **[確定]** 。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-a-sql-server-agent-job"></a>若要建立 SQL Server Agent 作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_job  
        @job_name = N'Weekly Sales Data Backup' ;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',  
        @freq_type = 1,  
        @active_start_time = 233000 ;  
    USE msdb ;  
    GO  
    EXEC sp_attach_schedule  
       @job_name = N'Weekly Sales Data Backup',  
       @schedule_name = N'RunOnce';  
    GO  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Data Backup';  
    GO  
    ```  
  
如需詳細資訊，請參閱：  
  
-   [sp_add_job (Transact-SQL)](https://msdn.microsoft.com/6ca8fe2c-7b1c-4b59-b4c7-e3b7485df274)  
  
-   [sp_add_jobstep (Transact-SQL)](https://msdn.microsoft.com/97900032-523d-49d6-9865-2734fba1c755)  
  
-   [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7)  
  
-   [sp_attach_schedule (Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)  
  
-   [sp_add_jobserver (Transact-SQL)](https://msdn.microsoft.com/485252cc-0081-490a-9bd1-cbbd68eea286)  
  
## <a name="SMOProcedure"></a>使用 SQL Server 管理物件  
**若要建立 SQL Server Agent 作業**  
  
使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 **Job** 類別的 **Create** 方法。 如需範例程式碼，請參閱 [使用 SQL Server Agent 排程自動管理工作](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)。  
  
