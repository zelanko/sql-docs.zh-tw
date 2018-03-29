---
title: 設定 SQL Server Agent 服務的 SQL Server 連線 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a2b5fcb2c67908df884e557acfded17203abfd9
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>設定 SQL Server Agent 服務的 SQL Server 連線 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 中使用 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 設定 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] Agent 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]之間的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務可使用「Windows 驗證」連接到 SQL Server 的本機執行個體。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要為 SQL Server Agent 設定 SQL Server 連接，使用：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 就不支援「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證」。 只有當您管理舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]時，才能使用這個選項。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務帳戶所需之 Windows 權限的詳細資訊，請參閱＜ [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) ＞及＜ [設定 Windows 服務帳戶](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)＞。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>若要設定 SQL Server 連接  
  
1.  在 **[物件總管]**中，按一下加號展開要設定與其 SQL Server Agent 服務連接的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 <伺服器名稱>] 對話方塊的 [選取頁面] 底下，按一下 [連線]。  
  
4.  在 [SQL Server 連接] 底下選取 [使用 Windows 驗證]，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 利用 [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] [!INCLUDE[ssDE](../../includes/ssde_md.md)] 的執行個體。 連接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] 及更新版本的資料庫需要 Windows 驗證。  
  
