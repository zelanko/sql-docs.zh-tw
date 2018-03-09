---
title: "重新命名 SQL Server Agent 錯誤記錄檔 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- renaming SQL Server Agent error log
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: dee2b199-48af-44cb-9177-d029a5edb169
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b229be163df855d4594fec608c58248ab17d486e
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="rename-a-sql-server-agent-error-log-sql-server-management-studio"></a>Rename a SQL Server Agent Error Log (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]，在 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 中重新命名 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤所寫入的檔案。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   [若要使用 SQL Server Management Studio 重新命名 SQL Server Agent 錯誤記錄檔](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 不會寫入到新的記錄檔中，除非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務重新啟動。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 服務帳戶所需之 Windows 權限的詳細資訊，請參閱＜ [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) ＞及＜ [設定 Windows 服務帳戶](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014)＞。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-rename-a-sql-server-agent-error-log"></a>若要重新命名 SQL Server Agent 錯誤記錄檔  
  
1.  在 **[物件總管]**中，按一下加號展開伺服器，此伺服器包含要重新命名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 錯誤記錄檔。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  以滑鼠右鍵按一下 [錯誤記錄檔] 資料夾，然後選取 [設定]。  
  
4.  在 **[設定 SQL Server Agent 錯誤記錄檔]** 對話方塊的 **[錯誤記錄檔]** 方塊中，輸入錯誤記錄檔的新路徑與檔案名稱。 或者，按一下省略符號 **(...)** 開啟 [指定代理程式錯誤記錄檔的位置] 對話方塊。  
  
5.  完成後，請按一下 **[確定]**。  
  
