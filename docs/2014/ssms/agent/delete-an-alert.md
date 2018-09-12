---
title: 刪除警示 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], deleting
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- removing alerts
ms.assetid: c982b208-e2d1-4d34-8cee-940b9baf6586
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37634ece2e7263cc80793935b8f37ee09dc49a35
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818144"
---
# <a name="delete-an-alert"></a>Delete an Alert
  本主題說明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目刪除警示：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 移除警示也會移除警示的任何相關通知。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 依預設，只有 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能夠刪除警示。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-an-alert"></a>若要刪除警示  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要刪除的 SQL Server Agent 警示。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[警示]** 資料夾。  
  
4.  在您要刪除的警示上按一下滑鼠右鍵，然後選取 [刪除]。  
  
5.  在 **[刪除物件]** 對話方塊中，確認已選取正確的警示，然後按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-alert"></a>若要刪除警示  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- deletes the SQL Server Agent alert called 'Test Alert.'  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_alert  
       @name = N'Test Alert' ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 s[sp_delete_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-alert-transact-sql)。  
  
  
