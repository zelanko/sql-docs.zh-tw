---
title: 檢視作業記錄 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe2287c5dca70fb78371e3f23dd199013c81c611
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208388"
---
# <a name="view-the-job-history"></a>檢視作業記錄
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中檢視 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業記錄。  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目檢視作業記錄：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-job-history-log"></a>若要檢視作業記錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，然後展開 **[作業]**。  
  
3.  以滑鼠右鍵按一下作業，然後按一下 **[檢視記錄]**。  
  
4.  在 [記錄檔檢視器] 中檢視作業記錄。  
  
5.  若要更新作業記錄，請按一下 **[重新整理]**。 若要檢視較少的資料列，請按一下 **[篩選]** 按鈕，並輸入篩選參數。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-job-history-log"></a>若要檢視作業記錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_help_jobhistory &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要檢視作業記錄**  
  
 使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 `EnumHistory` 類別的 `Job` 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
