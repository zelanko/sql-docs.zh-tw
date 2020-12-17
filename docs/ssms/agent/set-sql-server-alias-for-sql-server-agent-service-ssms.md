---
description: 設定 SQL Server Agent 服務的 SQL Server 別名
title: 設定 SQL Server Agent 服務的 SQL Server 別名
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 4530aebde58448903015b8f948ad8f005d9134ee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472239"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service"></a>設定 SQL Server Agent 服務的 SQL Server 別名

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> [Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL 受控執行個體與 SQL Server 之間的 T-SQL 差異](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 設定 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 別名，以供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用來連線到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務預設會使用不需要額外的用戶端組態之動態伺服器名稱，透過具名管道連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 只有未使用預設網路傳輸，或當您連接到正在接聽替代具名管道之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，才需要設定伺服器連接別名。  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>限制事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之本機執行個體的別名，否則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   只有當您擁有使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 節點的權限時，[物件總管] 才會顯示該節點。  
  
### <a name="security"></a><a name="Security"></a>安全性  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissions  
若要執行功能，您必須將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 設定為使用帳戶認證，此帳戶必須是 **中** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](系統管理員) 固定伺服器角色的成員。 此帳戶必須擁有下列 Windows 權限：  
  
-   以服務登入 (SeServiceLogonRight)  
  
-   取代處理序層級 Token (SeAssignPrimaryTokenPrivilege)  
  
-   略過跨越檢查 (SeChangeNotifyPrivilege)  
  
-   調整處理序的記憶體配額 (SeIncreaseQuotaPrivilege)  
  
如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶所需之 Windows 權限的詳細資訊，請參閱＜ [選取 SQL Server Agent 服務的帳戶](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) ＞及＜ [設定 Windows 服務帳戶](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)＞。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>若要為 SQL Server Agent 服務設定 SQL Server 別名  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)] 的執行個體，然後展開該執行個體。  
  
2.  以滑鼠右鍵按一下 [SQL Server Agent]，然後按一下 [屬性]。  
  
3.  在 [SQL Server Agent 屬性 _server\_name_] 對話方塊的 [選取頁面] 底下，選取 [連線]，然後  
  
4.  在 **[別名本機主機伺服器]** 方塊中，輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 要連接之伺服器的別名。  
  
5.  按一下 [確定]  。  
