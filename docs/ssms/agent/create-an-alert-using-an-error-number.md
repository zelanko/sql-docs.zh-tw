---
description: 使用錯誤號碼建立警示
title: 使用錯誤號碼建立警示
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 704cf323bef3a94ba3c73fd3c899b93b7732e1b0
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784985"
---
# <a name="create-an-alert-using-an-error-number"></a>使用錯誤號碼建立警示
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](https://docs.microsoft.com/azure/azure-sql/managed-instance/sql-managed-instance-paas-overview)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱[來自 SQL Server 的 Azure SQL 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) \(部分機器翻譯\)。

本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，以在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示，其會在發生指定號碼的錯誤時引發警示。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統，建議您利用這個方式來設定警示基礎結構。  
  
-   **xp_logevent** 產生的事件出現在 master 資料庫中。 因此，除非警示的 **\@database_name** 是 **'master'** 或 NULL，否則，**xp_logevent** 不會觸發警示。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_add_alert**。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>若要使用錯誤號碼建立警示  
  
1.  在 **[物件總管]** 中，按一下加號，以展開您要使用錯誤號碼建立警示的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 **[警示]** ，然後選取 **[新增警示]**。  
  
4.  在 **[新增警示]** 對話方塊中的 **[名稱]** 方塊，輸入此警示的名稱。  
  
5.  選取 **[啟用]** 核取方塊以讓警示得以執行。 根據預設，會選取 **[啟用]** 。  
  
6.  在 **[類型]** 清單中，選取 **[SQL Server 事件警示]**。  
  
7.  在 **[事件警示定義]** 下，從 **[資料庫名稱]** 清單中選取資料庫，將警示限制在特定資料庫。  
  
8.  在 **[將根據下列條件引發警示]** 下，按一下 **[錯誤號碼]**，然後為警示輸入有效的錯誤號碼。 或者，按一下 **[嚴重性]** ，然後選取將會引發警示的特定嚴重性。  
  
9. 核取對應到 **[訊息包含下列內容時引發警示]** 核取方塊，將警示限制在特定字元順序，然後在 **[訊息文字]** 中輸入關鍵字或字元字串。 最大字元數為 100。  
  
10. 按一下 [確定]。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>若要使用錯誤號碼建立警示  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up
    -- the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up
    -- the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The DB will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)。  
  
