---
title: 定義對警示的回應 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], responding to
- responding to alerts
ms.assetid: c86ca6eb-c59f-46e9-bc32-d474e7c3b170
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ac3e9ee443f0c10a39128fc1d6aab6813ec4f4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62524068"
---
# <a name="define-the-response-to-an-alert-sql-server-management-studio"></a>定義對警示的回應 (SQL Server Management Studio)
  本主題描述如何[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../includes/tsql-md.md)]，在中定義回應 Agent 警示的方式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列內容定義對警示的回應：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   在未來版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中，將會從 Agent 移除 [呼機] 和 [ **net send** ] 選項。 請避免在新的開發工作中使用這些功能，並規劃修改目前使用這些功能的應用程式。  
  
-   請注意，必須設定 SQL Server Agent 使用 Database Mail，才能將電子郵件及呼叫器通知傳送給操作員。 如需詳細資訊，請參閱＜ [指派警示給操作員](assign-alerts-to-an-operator.md)＞。  
  
-   
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供了一種簡單的圖形方式供您管理各項作業，建議您利用這個方式來建立和管理作業基礎結構。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠定義對警示的回應。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-the-response-to-an-alert"></a>若要定義對警示的回應  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含您要定義回應的警示。  
  
2.  按一下加號展開 **[SQL Server Agent]** 。  
  
3.  按一下加號展開 **[警示]** 資料夾。  
  
4.  在要定義回應的警示上按一下滑鼠右鍵，然後選取 [屬性]****。  
  
5.  在 [ _alert_name_**警示屬性**] 對話方塊的 [**選取頁面**] 底下，選取 [**回應**]。  
  
6.  選取 **[執行作業]** 核取方塊，然後從 **[執行作業]** 核取方塊底下的清單中選取發生警示時要執行的作業。 您可以按一下 **[新增作業]** 來建立新作業。 您可以按一下 **[檢視作業]** 檢視作業的詳細資訊。 如需 [**新增作業**] 和 [**作業屬性**]_job_name_ ] 對話方塊中可用選項的詳細資訊，請參閱[建立作業](create-a-job.md)和[查看作業](view-a-job.md)。  
  
7.  如果您要在啟動警示時通知操作員，請選取 **[通知操作員]** 核取方塊。 在**運算子清單**中，選取下列一或多種方法通知操作員：[電子郵件]****、[呼叫器]**** 或 [Net Send]****。 您可以按一下 **[新增操作員]** 來建立新操作員。 您可以按一下 **[檢視操作員]** 檢視操作員的詳細資訊。 如需有關 **[新增操作員]** 和 **[檢視操作員屬性]** 對話方塊中之可用選項的詳細資訊，請參閱＜ [Create an Operator](create-an-operator.md) ＞和＜ [View Information About an Operator](view-information-about-an-operator.md)＞。  
  
8.  完成後，請按一下 **[確定]** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-define-the-response-to-an-alert"></a>若要定義對警示的回應  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- adds an e-mail notification for Test Alert.  
    -- assumes that Test Alert already exists and that Fran??ois Ajenstat is a valid operator name   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'Fran??ois Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_add_notification &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)。  
  
  
