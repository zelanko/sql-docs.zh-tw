---
title: 變更 SQL Server Agent 主要作業的步驟 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 8f1a0ee6-49ff-4080-94ca-d661daeff2a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1a60d9e5d8569324cc3f68200d4a5a232b930d8b
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133258"
---
# <a name="change-steps-of-a-sql-server-agent-master-job"></a>變更 SQL Server Agent 主要作業的步驟
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中變更 SQL Server Agent 主要作業的步驟。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目來變更 SQL Server Agent 主要作業的步驟：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 主要作業無法同時存在於本機和遠端伺服器內。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 除非您是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員，否則您只能修改您所擁有的作業。 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>若要變更 SQL Server Agent 主要作業的步驟  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要修改步驟之作業的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[作業]** 資料夾。  
  
4.  以滑鼠右鍵按一下您想要修改步驟的作業，然後選取 [屬性]。  
  
5.  在 [作業屬性 -_job_name_] 對話方塊的 [選取頁面] 下，選取 [步驟]。  
  
6.  按一下 [**編輯**來開啟**作業步驟屬性-**_<_ ] 對話方塊。 如需有關此對話方塊中可用之選項的詳細資訊，請參閱[作業步驟屬性：新增作業步驟&#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)並[作業步驟屬性：新增作業步驟&#40;進階頁面&#41;](job-step-properties-new-job-step-advanced-page.md)。  
  
7.  完成後，請按一下 **[確定]**。  
  
8.  在 **作業屬性-**_job_name_  對話方塊中，按一下 **確定**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>若要變更 SQL Server Agent 主要作業的步驟  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] 。  
  
    ```  
    -- changes the number of retry attempts for the first step of the Weekly Sales Data Backup job.   
    -- After running this example, the number of retry attempts is 10   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1,  
        @retry_attempts = 10 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_update_jobstep &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)。  
  
  
