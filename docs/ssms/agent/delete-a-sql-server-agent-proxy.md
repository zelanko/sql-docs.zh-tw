---
title: 刪除 SQL Server Agent Proxy | Microsoft Docs
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
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73c929f0935cc5461eed6a7ac043ab24c2b4cf32
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33045125"
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database 受控執行個體](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)目前支援多數 (但非全部) 的 SQL Server Agent 功能。 如需詳細資料，請參閱 [Azure SQL Database 受控執行個體與 SQL Server 之間的 T-SQL 差異](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)。

此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 或 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] ，在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 中刪除 [!INCLUDE[tsql](../../includes/tsql_md.md)]Agent Proxy 帳戶。  
  
**本主題內容**  
  
-   **開始之前：**  
  
    [限制事項](#Restrictions)  
  
    [Security](#Security)  
  
-   **若要使用下列項目刪除 SQL Server Agent Proxy 帳戶：**  
  
    [Transact-SQL](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>開始之前  
  
### <a name="Restrictions"></a>限制事項  
  
-   當您刪除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Proxy 帳戶時，請確定該 Proxy 未參考任何作用中的作業步驟。 若要檢查是否有任何作業步驟參考該 Proxy，請以滑鼠右鍵按一下該 Proxy，選取 [屬性]，然後選取 [<Proxy 名稱> Proxy 帳戶屬性] 對話方塊中的 [參考] 頁面。 如果刪除一個 Proxy， **[刪除物件]** 對話方塊中有個選項，可以重新指派該 Proxy 使用的所有作業步驟。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent Proxy 使用認證來儲存 Windows 使用者帳戶的相關資訊。 認證中所指定的使用者，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行的電腦上必須要有「以批次工作登入」的權限。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會檢查 Proxy 的子系統存取權，而且每當作業步驟執行時，就會提供 Proxy 的存取權。 如果 Proxy 不再擁有子系統的存取權，作業步驟就會失效。 否則， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent 會模擬 Proxy 中所指定的使用者，並執行作業步驟。  
  
-   如果使用者的登入身分可以存取 Proxy，或者使用者隸屬於可存取 Proxy 的角色，該使用者就可以使用作業步驟中的 Proxy。  
  
### <a name="Security"></a>Security  
  
#### <a name="Permissions"></a>Permissions  
只有 **sysadmin** 固定伺服器角色的成員才能建立、修改或刪除 Proxy 帳戶。  
  
## <a name="SSMSProcedure"></a>使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>若要刪除 SQL Server Agent Proxy 帳戶  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含要刪除之 Agent Proxy 帳戶的伺服器。  
  
2.  按一下加號展開 **[SQL Server Agent]**。  
  
3.  按一下加號展開 **[Proxy]** 資料夾。  
  
4.  按一下加號，展開包含要刪除之 Proxy 帳戶的子系統 (例如 [ActiveX Script])。  
  
5.  以滑鼠右鍵按一下您要刪除的 Proxy 帳戶，然後選取 [刪除]。  
  
6.  在 **[刪除物件]** 對話方塊中，確認已選取正確的 Proxy 帳戶。 核取 **[重新指派給]** 核取方塊，將參考此 Proxy 帳戶的工作步驟重新指派給另一個帳戶。  
  
7.  按一下 [確定] 。  
  
## <a name="TsqlProcedure"></a>使用 Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>若要刪除 SQL Server Agent Proxy 帳戶  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde_md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
如需詳細資訊，請參閱 [sp_delete_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c)。  
  
