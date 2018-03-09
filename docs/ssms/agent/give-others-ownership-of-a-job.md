---
title: "將作業擁有權授與其他人 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c6fc8870f446b9b34f55c965ad13132e6ce7d418
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何將 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業的擁有權重新指派給其他使用者。  
  
-   **開始之前：**[限制事項](#Restrictions)、[安全性](#Security)  
  
-   **若要使用下列項目賦予作業擁有權給其他人：**  
  
    [Transact-SQL](#SSMSProc2)  
  
    [Transact-SQL](#TsqlProc2)  
  
    [SQL Server 管理物件](#SMOProc2)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
若要建立作業，使用者必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 固定資料庫角色或 **系統管理員 (sysadmin)** 固定伺服器角色的成員。 只有作業擁有者或隸屬 **sysadmin** 角色的成員可以編輯作業。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 固定資料庫角色的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
您必須是系統管理員，才能夠變更作業的擁有者。  
  
將作業指派給另一個登入並不保證新的擁有者具有充分之使用權限能夠成功執行作業。  
  
### <a name="Security"></a>Security  
基於安全考量，只有作業擁有者或隸屬 **sysadmin** 角色的成員可以變更作業的定義。 只有 **sysadmin** (系統管理員) 固定伺服器角色的成員可以將作業擁有權指定給其他使用者，而且無論作業擁有者是誰，都可以執行任何作業。  
  
> [!NOTE]  
> 如果將作業擁有權變更給非 **系統管理員 (sysadmin)** 固定伺服器角色成員的使用者，而且作業正在執行要求 Proxy 帳戶的作業步驟 (例如， [!INCLUDE[ssIS](../../includes/ssis_md.md)] 套件執行)，請確定使用者擁有該 Proxy 帳戶的存取權，否則作業將會失敗。  
  
#### <a name="Permissions"></a>Permissions  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMSProc2"></a>使用 SQL Server Management Studio  
**若要賦予作業擁有權給其他人**  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent] 和 [作業]、以滑鼠右鍵按一下作業，然後按一下 [屬性]。  
  
3.  在 **[擁有者]** 清單選取登入。 您必須是系統管理員，才能夠變更作業的擁有者。  
  
    將作業指派給另一個登入並不保證新的擁有者具有充分之使用權限能夠成功執行作業。  
  
## <a name="TsqlProc2"></a>使用 Transact-SQL  
**若要賦予作業擁有權給其他人**  
  
1.  在 [物件總管] 中，連接到 Database Engine 的執行個體，然後展開該執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]**。  
  
3.  在查詢視窗中，輸入下列使用 [sp_manage_jobs_by_login (Transact-SQL)](http://msdn.microsoft.com/en-us/832ec15a-6e92-4eb5-8c4a-af4dba79fbaa) 系統預存程序的陳述式。 下列範例會將 `danw` 的所有作業重新指派給 `françoisa`。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
## <a name="SMOProc2"></a>使用 SQL Server 管理物件  
**若要賦予作業擁有權給其他人**  
  
1.  使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 **Job** 類別。 如需範例程式碼，請參閱 [使用 SQL Server Agent 排程自動管理工作](http://msdn.microsoft.com/en-us/900242ad-d6a2-48e9-8a1b-f0eea4413c16)。  
  
## <a name="see-also"></a>另請參閱  
[實作作業](../../ssms/agent/implement-jobs.md)  
[建立作業](../../ssms/agent/create-jobs.md)  
  
