---
title: 檢視有關警示的資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- viewing alerts
- alerts [SQL Server], viewing
- displaying alerts
- status information [SQL Server], alerts
ms.assetid: a0e3a8c4-e3c2-42a5-b2f8-aa06061d3fa6
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee72512a507299e71f13fee689709a9403bb04e4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058661"
---
# <a name="view-information-about-an-alert"></a>檢視有關警示的資訊
  本主題描述如何 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用或，在中查看 Agent 警示的相關資訊 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視有關警示的資訊：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 依預設， **系統管理員 (sysadmin)** 固定伺服器角色的成員可以檢視警示的相關資訊。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-information-about-an-alert"></a>若要檢視有關警示的資訊  
  
1.  在 **[物件總管]** 中，按一下加號，展開要檢視警示相關資訊的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[警示]** 資料夾。  
  
4.  以滑鼠右鍵按一下您想要檢視其資訊的警示，然後選取 [屬性]****。  
  
     如需 [<警示名稱> 警示屬性]__**** 對話方塊中之可用選項的詳細資訊，請參閱：  
  
    -   [警示屬性-新增警示 &#40;一般頁面&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
    -   [警示屬性-新增警示 &#40;回應頁面&#41;](alert-properties-new-alert-response-page.md)  
  
    -   [警示屬性：新增警示 &#40;選項頁面&#41;](alert-properties-new-alert-options-page.md)  
  
    -   [警示屬性 &#40;記錄頁面&#41;](alert-properties-history-page.md)  
  
5.  完成時按一下 **[確定]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-information-about-an-alert"></a>若要檢視有關警示的資訊  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- reports information about the Demo: Sev. 25 Errors alert  
    -- This example assumes that the 'Demo: Sev. 25 Errors' alert exists.  
    USE msdb ;  
    GO  
  
    EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors'  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_help_alert &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-alert-transact-sql)。  
  
  
