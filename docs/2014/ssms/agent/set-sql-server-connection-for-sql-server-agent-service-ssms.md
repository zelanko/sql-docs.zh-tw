---
title: 設定 SQL Server Agent 服務的 SQL Server 連接（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: stevestein
ms.author: sstein
ms.openlocfilehash: 686e7026495c827101b279ee779db0e30852bb49
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067593"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>設定 SQL Server Agent 服務的 SQL Server 連線 (SQL Server Management Studio)
  此主題描述如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]之間的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務可使用「Windows 驗證」連接到 SQL Server 的本機執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要為 SQL Server Agent 設定 SQL Server 連接，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 就不支援「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證」。 只有當您管理舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，才能使用這個選項。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需 Agent 服務帳戶所需之 Windows 許可權的詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，請參閱[選取 SQL Server Agent 服務的帳戶](select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶與許可權](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>若要設定 SQL Server 連接  
  
1.  在 **[物件總管]** 中，按一下加號展開要設定與其 SQL Server Agent 服務連接的伺服器。  
  
2.  以滑鼠右鍵按一下**SQL Server Agent** ，然後選取 [**屬性**]。  
  
3.  在 [SQL Server Agent 屬性]**** 對話方塊的 [選取頁面]**** 底下，按一下 [連線]****。  
  
4.  在 [SQL Server 連線]**** 底下選取 [使用 Windows 驗證]****，讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 使用  Windows 驗證來連接到 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體。 連接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的資料庫需要 Windows 驗證。  
  
  
