---
title: 指派警示給操作員 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3cc238b952c03595035856f377b6fdbb9eaf5e2c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048795"
---
# <a name="assign-alerts-to-an-operator"></a>指派警示給操作員
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，將 Agent 警示指派給操作員，使其可以接收有關中作業的通知 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目指派警示給操作員：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統。 建議您利用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來設定您的警示基礎結構。  
  
-   若要傳送通知來回應警示，您必須先設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來傳送郵件。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
-   如果傳送電子郵件訊息或呼叫器通知發生失敗，此失敗會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務錯誤記錄檔中報告。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠指派警示給操作員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-assign-alerts-to-an-operator"></a>若要指派警示給操作員  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含您要指派警示的操作員。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[操作員]** 資料夾。  
  
4.  以滑鼠右鍵按一下要指派警示的操作員並選取 [屬性]****，然後選取 [通知]**** 頁面。  
  
5.  在 [ _operator_name_**屬性**] 對話方塊的 [**選取頁面**] 底下，選取 [**通知**]。  
  
6.  在 **[檢視傳送給這名使用者的通知來源]** 下選取 **[警示]** ，以檢視傳送給這名操作員的警示清單；或選取 **[作業]** ，以檢視會傳送通知給這名操作員的作業清單。 選取下列一個或多個核取方塊，視需要定義每個通知的通知方法：[電子郵件]****、[呼叫器]**** 或 [Net send]****。  
  
7.  完成時按一下 **[確定]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-assign-alerts-to-an-operator"></a>若要指派警示給操作員  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'Fran??ois Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_notification &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)。  
  
  
