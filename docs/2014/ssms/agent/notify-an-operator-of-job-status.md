---
title: 通知操作員作業狀態 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7762daa362b73f981603f7d32a41b8084327e1f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185318"
---
# <a name="notify-an-operator-of-job-status"></a>通知操作員作業狀態
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]中設定通知選項，以便讓 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 將與作業有關的通知傳送給操作員。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目通知操作員作業狀態：**  
  
     [Transact-SQL](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理物件](#SMO)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>若要通知操作員作業狀態  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體，然後展開該執行個體。  
  
2.  依序展開 [SQL Server Agent] 和 [作業]、以滑鼠右鍵按一下要編輯的作業，然後選取 [屬性]。  
  
3.  在 **[作業屬性]** 對話方塊中，選取 **[通知]** 頁面。  
  
4.  如果您想以電子郵件通知操作員，請核取 [電子郵件]、從清單選取操作員，然後選取下列其中一個選項：  
  
    -   **[當作業成功時]** 即可在作業順利完成時，通知操作員。  
  
    -   **[當作業失敗時]** 會在作業未順利完成時通知操作員。  
  
    -   **[作業完成時]** 可在無論完成狀態為何，都通知操作員。  
  
5.  如果您想以呼叫器來通知操作員，請核取 **[呼叫器]**、從清單選取操作員，然後選取下列其中一個選項：  
  
    -   **[當作業成功時]** 即可在作業順利完成時，通知操作員。  
  
    -   **[當作業失敗時]** 會在作業未順利完成時通知操作員。  
  
    -   **[作業完成時]** 可在無論完成狀態為何，都通知操作員。  
  
6.  如果您想以網路傳送的方式來通知操作員，請核取 **[網路傳送]**、從清單選取操作員，然後選取下列其中一個選項：  
  
    -   **[當作業成功時]** 即可在作業順利完成時，通知操作員。  
  
    -   **[當作業失敗時]** 會在作業未順利完成時通知操作員。  
  
    -   **[作業完成時]** 可在無論完成狀態為何，都通知操作員。  
  
##  <a name="TSQL"></a> 使用 Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>若要通知操作員作業狀態  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_add_notification &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)。  
  
##  <a name="SMO"></a> 使用 SQL Server 管理物件  
 **若要通知操作員作業狀態**  
  
 使用`Job`藉由使用您選擇，例如 Visual Basic、 Visual C# 或 PowerShell 的程式語言的類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
  
