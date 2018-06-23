---
title: 刪除一個或多個作業 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 98721e58322867b942703fc245115b497ad79c34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131852"
---
# <a name="delete-one-or-more-jobs"></a>刪除一個或多個作業
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中刪除 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
 
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 除非您是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，否則您只能刪除您擁有的作業步驟。  
  
 
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>若要刪除作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，展開 **[作業]**，以滑鼠右鍵按一下要刪除的作業，然後按一下 **[刪除]**。  
  
3.  在 **[刪除物件]** 對話方塊中，確認已選取您要刪除的作業。  
  
4.  按一下 [確定] 。  
  
#### <a name="to-delete-multiple-jobs"></a>若要刪除多個作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 **[作業活動監視器]**，然後按一下 **[檢視作業活動]**。  
  
4.  在「作業活動監視器」中，選取要刪除的作業，以滑鼠右鍵按一下選取範圍，然後選擇 **[刪除作業]**。  
  

  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-job"></a>若要刪除作業  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_delete_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql)。  
  

  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要刪除多個作業**  
  
 使用`JobCollection`使用您選擇，例如 Visual Basic、 Visual C# 或 PowerShell 的程式語言的類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  

  
  
