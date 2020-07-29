---
title: 排定作業執行時間
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scheduling jobs [SQL Server]
- SQL Server Agent jobs, scheduling
- jobs [SQL Server Agent], scheduling
ms.assetid: f626390a-a3df-4970-b7a7-a0529e4a109c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4c7b5d10e497cb87c2ac90b5d009a074c97b1597
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644730"
---
# <a name="schedule-a-job"></a>排定作業執行時間
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何排程 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
-   **開始之前：**  
  
    [安全性](#Security)  
  
-   **若要使用下列項目排程作業：**  
  
    [Transact-SQL](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="security"></a><a name="Security"></a>安全性  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-and-attach-a-schedule-to-a-job"></a>若要建立並附加排程至作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent]  和 [作業]  、以滑鼠右鍵按一下要排程的作業，然後按一下 [屬性]  。  
  
3.  按一下 **[排程]** 頁面，然後按一下 **[新增]** 。  
  
4.  在 **[名稱]** 方塊中，輸入新排程的名稱。  
  
5.  如果您不要排程在建立後立即生效，請清除 **[啟用]** 核取方塊。  
  
6.  針對 **[排程類型]** ，選取下列其中一項：  
  
    -   按一下 **[當 SQL Server Agent 啟動時自動啟動]** ，以在啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務時啟動作業。  
  
    -   按一下 **[只要 CPU 閒置就啟動]** ，以便在 CPU 到達閒置條件時啟動作業。  
  
    -   如果您想要重複執行排程，請按一下 **[重複執行]** 。 若要設定重複執行的排程，請完成對話方塊上的 **[頻率]** 、 **[每日頻率]** 和 **[持續時間]** 群組。  
  
    -   如果您只要排程執行一次，請按一下 **[執行一次]** 。 若要設定 [執行一次]  排程，請完成對話方塊上的 [僅執行一次]  群組。  
  
#### <a name="to-attach-a-schedule-to-a-job"></a>附加排程至作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent]  和 [作業]  、以滑鼠右鍵按一下要排程的作業，然後按一下 [屬性]  。  
  
3.  選取 **[排程]** 頁面，然後按一下 **[挑選]** 。  
  
4.  選取您想要附加的排程，然後按一下 **[確定]** 。  
  
5.  在 [作業屬性]  對話方塊中，按兩下附加的排程。  
  
6.  確認 **[開始日期]** 的設定是否正確。 如果不正確，請設定您想要讓排程啟動的日期，然後按一下 **[確定]** 。  
  
7.  在 **[作業屬性]** 對話方塊中，按一下 **[確定]** 。  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-schedule-a-job"></a>排程作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE msdb ;  
    GO  
    -- creates a schedule named NightlyJobs.   
    -- Jobs that use this schedule execute every day when the time on the server is 01:00.   
    EXEC sp_add_schedule  
        @schedule_name = N'NightlyJobs' ,  
        @freq_type = 4,  
        @freq_interval = 1,  
        @active_start_time = 010000 ;  
    GO  
    -- attaches the schedule to the job BackupDatabase  
    EXEC sp_attach_schedule  
       @job_name = N'BackupDatabase',  
       @schedule_name = N'NightlyJobs' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_schedule (Transact-SQL)](https://msdn.microsoft.com/9060aae3-3ddd-40a5-83bb-3ea7ab1ffbd7) 和 [sp_attach_schedule (Transact-SQL)](https://msdn.microsoft.com/80c80eaf-cf23-4ed8-b8dd-65fe59830dd1)。  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>使用 SQL Server 管理物件  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **JobSchedule** 類別。 如需詳細資訊，請參閱[SQL Server 管理物件 (SMO)](https://msdn.microsoft.com/library/ms162169.aspx)。  
  
