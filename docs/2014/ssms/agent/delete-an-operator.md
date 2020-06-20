---
title: 刪除操作員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- canceling operators
- removing operators
- deleting operators
- dropping operators
- jobs [SQL Server Agent], operators
- operators (users) [Database Engine], deleting with Management Studio
ms.assetid: 2b7b8627-082d-4189-8584-abd3a9b604cf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 75bea1c5c5fabff7ce55fe07a5181baa8f99e0fe
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056611"
---
# <a name="delete-an-operator"></a>刪除操作員
  本主題描述如何使用或，在中移除操作員，使其不會再收到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 警示通知 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目刪除操作員：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 當移除操作員時，也會移除操作員的所有相關通知。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 **系統管理員 (sysadmin)** 固定伺服器角色的成員可以刪除操作員。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-an-operator"></a>若要刪除操作員  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含要刪除之操作員的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[操作員]** 資料夾。  
  
4.  以滑鼠右鍵按一下您要刪除的操作員，然後選取 [刪除]****。  
  
5.  在 **[刪除物件]** 對話方塊中，確定已選取正確的操作員，然後按一下 **[確定]**。 如果希望另一個操作員可以收到會傳送給已刪除操作員的警示與作業，請核取 **[重新指派給]** ，然後在清單中選取操作員。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-an-operator"></a>若要刪除操作員  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- deletes operator 'Test Operator' and reassigns all alerts and jobs sent to that operator to 'Fran??ois Ajenstat'  
    USE msdb ;  
    GO  
  
    EXEC sp_delete_operator @name = 'Test Operator',  
        @reassign_to_operator = 'Fran??ois Ajenstat';  
    GO  
    ```  
  
 如需詳細資訊，請參閱[sp_delete_operator &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-operator-transact-sql)。  
  
  
