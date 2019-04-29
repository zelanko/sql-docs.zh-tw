---
title: 設定服務啟動帳戶的 SQL Server Agent （SQL Server 組態管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30c50d1f6efc44c17eac76e0e03432c2461da296
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63033648"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動帳戶會定義 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行的 Windows 帳戶以及它的網路權限。 此主題描述如何透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 組態管理員來設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Agent 服務帳戶。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [若要使用 SQL Server Management Studio，為 SQL Server Agent 設定服務啟動帳戶](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]開始， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 不再要求服務啟動帳戶一定是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Administrators 群組的成員。 不過， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務啟動帳戶必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin 固定伺服器角色的成員。 如果使用多伺服器作業處理，帳戶也必須是主要伺服器上 msdb 資料庫角色 TargetServersRole 的成員。  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要執行其函式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理程式必須設定為使用之成員的帳戶認證`sysadmin`固定的伺服器角色中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需有關所需的 Windows 權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 服務帳戶，請參閱 <<c2> [ 選取 SQL Server Agent 服務的帳戶](select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶和權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>若要為 SQL Server Agent 設定服務啟動帳戶  
  
1.  在 **[已註冊的伺服器]**，按一下加號展開 **[Database Engine]**。  
  
2.  按一下加號展開 **[本機伺服器群組]** 資料夾。  
  
3.  以滑鼠右鍵按一下您要設定服務啟動帳戶的伺服器執行個體，並選取 [SQL Server 組態管理員...]。  
  
4.  在 **[使用者帳戶控制]** 對話方塊中，按一下 **[是]**。  
  
5.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員的主控台窗格中，選取 **[SQL Server 服務]**。  
  
6.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server Agent (<伺服器名稱>)]，其中 <伺服器名稱> 是您要變更服務啟動帳戶的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 執行個體的名稱，然後選取 [屬性]。  
  
7.  在 [SQL Server Agent (<伺服器名稱>) 屬性] 對話方塊的 [登入] 索引標籤中，選取 [登入身分] 下的下列其中一個選項：  
  
    -   **內建帳戶**：如果您的作業僅需來自本機伺服器的資源，請選取此選項。 如需有關如何選擇 Windows 內建帳戶類型的詳細資訊，請參閱[選取 SQL Server Agent 服務的帳戶](https://msdn.microsoft.com/library/ms191543.aspx)。  
  
        > [!IMPORTANT]  
        >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務不支援 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的 [本機服務] 帳戶。  
  
    -   **這個帳戶**：如果您的作業需要網路上的資源 (包括應用程式資源)，或想要將事件轉寄給其他 Windows 應用程式記錄檔，又或者想要透過電子郵件或呼叫器來通知操作員，請選取此選項。  
  
         如果您選取這個選項：  
  
        1.  在 **[帳戶名稱]** 方塊中，輸入將用來執行 SQL Server Agent 的帳戶。 或者，按一下 **[瀏覽]** 開啟 **[選取使用者或群組]** 對話方塊，然後選取要使用的帳戶。  
  
        2.  在 **[密碼]** 方塊中，輸入帳戶的密碼。 在 [確認密碼] 方塊中重新輸入密碼。  
  
8.  按一下 [確定] 。  
  
9. 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，按一下 **[關閉]** 按鈕。  
  
  
