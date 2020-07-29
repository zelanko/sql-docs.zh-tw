---
title: 設定 SQL Server Agent 服務的 SQL Server 連線
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5aaf9e5a73edb232c237618c97aaea68cc732848
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85644492"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service"></a>設定 SQL Server Agent 服務的 SQL Server 連線

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]之間的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務可使用「Windows 驗證」連接到 SQL Server 的本機執行個體。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就不支援「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」。 只有當您管理舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶所需之 Windows 權限的詳細資訊，請參閱＜ [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) ＞及＜ [設定 Windows 服務帳戶](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>若要設定 SQL Server 連接  
  
1.  在 **[物件總管]** 中，按一下加號展開要設定與其 SQL Server Agent 服務連接的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，然後選取 [屬性]  。  
  
3.  在 [SQL Server Agent 屬性]  對話方塊的 [選取頁面]  底下，按一下 [連線]  。  
  
4.  在 [SQL Server 連線]  底下選取 [使用 Windows 驗證]  ，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 驗證來連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)] [!INCLUDE[msCoName](../../includes/msconame_md.md)] 的執行個體。 連接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的資料庫需要 Windows 驗證。  
  
