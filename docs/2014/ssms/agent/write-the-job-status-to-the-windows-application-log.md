---
title: 將作業狀態寫入到 Windows 應用程式記錄 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 13a3c6301de03461f709806e80fabefbd2e53d1d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814454"
---
# <a name="write-the-job-status-to-the-windows-application-log"></a>將作業狀態寫入到 Windows 應用程式記錄
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，將作業狀態寫入 Windows 應用程式事件記錄檔。  
  
 作業回應可確保資料庫管理員知道作業已完成，以及作業的執行頻率。 典型的作業回應包括：  
  
-   使用電子郵件、電子呼叫或 **net send** 訊息通知操作員。 如果操作員必須執行後續動作，請使用其中一個作業回應。 例如，如果備份作業成功完成，必須告知操作員以取下備份磁帶，並將其存放在安全的地方。  
  
-   將事件訊息寫入至 Windows 應用程式記錄。 這個回應只用於失敗的作業。  
  
-   自動刪除作業。 如果確定您將不再需要重新執行這個作業，請使用這個作業回應。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目，將作業狀態寫入 Windows 應用程式記錄檔：**  
  
     [Transact-SQL](#SSMS)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>若要將作業狀態寫入到 Windows 應用程式記錄  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  展開 **[SQL Server Agent]**，展開 **[作業]**，以滑鼠右鍵按一下要編輯的作業，然後按一下 **[屬性]**。  
  
3.  選取 **[通知]** 頁面。  
  
4.  勾選 **[寫入 Windows 應用程式事件記錄檔]**，並選擇下列其中一項：  
  
    -   按一下 [當作業成功時]，在作業成功完成時記錄作業狀態。  
  
    -   按一下 [當作業失敗時]，在作業失敗時記錄作業狀態。  
  
    -   按一下 [作業完成時]，不論完成狀態為何，一律記錄作業狀態。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要將作業狀態寫入到 Windows 應用程式記錄**  
  
 使用所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，呼叫 `EventLogLevel` 類別的 `Job` 屬性。  
  
 下列程式碼範例會設定作業在作業執行完成時，產生作業系統事件記錄項目。  
  
 **PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
  
