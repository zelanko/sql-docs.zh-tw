---
title: 使用嚴重性層級來建立警示 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e6cfd404c08f47fd1724eeac2793ba00c63befa9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032698"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，建立一種在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中發生某特定嚴重性層級事件時，所引發的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要用嚴重性層級建立警示，您可使用下列項目：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統，建議您利用這個方式來設定警示基礎結構。  
  
-   **xp_logevent** 產生的事件出現在 master 資料庫中。 因此，除非警示的 **xp_logevent** 是 **@database_name** 或 NULL，否則， **xp_logevent** 不會觸發警示。  
  
-   從 19 到 25 的嚴重性層級會傳送 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訊息到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 應用程式記錄檔並觸發警示。 嚴重性層級小於 19 的事件，只有在使用 **sp_altermessage**、RAISERROR WITH LOG 或 **xp_logevent** 強制寫入 Windows 應用程式記錄檔時，才會觸發警示。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_add_alert**。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>若要使用嚴重性層級建立警示  
  
1.  在 **[物件總管]** 中，按一下加號，以展開您要使用嚴重性層級建立警示的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 **[警示]** ，然後選取 **[新增警示]**。  
  
4.  在 **[新增警示]** 對話方塊中的 **[名稱]** 方塊，輸入此警示的名稱。  
  
5.  在 **[類型]** 清單中，選取 **[SQL Server 事件警示]**。  
  
6.  在 **[事件警示定義]** 下，從 **[資料庫名稱]** 清單中選取資料庫，將警示限制在特定資料庫。  
  
7.  在 **[將根據下列條件引發警示]** 下，按一下 **[嚴重性]** ，然後選取將會引發警示的特定嚴重性。  
  
8.  核取對應到 **[訊息包含下列內容時引發警示]** 核取方塊，將警示限制在特定字元順序，然後在 **[訊息文字]** 中輸入關鍵字或字元字串。 最大字元數為 100。  
  
9. 按一下 [確定] 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>若要使用嚴重性層級建立警示  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)。  
  
  
