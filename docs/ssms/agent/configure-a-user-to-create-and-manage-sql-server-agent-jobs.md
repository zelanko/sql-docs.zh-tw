---
title: 設定使用者可建立及管理 SQL Server Agent 作業 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1f161c586f190edc73ad538b2a0b9da4bc9d9421
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105852"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何設定使用者，以建立或執行 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業。  
  
-   **開始之前：**[安全性](#Security)  
  
-   **設定使用者以建立及管理 SQL Server Agent 作業，使用：**[SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>安全性  
若要設定使用者以建立或執行 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 作業，您必須先將現有 SQL Server 登入或 msdb 角色新增到 msdb 資料庫中的下列其中一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色：SQLAgentUserRole、SQLAgentReaderRole 或 SQLAgentOperatorRole。  
  
根據預設，這些資料庫角色的成員可以在以其身分執行的自有作業步驟。 如果這些非管理使用者想要執行作業來執行其他作業步驟類型 (例如， [!INCLUDE[ssIS](../../includes/ssis_md.md)] 封裝)，則他們需要有 Proxy 帳戶的存取權。 系統管理員 (sysadmin) 固定伺服器角色的所有成員都擁有建立、修改和刪除 Proxy 帳戶的權限。 如需有關與這些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色關聯之權限的詳細資訊，請參閱 [SQL Server Agent 固定資料庫角色](../../ssms/agent/sql-server-agent-fixed-database-roles.md)。  
  
#### <a name="Permissions"></a>Permissions  
如需詳細資訊，請參閱＜ [實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)＞。  
  
## <a name="SSMS"></a>使用 SQL Server Management Studio  
**若要將 SQL 登入或 msdb 角色加入 SQL Server Agent 固定資料庫角色中**  
  
1.  在 **[物件總管]** 中展開伺服器。  
  
2.  展開 **[安全性]**，再展開 **[登入]**。  
  
3.  以滑鼠右鍵按一下您要新增至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色的登入，然後選取 [屬性]。  
  
4.  在 **[登入屬性]** 對話方塊的 **[使用者對應]** 頁面上，選取包含 **msdb**的資料列。  
  
5.  在 **[資料庫角色成員資格對象: msdb]** 底下，核取適當的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 固定資料庫角色。  
  
**若要設定 Proxy 帳戶來建立及管理 SQL Server Agent 作業步驟**  
  
1.  在 **[物件總管]** 中展開伺服器。  
  
2.  展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [Proxy]，然後選取 [新增 Proxy]。  
  
4.  在 **[新 Proxy 帳戶]** 對話方塊的 **[一般]** 頁面上，指定新 Proxy 的 Proxy 名稱、認證名稱及描述。 請注意，在建立 SQL Server Agent Proxy 之前，您必須先建立認證。 如需建立認證的詳細資訊，請參閱[如何：建立認證 (SQL Server Management Studio)](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586) 及 [CREATE CREDENTIAL (Transact-SQL)](https://msdn.microsoft.com/d5e9ae69-41d9-4e46-b13d-404b88a32d9d)。  
  
5.  檢查這個 Proxy 適當的子系統。  
  
6.  在 **[主體]** 頁面上，加入或移除登入或角色，藉此授與或移除 Proxy 帳戶的存取。  
  
## <a name="see-also"></a>另請參閱  
[實作 SQL Server Agent 安全性](../../ssms/agent/implement-sql-server-agent-security.md)  
  
