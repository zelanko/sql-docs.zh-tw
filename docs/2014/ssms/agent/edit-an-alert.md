---
title: 編輯警示 | Microsoft Docs
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
- alerts [SQL Server], modifying
- modifying alerts
ms.assetid: f518e528-cc8f-446a-b37d-98505b86e430
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: acc1472501d21be27ffa8e71190a79961e8eb824
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808834"
---
# <a name="edit-an-alert"></a>Edit an Alert
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中編輯 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目編輯警示：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 依預設， **系統管理員 (sysadmin)** 固定伺服器角色的成員可以編輯警示中的資訊。 其他使用者必須被授與 **msdb** 資料庫的 **SQLAgentOperatorRole** 固定資料庫角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-edit-an-alert"></a>若要編輯警示  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含要編輯之警示的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[警示]** 資料夾。  
  
4.  以滑鼠右鍵按一下要編輯的警示，並且選取 [屬性]。  
  
5.  更新 **[一般]**、 **[回應]** 和 **[選項]** 頁面上的警示屬性。  
  
6.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-edit-an-alert"></a>若要編輯警示  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- changes the enabled setting of Test Alert to 0  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_alert  
        @name = N'Test Alert',  
        @enabled = 0 ;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 < [sp_update_alert &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)。  
  
  
