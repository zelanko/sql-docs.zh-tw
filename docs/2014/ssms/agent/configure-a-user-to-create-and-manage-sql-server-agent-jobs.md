---
title: 設定使用者可建立及管理 SQL Server Agent 作業 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a62f6c2e1ef86a6fcd5e532b2ef413d8142698e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63253554"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>設定使用者可建立及管理 SQL Server Agent 作業
  本主題描述如何設定使用者，以建立或執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
-   **開始之前：**[安全性](#Security)  
  
-   **若要設定使用者建立和管理 SQL Server Agent 作業，使用：**[SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 若要設定使用者，以建立或執行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，您必須先將現有的 SQL Server 登入或 msdb 角色加入下列其中一項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 固定資料庫角色中的 msdb 資料庫：SQLAgentUserRole、 SQLAgentReaderRole 或 SQLAgentOperatorRole。  
  
 根據預設，這些資料庫角色的成員可以在以其身分執行的自有作業步驟。 如果這些非管理使用者想要執行作業來執行其他作業步驟類型 (例如， [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝)，則他們需要有 Proxy 帳戶的存取權。 系統管理員 (sysadmin) 固定伺服器角色的所有成員都擁有建立、修改和刪除 Proxy 帳戶的權限。 如需有關與這些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色關聯之權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)。  
  
####  <a name="Permissions"></a> 權限  
 如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)＞。  
  
##  <a name="SSMS"></a> 使用 SQL Server Management Studio  
 **若要將 SQL 登入或 msdb 角色加入 SQL Server Agent 固定資料庫角色中**  
  
1.  在 **[物件總管]** 中展開伺服器。  
  
2.  展開 **[安全性]**，再展開 **[登入]**。  
  
3.  以滑鼠右鍵按一下您要新增至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的登入，然後選取 [屬性]。  
  
4.  在上**使用者對應**頁**登入屬性**對話方塊方塊中，選取 資料列包含`msdb`。  
  
5.  在 **[資料庫角色成員資格對象: msdb]** 底下，核取適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色。  
  
 **若要設定 Proxy 帳戶來建立及管理 SQL Server Agent 作業步驟**  
  
1.  在 **[物件總管]** 中展開伺服器。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [Proxy]，然後選取 [新增 Proxy]。  
  
4.  在 **[新 Proxy 帳戶]** 對話方塊的 **[一般]** 頁面上，指定新 Proxy 的 Proxy 名稱、認證名稱及描述。 請注意，在建立 SQL Server Agent Proxy 之前，您必須先建立認證。 如需建立認證的詳細資訊，請參閱[建立認證](../../relational-databases/security/authentication-access/create-a-credential.md)並[CREATE CREDENTIAL &#40;-&#41;](/sql/t-sql/statements/create-credential-transact-sql)。  
  
5.  檢查這個 Proxy 適當的子系統。  
  
6.  在 **[主體]** 頁面上，加入或移除登入或角色，藉此授與或移除 Proxy 帳戶的存取。  
  
## <a name="see-also"></a>另請參閱  
 [實作 SQL Server Agent 安全性](implement-sql-server-agent-security.md)  
  
  
