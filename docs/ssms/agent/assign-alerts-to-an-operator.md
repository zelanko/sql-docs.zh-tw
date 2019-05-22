---
title: 指派警示給操作員 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b889b3c391bde7e064eab49c3791fa05cdf1e674
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65104403"
---
# <a name="assign-alerts-to-an-operator"></a>指派警示給操作員
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中將 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示指派給操作員，讓操作員可以接收與作業相關的通知。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [安全性](#Security)  
  
-   **若要使用下列項目指派警示給操作員：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理整個警示系統。 建議您利用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 來設定您的警示基礎結構。  
  
-   若要傳送通知來回應警示，您必須先設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來傳送郵件。 如需詳細資訊，請參閱 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)。  
  
-   如果傳送電子郵件訊息或呼叫器通知發生失敗，此失敗會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務錯誤記錄檔中報告。  
  
### <a name="Security"></a>安全性  
  
#### <a name="Permissions"></a>Permissions  
只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠指派警示給操作員。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-assign-alerts-to-an-operator"></a>若要指派警示給操作員  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含您要指派警示的操作員。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[操作員]** 資料夾。  
  
4.  以滑鼠右鍵按一下要指派警示的操作員並選取 [屬性]，然後選取 [通知] 頁面。  
  
5.  在 [_operator\_name_ 屬性] 對話方塊中，選取 [選取頁面] 下的 [通知]。  
  
6.  在 **[檢視傳送給這名使用者的通知來源]** 下選取 **[警示]** ，以檢視傳送給這名操作員的警示清單；或選取 **[作業]** ，以檢視會傳送通知給這名操作員的作業清單。 選取下列一或多個核取方塊，視需要定義每個通知的通知方法：[電子郵件]、[呼叫器]，或 [Net send]。  
  
7.  完成後，請按一下 **[確定]**。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-assign-alerts-to-an-operator"></a>若要指派警示給操作員  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 [執行] 。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)。  
  
