---
title: 設定 SQL Server Agent 服務的 SQL Server 別名（SQL Server Management Studio） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 752796caafa86ece1b471beb25a77ea381497409
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62774390"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  本主題描述如何使用[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]設定別名，以供 Agent 用來連接到。 
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務預設會使用不需要額外的用戶端組態之動態伺服器名稱，透過具名管道連接至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。 只有未使用預設網路傳輸，或當您連接到正在接聽替代具名管道之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體時，才需要設定伺服器連接別名。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   [使用 SQL Server Management Studio 設定 SQL Server Agent 服務的 SQL Server 別名](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之本機執行個體的別名，否則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務帳戶所需之 Windows 許可權的詳細資訊，請參閱[選取 SQL Server Agent 服務的帳戶](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)和[設定 windows 服務帳戶與許可權](configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>若要為 SQL Server Agent 服務設定 SQL Server 別名  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]  ，然後按一下 [屬性]  。  
  
3.  在 [ **SQL Server Agent 屬性**_server_name_ ] 對話方塊的 [**選取頁面**] 底下，選取 [**連接**]，然後  
  
4.  在 **[別名本機主機伺服器]** 方塊中，輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 要連接之伺服器的別名。  
  
5.  按一下 [確定]  。  
  
  
