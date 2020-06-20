---
title: 將作業擁有權授與其他人 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2cf03fdc9031ce9761125d95619438837f2959bb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067782"
---
# <a name="give-others-ownership-of-a-job"></a>將作業擁有權授與其他人
  本主題描述如何將 Agent 作業的擁有權重新指派 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 給另一位使用者。  
  
-   **開始之前：**  [限制事項](#Restrictions)、[安全性](#Security)  
  
-   **若要使用下列項目賦予作業擁有權給其他人：**  
  
     [Transact-SQL](#SSMSProc2)  
  
     [Transact-SQL](#TsqlProc2)  
  
     [SQL Server 管理物件](#SMOProc2)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 若要建立作業，使用者必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 只有作業擁有者或隸屬 **sysadmin** 角色的成員可以編輯作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)。  
  
 您必須是系統管理員，才能夠變更作業的擁有者。  
  
 將作業指派給另一個登入並不保證新的擁有者具有充分之使用權限能夠成功執行作業。  
  
###  <a name="security"></a><a name="Security"></a> Security  
 基於安全考量，只有作業擁有者或隸屬 **sysadmin** 角色的成員可以變更作業的定義。 只有 **sysadmin** (系統管理員) 固定伺服器角色的成員可以將作業擁有權指定給其他使用者，而且無論作業擁有者是誰，都可以執行任何作業。  
  
> [!NOTE]  
>  如果將作業擁有權變更給非 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者，而且作業正在執行要求 Proxy 帳戶的作業步驟 (例如， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 套件執行)，請確定使用者擁有該 Proxy 帳戶的存取權，否則作業將會失敗。  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProc2"></a> 使用 SQL Server Management Studio  
 **若要賦予作業擁有權給其他人**  
  
1.  在 [物件總管]**** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent]**** 和 [作業]****、以滑鼠右鍵按一下作業，然後按一下 [屬性]****。  
  
3.  在 **[擁有者]** 清單選取登入。 您必須是系統管理員，才能夠變更作業的擁有者。  
  
     將作業指派給另一個登入並不保證新的擁有者具有充分之使用權限能夠成功執行作業。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProc2"></a> 使用 Transact-SQL  
 **若要賦予作業擁有權給其他人**  
  
1.  在 [物件總管] 中，連接到 Database Engine 的執行個體，然後展開該執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]**。  
  
3.  在查詢視窗中，輸入下列語句，以使用[sp_manage_jobs_by_login &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql)系統預存程式。 下列範例會將 `danw` 的所有作業重新指派給 `fran??oisa`。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'fran??oisa' ;  
    GO  
    ```  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMOProc2"></a>使用 SQL Server 管理物件  

### <a name="to-give-others-ownership-of-a-job"></a>若要賦予作業擁有權給其他人
  
1.  使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell 呼叫 `Job` 類別。 如需範例程式碼，請參閱 [使用 SQL Server Agent 排程自動管理工作](sql-server-agent.md)。  
  
## <a name="see-also"></a>另請參閱  
 [執行作業](implement-jobs.md)   
 [建立作業](create-jobs.md)  
