---
title: 建立操作員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 27f99081b3af76448732ae887fb6f6059628fd4a
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553052"
---
# <a name="create-an-operator"></a>建立操作員
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定使用者，以接收 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業的通知。  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   請注意，必須設定 SQL Server Agent 使用 Database Mail，才能將電子郵件及呼叫器通知傳送給操作員。 如需詳細資訊，請參閱＜ [指派警示給操作員](assign-alerts-to-an-operator.md)＞。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才可以建立操作員。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>若要建立操作員  
  
1.  在 **[物件總管]** 中，按一下加號展開要建立 SQL Server Agent 操作員的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  以滑鼠右鍵按一下 [操作員]  資料夾，然後選取 [新增操作員]  。  
  
    下列選項可從 **[新增操作員]** 對話方塊的 **[一般]** 頁面取得：  
  
    **名稱**  
    變更操作員的名稱。  
  
    **已啟用**  
    啟用操作員。 未啟用時，不會傳送通知給操作員。  
  
    **電子郵件名稱**  
    指定操作員的電子郵件地址。  
  
    **Net Send 位址**  
    指定用於 **net send**的位址。  
  
    **呼叫器電子郵件名稱**  
    指定操作員呼叫器所用的電子郵件地址。  
  
    **傳呼待命排程**  
    設定呼叫器使用中的時間。  
  
    **星期一至星期日**  
    選取呼叫器使用中的日子。  
  
    **工作日開始**  
    選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就會傳送訊息給呼叫器。  
  
    **工作日結束**  
    選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就不再傳送訊息給呼叫器。  
  
    下列選項可從 **[新增操作員]** 對話方塊的 **[通知]** 頁面取得：  
  
    **警示**  
    檢視執行個體中的警示。  
  
    **作業**  
    檢視執行個體中的作業。  
  
    **警示清單**  
    列出執行個體中的警示。  
  
    **作業清單**  
    列出執行個體中的作業。  
  
    **電子郵件**  
    使用電子郵件通知此操作員。  
  
    **呼叫器**  
    將電子郵件傳送至呼叫器位址，來通知此操作員。  
  
    **Net send**  
    使用 **net send**通知此操作員。  
  
4.  完成建立新的操作員後，請按一下 **[確定]** 。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-operator"></a>若要建立操作員  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- sets up the operator information for user 'danwi.'
    -- The operator is enabled.   
    -- SQL Server Agent sends notifications by pager 
    -- from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_operator (Transact-SQL)](https://msdn.microsoft.com/817cd98a-4dff-4ed8-a546-f336c144d1e0)。  
  
