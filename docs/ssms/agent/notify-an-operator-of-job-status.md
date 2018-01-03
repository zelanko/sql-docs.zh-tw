---
title: "通知操作員作業狀態 | Microsoft Docs"
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
- status information [SQL Server], jobs
- jobs [SQL Server Agent], notification options
- SQL Server Agent jobs, status
- jobs [SQL Server Agent], status
- SQL Server Agent jobs, notification options
- notifications [SQL Server], job status
ms.assetid: e7399505-27ac-48d9-a637-73bf92b9df49
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6b2e18889789f8849546295fbce2b5961c003935
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="notify-an-operator-of-job-status"></a>Notify an Operator of Job Status
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)] 或 SQL Server 管理物件，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中設定通知選項，以便讓 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 將與作業有關的通知傳送給操作員。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要使用下列項目通知操作員作業狀態：**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理物件](#SMO)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
如需詳細資訊，請參閱＜ [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
  
#### <a name="to-notify-an-operator-of-job-status"></a>若要通知操作員作業狀態  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
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
  
## <a name="TSQL"></a>使用 Transact-SQL  
  
#### <a name="to-notify-an-operator-of-job-status"></a>若要通知操作員作業狀態  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] 。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert).  
    -- This example assumes that Test Alert already exists
    --  and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_notification   
    @alert_name = N'Test Alert',   
    @operator_name = N'François Ajenstat',   
    @notification_method = 1 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_notification (Transact-SQL)](http://msdn.microsoft.com/en-us/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)。  
  
## <a name="SMO"></a>使用 SQL Server 管理物件  
**若要通知操作員作業狀態**  
  
透過所選的程式語言，例如 Visual Basic、Visual C# 或 PowerShell，使用 **Job** 類別。 如需詳細資訊，請參閱 [SQL Server 管理物件 (SMO)](http://msdn.microsoft.com/library/ms162169.aspx)。  
  
