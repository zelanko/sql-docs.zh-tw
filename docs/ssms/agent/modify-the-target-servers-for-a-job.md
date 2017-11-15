---
title: "修改作業的目標伺服器 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 953bff191540cd6045d8e82e46d60d1efb6a2b15
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="modify-the-target-servers-for-a-job"></a>Modify the Target Servers for a Job
本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中變更 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業的目標伺服器。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要修改作業的目標伺服器，使用：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
依預設，只有系統管理員 (sysadmin) 固定伺服器角色的成員，才能夠執行這個預存程序。 其他使用者必須獲得授與 msdb 資料庫的下列其中一個 SQL Server Agent 固定資料庫角色：  
  
1.  **SQLAgentUserRole**  
  
2.  **SQLAgentReaderRole**  
  
3.  SQLAgentOperatorRole  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>若要為作業修改目標伺服器  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent] 和 [作業]、以滑鼠右鍵按一下某個作業，然後按一下 [屬性]。  
  
3.  在 [作業屬性] 對話方塊中，選取 [目標] 頁面，然後按一下 [目標本機伺服器] 或 [目標多個伺服器]。  
  
    如果選擇 **[目標多個伺服器]**，請選取伺服器名稱左邊的方塊，以指定要做為作業目標的伺服器。 至於不要做為作業目標的伺服器，請確認已取消選取其核取方塊。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>若要為作業修改目標伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 這個範例會將多伺服器作業 Weekly Sales Backups 指派給伺服器 SEATTLE2。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
```  
  
如需詳細資訊，請參閱 [sp_add_jobserver (Transact-SQL)](http://msdn.microsoft.com/en-us/485252cc-0081-490a-9bd1-cbbd68eea286)。  
  
## <a name="see-also"></a>另請參閱  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
