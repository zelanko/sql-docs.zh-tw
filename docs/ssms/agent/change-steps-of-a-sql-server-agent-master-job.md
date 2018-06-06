---
title: 變更 SQL Server Agent 主要作業的步驟 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f1a0ee6-49ff-4080-94ca-d661daeff2a6
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 499e9ab5507b115d495276abcc0a9df2a9765a95
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="change-steps-of-a-sql-server-agent-master-job"></a>Change Steps of a SQL Server Agent Master Job
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql_md.md)]中變更 SQL Server Agent 主要作業的步驟。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目來變更 SQL Server Agent 主要作業的步驟：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 主要作業無法同時存在於本機和遠端伺服器內。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
除非您是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員，否則您只能修改您所擁有的作業。 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>若要變更 SQL Server Agent 主要作業的步驟  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要修改步驟之作業的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[作業]** 資料夾。  
  
4.  以滑鼠右鍵按一下您想要修改步驟的作業，然後選取 [屬性]。  
  
5.  在 [作業屬性 - <作業名稱>] 對話方塊的 [選取頁面] 底下，選取 [步驟]。  
  
6.  按一下 [編輯] 開啟 [作業步驟屬性 - <作業步驟名稱>] 對話方塊。 如需此對話方塊中可用選項的詳細資訊，請參閱[作業步驟屬性 - 新增作業步驟 &#40;一般頁面&#41;](../../ssms/agent/job-step-properties-new-job-step-general-page.md) 和[作業步驟屬性 - 新增作業步驟 &#40;進階頁面&#41;](../../ssms/agent/job-step-properties-new-job-step-advanced-page.md)。  
  
7.  完成後，請按一下 **[確定]**。  
  
8.  在 [作業屬性 - <作業名稱>] 對話方塊中，按一下 [確定]。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>若要變更 SQL Server Agent 主要作業的步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- changes the number of retry attempts for the first step
    -- of the Weekly Sales Data Backup job.   
    -- After running this example, the number of retry attempts is 10   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1,  
        @retry_attempts = 10 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_update_jobstep (Transact-SQL)](http://msdn.microsoft.com/en-us/e158802c-c347-4a5d-bf75-c03e5ae56e6b)。  
  
