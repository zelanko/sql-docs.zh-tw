---
title: 建立維護計畫 | Microsoft 文件
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- maintenance plans [SQL Server], creating
ms.assetid: a945cb65-ba7a-42f4-bbd9-6ec675745523
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1dc50611e1497d84335f29d763c280cb09e9d41b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "70874747"
---
# <a name="create-a-maintenance-plan"></a>建立維護計畫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中建立單一伺服器或多伺服器維護計畫。 您可以使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]透過兩種方式的其中一種建立這些維護計畫：使用「維護計畫精靈」或設計介面。 本精靈最適用於建立基本的維護計畫，使用設計介面建立計畫時可讓您利用加強的工作流程。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
     
     [先決條件](#Prerequisite)  
  
     [安全性](#Security)  
  
-   **使用下列方法建立維護計畫：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 若要建立多伺服器維護計畫，必須設定多伺服器環境，其中包含一個主要伺服器以及一或多個目標伺服器。 多伺服器維護計畫必須在主要伺服器上建立和維護。 您可以在目標伺服器上檢視這些計畫，但不能加以維護。 
 
###  <a name="Prerequisite"></a> 必要條件  
必須啟用 [Agent XPs 伺服器組態選項](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) 。
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 若要建立或管理維護計畫，您必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-maintenance-plan-using-the-maintenance-plan-wizard"></a>若要使用維護計畫精靈來建立維護計畫  
  
1.  在 [物件總管] 中，按一下加號以展開您要建立維護計畫的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [維護計畫]  資料夾，然後選取 [維護計畫精靈]  。  
  
4.  請遵循精靈的步驟來建立維護計畫。 如需詳細資訊，請參閱 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  
#### <a name="to-create-a-maintenance-plan-using-the-design-surface"></a>使用設計介面建立維護計畫  
  
1.  在 [物件總管] 中，按一下加號以展開您要建立維護計畫的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [維護計畫]  資料夾，然後選取 [新增維護計畫]  。  
  
4.  遵循[建立維護計畫 &#40;維護計畫設計介面&#41;](../../relational-databases/maintenance-plans/create-a-maintenance-plan-maintenance-plan-design-surface.md) 中的步驟建立維護計畫。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-maintenance-plan"></a>若要建立維護計畫  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    USE msdb;  
    GO  
    --  Adds a new job, executed by the SQL Server Agent service, called "HistoryCleanupTask_1".  
    EXEC dbo.sp_add_job  
       @job_name = N'HistoryCleanupTask_1',   
       @enabled = 1,   
       @description = N'Clean up old task history' ;   
    GO  
    -- Adds a job step for reorganizing all of the indexes in the HumanResources.Employee table to the HistoryCleanupTask_1 job.   
    EXEC dbo.sp_add_jobstep  
        @job_name = N'HistoryCleanupTask_1',   
        @step_name = N'Reorganize all indexes on HumanResources.Employee table',   
        @subsystem = N'TSQL',   
        @command = N'USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_LoginID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX AK_Employee_rowguid ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX IX_Employee_OrganizationNode ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    USE AdventureWorks2012  
    GO  
    ALTER INDEX PK_Employee_BusinessEntityID ON HumanResources.Employee REORGANIZE WITH ( LOB_COMPACTION = ON )   
    GO  
    ',   
        @retry_attempts = 5,   
        @retry_interval = 5 ;   
    GO  
    -- Creates a schedule named RunOnce that executes every day when the time on the server is 23:00.   
    EXEC dbo.sp_add_schedule  
        @schedule_name = N'RunOnce',   
        @freq_type = 4,   
        @freq_interval = 1,   
        @active_start_time = 233000 ;   
    GO  
    -- Attaches the RunOnce schedule to the job HistoryCleanupTask_1.   
    EXEC sp_attach_schedule  
       @job_name = N'HistoryCleanupTask_1',  
       @schedule_name = N'RunOnce' ;   
    GO  
  
    ```  
  
 如需詳細資訊，請參閱  
  
-   [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)  
  
-   [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)  
  
-   [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
