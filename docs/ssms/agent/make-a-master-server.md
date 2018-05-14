---
title: 設為主要伺服器 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 12fe6ba1182f5ad4cfa60176eba40a3de28971a3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 設為主要伺服器 [!INCLUDE[tsql](../../includes/tsql_md.md)]。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [Security](#Security)  
  
-   **若要設為主要伺服器，使用：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Security"></a>Security  
具有與 Proxy 相關聯之步驟的散發式作業，而該 Proxy 是在目標伺服器上的 Proxy 帳戶內容下執行 。 請確保符合以下條件，否則與 Proxy 相關聯之作業步驟將不會從主要伺服器下載至目標：  
  
-   主要伺服器登錄子機碼 **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;執行個體名稱&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) 設定為 1 (true)。 依預設，這個子機碼設為 0 (False)。  
  
-   存在於目標伺服器上的 Proxy 帳戶，而該帳戶名稱與執行作業步驟之主要伺服器上的 Proxy 帳戶名稱相同。  
  
如果使用 Proxy 帳戶的作業步驟在從主要伺服器下載 Proxy 帳戶至目標伺服器時失敗，您可以在 **msdb** 資料庫的 **sysdownloadlist** 資料表中，檢查 **error_message** 資料行，以了解下列錯誤訊息：  
  
-   「作業步驟需要 Proxy 帳戶，不過目標伺服器上已停用 Proxy 比對。」  
  
    若要解決這個錯誤，請將 **AllowDownloadedJobsToMatchProxyName** 登錄子機碼設為 1。  
  
-   「找不到 Proxy。」  
  
    若要解決這個錯誤，請確定目標伺服器上有 Proxy 帳戶，且帳戶名稱與執行該作業步驟的主要伺服器 Proxy 帳戶相同。  
  
#### <a name="Permissions"></a>Permissions  
這個程序的執行權限預設會授與 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-make-a-master-server"></a>若要設為主要伺服器  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 **[SQL Server Agent]**，指向 **[多重伺服器管理]**，然後按一下 **[設為主要伺服器]**。 **「主要伺服器精靈」** 會引導您完成設定主要伺服器與新增目標伺服器的步驟。  
  
3.  從 [主要伺服器操作員] 頁面設定主要伺服器的操作員。若要使用電子郵件或呼叫器傳送通知給操作員，則必須設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 來傳送電子郵件。 若要使用 **net send**傳送通知給操作員， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 所在伺服器上必須執行 Messenger 服務。  
  
    **電子郵件地址**  
    設定操作員的電子郵件地址。  
  
    **呼叫器號碼**  
    設定操作員的呼叫器電子郵件地址。  
  
    **Net Send 位址**  
    設定操作員的 **net send** 地址。  
  
4.  從 **[目標伺服器]** 頁面選取主要伺服器的目標伺服器。  
  
    **已註冊的伺服器**  
    列出在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 註冊，但尚未成為目標伺服器的伺服器。  
  
    **目標伺服器**  
    列出目標伺服器。  
  
    **>**  
    將選取的伺服器移動至目標伺服器清單。  
  
    **>>**  
    將所有的伺服器移動至目標伺服器清單。  
  
    **<**  
    將選取的伺服器從目標伺服器清單中移除。  
  
    **<<**  
    將所有的伺服器從目標伺服器清單中移除。  
  
    **加入連接**  
    將伺服器加入目標伺服器清單中，但不註冊伺服器。  
  
    **[連接]**  
    變更選取之伺服器的連接屬性。  
  
5.  從 **[主要伺服器登入認證]** 頁面指定在必要時，是否要為目標伺服器建立新的登入，並指派存取主要伺服器的權限給該登入。  
  
    **如有必要，請建立新的登入，並指派存取 MSX 的權限給該登入**  
    如果指定的登入並不存在，就會在目標伺服器上建立新的登入。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-make-a-master-server"></a>若要設為主要伺服器  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會將目前的伺服器列入 AdventureWorks1 主要伺服器中。 目前伺服器的位置是「第 21 棟，309 室，機架 5」。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
如需詳細資訊，請參閱 [sp_msx_enlist (Transact-SQL)](http://msdn.microsoft.com/en-us/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)。  
  
## <a name="see-also"></a>另請參閱  
[建立多伺服器環境](../../ssms/agent/create-a-multiserver-environment.md)  
[將整個企業的管理自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
