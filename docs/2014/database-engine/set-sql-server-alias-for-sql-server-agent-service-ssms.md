---
title: 將 SQL Server 別名設定 SQL Server Agent 服務 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c1f54692a79d2b3108d60ddfee5e3611e6d6dd4
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43818074"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 設定 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 別名，以供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 用來連接到 [!INCLUDE[ssDE](../includes/ssde-md.md)]。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 服務預設會使用不需要額外的用戶端組態之動態伺服器名稱，透過具名管道連接至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體。 只有未使用預設網路傳輸，或當您連接到正在接聽替代具名管道之 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體時，才需要設定伺服器連接別名。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [若要使用 SQL Server Management Studio，為 SQL Server Agent 服務設定 SQL Server 別名](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 之本機執行個體的別名，否則 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需有關所需的 Windows 權限[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Agent 服務帳戶，請參閱 <<c2> [ 選取 SQL Server Agent 服務的帳戶](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶和權限](configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>若要為 SQL Server Agent 服務設定 SQL Server 別名  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後按一下 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 <伺服器名稱>] 對話方塊的 [選取頁面] 底下，選取 [連線]，然後  
  
4.  在 **[別名本機主機伺服器]** 方塊中，輸入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent 要連接之伺服器的別名。  
  
5.  按一下 [確定] 。  
  
  
