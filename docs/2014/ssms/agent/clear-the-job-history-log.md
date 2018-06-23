---
title: 清除作業記錄檔 | Microsoft Docs
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
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 813f4090b95266f924f7c17bd359658136f0012f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023267"
---
# <a name="clear-the-job-history-log"></a>清除作業記錄檔
  此主題描述如何使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中刪除 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] or SQL Server Management Objects.  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目清除作業記錄：**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-clear-the-job-history-log"></a>若要清除作業記錄檔  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，然後展開 **[作業]**。  
  
3.  以滑鼠右鍵按一下某個作業，然後按一下 **[檢視記錄]**。  
  
4.  在 **[記錄檔檢視器]** 中，選取您要清除其記錄的作業，然後執行下列其中一項：  
  
    -   按一下 **[刪除]**，然後按一下 **[刪除記錄]** 對話方塊中的 **[刪除所有的記錄]** 。 您可以刪除所有的作業記錄，也可以只刪除某個特定日期之前的記錄。 如果您要移除所有的作業記錄，請按一下 **[刪除所有的記錄]**。 如果您只要移除舊的作業記錄，請按一下 **[刪除在這之前的記錄]**，然後指定日期。  
  
    -   如果您要清除多重伺服器作業的記錄，請按一下 **[作業狀態]** 。 按一下 **[作業]**，按一下作業名稱，然後按一下 **[檢視遠端作業記錄]**。  
  
5.  按一下 **[刪除]**。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-clear-the-job-history-log"></a>若要清除作業記錄檔  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要清除作業記錄檔**  
  
 透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 `PurgeJobHistory` 類別的 `JobServer` 方法。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  