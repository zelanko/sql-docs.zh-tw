---
title: "設定用戶端通訊協定 | Microsoft Docs"
ms.custom: 
ms.date: 07/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
caps.latest.revision: "35"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9f3e68de28e6dd2052b2f0fd0f40acd5a167678
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="configure-client-protocols"></a>設定用戶端通訊協定
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定管理員，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定用戶端應用程式所使用的用戶端通訊協定。 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援使用 TCP/IP 網路通訊協定和具名管道通訊協定來進行用戶端通訊。 如果用戶端是連接到同一部電腦上的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，也可以使用共用記憶體通訊協定。 選取通訊協定有三種常見的方法。  
  
-   您可以在「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」中設定通訊協定順序，來設定所有用戶端應用程式使用相同的網路通訊協定。  
  
-   藉由建立別名，您可以設定單一用戶端應用程式使用不同的網路通訊協定。 如需詳細資訊，請參閱[建立或刪除用戶端使用的伺服器別名 &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)。  
  
-   有些用戶端應用程式 (如 sqlcmd.exe) 可以指定通訊協定做為連接字串的一部分。 如需詳細資訊，請參閱[使用 sqlcmd 連接至 Database Engine](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
###  <a name="EnableDisable"></a> 啟用或停用用戶端通訊協定  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，展開 [SQL Server Native Client Configuration (SQL Server Native Client 組態)]，並以滑鼠右鍵按一下 [用戶端通訊協定]，然後按一下 [屬性]。  
  
2.  在 **[停用的通訊協定]** 方塊中按一下某通訊協定，再按一下 **[啟用]**，即可啟用通訊協定。  
  
3.  在 **[啟用的通訊協定]** 方塊中按一下某通訊協定，再按一下 **[停用]**，即可停用通訊協定。  
  
###  <a name="ChangeDefault"></a> 變更用戶端電腦的預設通訊協定或通訊協定順序  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，展開 [SQL Server Native Client Configuration (SQL Server Native Client 組態)]，並以滑鼠右鍵按一下 [用戶端通訊協定]，然後按一下 [屬性]。  
  
2.  在 **[啟用的通訊協定]** 方塊中，按一下 **[上移]** 或 **[下移]**，來變更要連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時使用通訊協定的順序。 **[啟用的通訊協定]** 方塊裡最上方的通訊協定，是預設通訊協定。  
  
    > [!IMPORTANT]  
    >  「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員」會為伺服器別名組態與預設用戶端網路程式庫建立登錄項目。 然而，應用程式並不會安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端網路程式庫或網路通訊協定。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用戶端網路程式庫是在安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時安裝；網路通訊協定是在安裝 Microsoft Windows 時安裝 (或透過 [控制台] 中的 [網路] 安裝)。 某些特定網路通訊協定可能不會隨 Windows 安裝。 如需有關安裝這些網路通訊協定的詳細資訊，請參閱供應商說明文件。  
  
###  <a name="Configure"></a> 設定用戶端使用 TCP/IP  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，展開 [SQL Server Native Client Configuration (SQL Server Native Client 組態)]，並以滑鼠右鍵按一下 [用戶端通訊協定]，然後按一下 [屬性]。  
  
2.  請在 **[啟用的通訊協定]** 方塊中，按一下向上箭號與向下箭號，以便在嘗試連接 SQL Server 時變更通訊協定的順序。 **[啟用的通訊協定]** 方塊裡最上方的通訊協定，是預設通訊協定。  
  
 您可以勾選 **[啟用共用記憶體通訊協定]** 方塊來個別啟用共用記憶體通訊協定。  
  
## <a name="see-also"></a>另請參閱  
 [設定遠端登入逾時伺服器組態選項](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
