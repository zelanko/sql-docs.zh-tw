---
title: 使用錯誤號碼來建立警示 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- alerts [SQL Server], error numbers
ms.assetid: 03dd7fac-5073-4f86-babd-37e45a86023c
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 453c8e5a2361e93580b7cdd737f03d357946df89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090145"
---
# <a name="create-an-alert-using-an-error-number"></a>使用錯誤號碼建立警示
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中建立 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示，當發生指定號碼的錯誤時會引發警示。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [安全性](#Security)  
  
-   **若要使用下列項目，使用錯誤號碼建立警示：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統，建議您利用這個方式來設定警示基礎結構。  
  
-   **xp_logevent** 產生的事件出現在 master 資料庫中。 因此，除非警示的 **xp_logevent** 是 **@database_name** 或 NULL，否則， **xp_logevent** 不會觸發警示。  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠執行 **sp_add_alert**。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-an-error-number"></a>若要使用錯誤號碼建立警示  
  
1.  在 **[物件總管]** 中，按一下加號，以展開您要使用錯誤號碼建立警示的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  以滑鼠右鍵按一下 **[警示]** ，然後選取 **[新增警示]** 。  
  
4.  在 **[新增警示]** 對話方塊中的 **[名稱]** 方塊，輸入此警示的名稱。  
  
5.  選取 **[啟用]** 核取方塊以讓警示得以執行。 根據預設，會選取 **[啟用]** 。  
  
6.  在 **[類型]** 清單中，選取 **[SQL Server 事件警示]** 。  
  
7.  在 **[事件警示定義]** 下，從 **[資料庫名稱]** 清單中選取資料庫，將警示限制在特定資料庫。  
  
8.  在 **[將根據下列條件引發警示]** 下，按一下 **[錯誤號碼]** ，然後為警示輸入有效的錯誤號碼。 或者，按一下 **[嚴重性]** ，然後選取將會引發警示的特定嚴重性。  
  
9. 核取對應到 **[訊息包含下列內容時引發警示]** 核取方塊，將警示限制在特定字元順序，然後在 **[訊息文字]** 中輸入關鍵字或字元字串。 最大字元數為 100。  
  
10. 按一下 [確定]  。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
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
  
