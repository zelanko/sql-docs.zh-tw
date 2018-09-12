---
title: 重新命名 SQL Server Agent 錯誤記錄檔 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- renaming SQL Server Agent error log
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: dee2b199-48af-44cb-9177-d029a5edb169
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b69da2ab744d594d0d149a59e4f86c52481f4e70
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815074"
---
# <a name="rename-a-sql-server-agent-error-log-sql-server-management-studio"></a>Rename a SQL Server Agent Error Log (SQL Server Management Studio)
  此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中重新命名 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤所寫入的檔案。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [若要使用 SQL Server Management Studio 重新命名 SQL Server Agent 錯誤記錄檔](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 不會寫入到新的記錄檔中，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務重新啟動。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
 如需有關所需的 Windows 權限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agent 服務帳戶，請參閱 <<c2> [ 選取 SQL Server Agent 服務的帳戶](select-an-account-for-the-sql-server-agent-service.md)和[設定 Windows 服務帳戶和權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-sql-server-agent-error-log"></a>若要重新命名 SQL Server Agent 錯誤記錄檔  
  
1.  在 **[物件總管]** 中，按一下加號展開伺服器，此伺服器包含要重新命名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 錯誤記錄檔。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [錯誤記錄檔] 資料夾，然後選取 [設定]。  
  
4.  在 **[設定 SQL Server Agent 錯誤記錄檔]** 對話方塊的 **[錯誤記錄檔]** 方塊中，輸入錯誤記錄檔的新路徑與檔案名稱。 或者，按一下省略符號 **(...)** 開啟 [指定代理程式錯誤記錄檔的位置] 對話方塊。  
  
5.  完成後，請按一下 **[確定]**。  
  
  
