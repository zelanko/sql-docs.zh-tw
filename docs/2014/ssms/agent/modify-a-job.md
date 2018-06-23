---
title: 修改作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: caceadb3d1cc35bc9adb7a1ac97d03dadad76934
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145079"
---
# <a name="modify-a-job"></a>Modify a Job
  此主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中變更 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] Agent 作業的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**   
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目修改作業：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 主要作業無法同時存在於本機和遠端伺服器內。  
  
###  <a name="Security"></a> 安全性  
 除非您是系統管理員 ( **sysadmin** ) 固定伺服器角色的成員，否則您只能修改您所擁有的作業。 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>若要修改作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 [SQL Server Agent]，展開 [作業]，以滑鼠右鍵按一下要修改的作業，然後按一下 [屬性]。  
  
3.  在 **[作業屬性]** 對話方塊中，利用相對應的頁面更新作業的屬性、步驟、排程、警示及通知。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-modify-a-job"></a>若要修改作業  
  
1.  在 [物件總管] 中，連接到 Database Engine 的執行個體，然後展開該執行個體。  
  
2.  在工具列上，按一下 **[新增查詢]**。  
  
3.  在查詢視窗中，使用下列系統預存程序修改作業。  
  
    -   執行[sp_update_job &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)變更作業的屬性。  
  
    -   執行[sp_update_schedule &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql)變更作業定義的排程詳細資料。  
  
    -   執行[sp_add_jobstep &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)要加入新的作業步驟。  
  
    -   執行[sp_update_jobstep &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)變更預先存在的作業步驟。  
  
    -   執行[sp_delete_jobstep &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)若要從作業中移除的作業步驟。  
  
    -   修改任何 SQL Server Agent 主要作業的其他預存程序：  
  
        -   執行[sp_delete_jobserver &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql)刪除目前與作業相關聯的伺服器。  
  
        -   執行[sp_add_jobserver &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)要伺服器關聯到目前的工作。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要修改作業**  
  
 使用`Job`使用您選擇，例如 Visual Basic、 Visual C# 或 PowerShell 的程式語言的類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
