---
title: 設定 SQL Server 連接 SQL Server Agent 服務 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a05c720a2db962683c81ad948aa616b5c6b20fd1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48161418"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>設定 SQL Server Agent 服務的 SQL Server 連線 (SQL Server Management Studio)
  此主題描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]之間的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務可使用「Windows 驗證」連接到 SQL Server 的本機執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要為 SQL Server Agent 設定 SQL Server 連接，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就不支援「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」。 只有當您管理舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需有關所需的 Windows 權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 服務帳戶，請參閱 <<c2> [ 選取 SQL Server Agent 服務的帳戶](select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶和權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>若要設定 SQL Server 連接  
  
1.  在 **[物件總管]** 中，按一下加號展開要設定與其 SQL Server Agent 服務連接的伺服器。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後選取 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 <伺服器名稱>] 對話方塊的 [選取頁面] 底下，按一下 [連線]。  
  
4.  在 [SQL Server 連接] 底下選取 [使用 Windows 驗證]，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 利用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 驗證連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。 連接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的資料庫需要 Windows 驗證。  
  
  
