---
title: 修改作業的目標伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 246a5bb59a681a70734cc8cabef4f724cda1b52e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048788"
---
# <a name="modify-the-target-servers-for-a-job"></a>修改作業的目標伺服器
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，在中變更 Agent 作業的目標伺服器 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要修改作業的目標伺服器，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 根據預設，系統管理員固定伺服器角色的成員可執行此預存程序。 其他使用者必須獲得授與 msdb 資料庫的下列其中一個 SQL Server Agent 固定資料庫角色：  
  
1.  `SQLAgentUserRole`  
  
2.  `SQLAgentReaderRole`  
  
3.  SQLAgentOperatorRole  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>若要為作業修改目標伺服器  
  
1.  在 [物件總管]**** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent]**** 和 [作業]****、以滑鼠右鍵按一下某個作業，然後按一下 [屬性]****。  
  
3.  在 [作業屬性]**** 對話方塊中，選取 [目標]**** 頁面，然後按一下 [目標本機伺服器]**** 或 [目標多個伺服器]****。  
  
     如果選擇 **[目標多個伺服器]**，請選取伺服器名稱左邊的方塊，以指定要做為作業目標的伺服器。 至於不要做為作業目標的伺服器，請確認已取消選取其核取方塊。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>若要為作業修改目標伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例會將多伺服器作業 Weekly Sales Backups 指派給伺服器 SEATTLE2。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
  
```  
  
 如需詳細資訊，請參閱[sp_add_jobserver &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [將整個企業的管理自動化](automated-administration-across-an-enterprise.md)  
  
  
