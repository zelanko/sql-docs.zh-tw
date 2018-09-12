---
title: 實作 SQL Server Agent 安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, security
- security [SQL Server Agent], about security
- security [SQL Server Agent]
- security [SQL Server], SQL Server Agent
ms.assetid: d770d35c-c8de-4e00-9a85-7d03f45a0f0d
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b945b42542948a52c0bec32de41afbf7ce664c
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818804"
---
# <a name="implement-sql-server-agent-security"></a>實作 SQL Server Agent 安全性
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 讓資料庫管理員可以在只具有執行作業步驟所需權限的安全內容中執行每個作業步驟，此權限由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent Proxy 決定。 若要設定特定作業步驟的權限，請建立具有必要權限的 Proxy，然後將該 Proxy 指派給作業步驟。 您可以將 Proxy 指派給多個作業步驟。 對於要求相同權限的作業步驟，可以使用相同的 Proxy。  
  
 下一節將解釋您必須授與使用者哪些資料庫角色，他們才能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來建立或執行作業。  
  
## <a name="granting-access-to-sql-server-agent"></a>授與 SQL Server Agent 的存取權  
 若要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent，使用者必須是下列一個或多個固定資料庫角色的成員：  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 這些角色儲存在 **msdb** 資料庫中。 根據預設，沒有任何使用者隸屬於這些資料庫角色的成員。 您必須明確授與這些角色的成員資格。 **系統管理員** 固定伺服器角色的成員使用者對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 具有完整的存取權，完全不需要是這些固定資料庫角色的成員，就能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。 若使用者不是這些資料庫角色或 **系統管理員** 角色的成員，當他們使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，將無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent 節點。  
  
 這些資料庫角色的成員可以檢視與執行自己所擁有的物件，並建立以現有 Proxy 帳戶身分執行的作業步驟。 如需上述每個角色所關聯之特定權限的詳細資訊，請參閱＜ [SQL Server Agent 固定資料庫角色](sql-server-agent-fixed-database-roles.md)＞。  
  
 **系統管理員** 固定伺服器角色的成員有權建立、修改與刪除 Poxy 帳戶。 **系統管理員** 角色的成員有權建立以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶 (此帳戶是用於啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的帳戶)。  
  
## <a name="guidelines"></a>指導方針  
 請依照下列指導方針來改進 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 實作的安全性。  
  
-   為 Proxy 建立專屬的使用者帳戶，並只使用這些 Proxy 使用者帳戶來執行作業步驟。  
  
-   只授與必要的權限給 Proxy 使用者帳戶。 對於指派給特定 Proxy 帳戶的作業步驟，只授與它們執行所需的必要權限。  
  
-   請勿使用隸屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows Administrators **群組的 Microsoft Windows 帳戶身分執行** Agent 服務。  
  
-   只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認證存放區安全，Proxy 才安全。  
  
-   如果使用者寫入作業可以寫入 NT 事件記錄檔，它們可以透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 引發警示。  
  
-   請勿將 NT 管理員帳戶指定為服務帳戶或 Proxy 帳戶。  
  
-   請注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 有存取對方資產的權限。 這兩個服務共用單一處理序空間，而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務上的系統管理員 (sysadmin)。  
  
-   當 TSX 在 MSX 上編列時，MSX 系統管理員 (sysadmin) 會取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]TSX 執行個體的完整控制權。  
  
-   ACE 是延伸模組，並不能叫用它本身。 ACE 是由 Chainer ScenarioEngine.exe (也稱為 Microsoft.SqlServer.Chainer.Setup.exe) 叫用，也可由另一個主機處理序叫用。  
  
-   ACE 取決於 SSDP 所擁有的下列組態 DLL，因為 ACE 會呼叫 DLL 的這些 API：  
  
    -   **SCO** - Microsoft.SqlServer.Configuration.Sco.dll，包括虛擬帳戶的新 SCO 驗證  
  
    -    - Microsoft.SqlServer.Configuration.Cluster.dll  
  
    -   **SFC** - Microsoft.SqlServer.Configuration.SqlConfigBase.dll  
  
    -   **延伸模組** - Microsoft.SqlServer.Configuration.ConfigExtension.dll  
  
## <a name="see-also"></a>另請參閱  
 [Predefined Roles](../../reporting-services/security/role-definitions-predefined-roles.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)   
 [sp_droprolemember &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)   
 [SQL Server Database Engine 和 Azure SQL Database 的資訊安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
