---
title: "修改與 Agent 主要作業相關聯的目標伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 176e73b6-08aa-48ec-b349-e84b431e65cc
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f431174986975cc5b5d6f25c6e9aa89469ee94b4
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>修改與 SQL Server Agent 主要作業相關聯的目標伺服器
本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql_md.md)]中修改與 SQL Server Agent 主要作業相關聯的目標伺服器。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目來修改與 SQL Server Agent 主要作業相關聯的目標伺服器：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 主要作業無法同時存在於本機和遠端伺服器內。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
除非您是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員，否則您只能修改您所擁有的作業。 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-associated-with-a-sql-server-agent-master-job"></a>若要修改與 SQL Server Agent 主要作業相關聯的目標伺服器  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要修改目標伺服器之作業的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[作業]** 資料夾。  
  
4.  以滑鼠右鍵按一下您想要修改目標伺服器的作業，然後選取 [屬性]****。  
  
5.  在 [作業屬性 - <作業名稱>]****** 對話方塊的 [選取頁面]**** 底下，選取 [目標]****。 如需有關此頁面可用之選項的詳細資訊，請參閱[作業屬性 - 新增作業 &#40;目標頁面&#41;](../../ssms/agent/job-properties-new-job-targets-page.md)。  
  
6.  完成後，請按一下 **[確定]**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-delete-a-target-server-currently-associated-with-a-sql-server-agent-master-job"></a>若要刪除目前與 SQL Server Agent 主要作業相關聯的目標伺服器  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] ****。  
  
    ```  
    -- removes the server SEATTLE2 from processing the Weekly Sales Backupsjob   
    -- assumes that the Weekly Sales Backups job exists  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_delete_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/6d63ed32-68cf-4d8f-aa40-05a3826e05b8)。  
  
#### <a name="to-associate-a-target-server-with-the-current-sql-server-agent-master-job"></a>若要將目標伺服器與目前的 SQL Server Agent 主要作業產生關聯  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] ****。  
  
    ```  
    -- assigns the multiserver job Weekly Sales Backups to the server SEATTLE2   
    -- assumes that the Weekly Sales Backups job already exists and that   
    -- SEATTLE2 is registered as a target server for the current instance  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_jobserver  
        @job_name = N'Weekly Sales Backups',  
        @server_name = N'SEATTLE2' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286)。  
  

