---
title: "建立操作員 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: afca596bc8dc55411bcfbd48b74d3bdfd7c11248
ms.lasthandoff: 04/11/2017

---
# <a name="create-an-operator"></a>建立操作員
此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 或 [!INCLUDE[tsql](../../includes/tsql_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中設定使用者，以接收 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 作業的通知。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目建立操作員：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   呼叫器和 **net send** 選項會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 未來版本的 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   請注意，必須設定 SQL Server Agent 使用 Database Mail，才能將電子郵件及呼叫器通知傳送給操作員。 如需詳細資訊，請參閱＜ [指派警示給操作員](http://msdn.microsoft.com/library/ms190038.aspx)＞。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才可以建立操作員。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-create-an-operator"></a>若要建立操作員  
  
1.  在 **[物件總管]**中，按一下加號展開要建立 SQL Server Agent 操作員的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [操作員]**** 資料夾，然後選取 [新增操作員]****。  
  
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
    選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 就會傳送訊息給呼叫器。  
  
    **工作日結束**  
    選取時間，在該時間之後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 就不再傳送訊息給呼叫器。  
  
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
  
    **Net Send**  
    使用 **net send**通知此操作員。  
  
4.  完成建立新的操作員後，請按一下 **[確定]**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-create-an-operator"></a>若要建立操作員  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] ****。  
  
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
  
如需詳細資訊，請參閱 [sp_add_operator (Transact-SQL)](http://msdn.microsoft.com/en-us/817cd98a-4dff-4ed8-a546-f336c144d1e0)。  
  

