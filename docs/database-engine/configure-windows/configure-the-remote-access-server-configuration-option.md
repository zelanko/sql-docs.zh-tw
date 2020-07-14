---
title: 設定 remote access 伺服器組態選項 | Microsoft Docs
description: 了解即將淘汰之遠端存取選項的替代方案。 檢視可用來對 SQL Server 連線問題進行疑難排解的其他來源。
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], stored procedure execution
ms.assetid: f5de748d-1c55-4714-9661-38fe62e5095f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fba193e5f6493e722bd1171c333b4aa2e700ff50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785802"
---
# <a name="configure-the-remote-access-server-configuration-option"></a>設定 remote access 伺服器組態選項
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本主題是關於「遠端存取」功能。 這個組態選項是即將淘汰的模糊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通訊功能，建議您不要使用這項功能。 如果您因為無法連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而到達此頁面，請改為參閱下列其中一項主題：  
  
-   [教學課程：資料庫引擎使用者入門](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  
-   [登入 SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md)  
  
-   [當系統管理員遭到鎖定時連接到 SQL Server](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
-   [連接至已註冊的伺服器 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/connect-to-a-registered-server-sql-server-management-studio.md)  
  
-   [從 SQL Server Management Studio 連接到任何 SQL Server 元件](../../ssms/f1-help/connect-to-any-sql-server-component-from-sql-server-management-studio.md)  
  
-   [使用 sqlcmd 連接至 Database Engine](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md)  
  
-   [如何疑難排解與 SQL Server Database Engine 的連接](https://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
 程式設計人員可能會對下列主題感興趣︰  
  
-   [How To:Connect to SQL Server Using SQL Authentication in ASP.NET 2.0](https://msdn.microsoft.com/library/ff648340.aspx) (如何：使用 ASP.NET 2.0 中的 SQL 驗證連接到 SQL Server)  
  
-   [連接到 SQL Server 的執行個體](../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)  
  
-   [操作說明：建立 SQL Server 資料庫的連線](https://msdn.microsoft.com/library/s4yys16a.aspx)  
  
 **從這裡開始是本主題的主要內文。**  
  
 此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] remote access [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **remote access** 選項會控制本機或遠端伺服器 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的執行所在) 上執行的預存程序。 這個選項的預設值是 1。 這會授與權限以從遠端伺服器執行本機預存程序，或從本機伺服器執行遠端預存程序。 若要防止在遠端伺服器上執行本機預存程序，或在本機伺服器上執行遠端預存程序，請將此選項設定為 0。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 請改用 [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)。
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 remote access 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定遠端存取選項之後](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   [遠端存取] 選項只適用於透過 [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) 新增的伺服器，且其包含回溯相容性。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-access-option"></a>設定 remote access 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[連接]** 節點。  
  
3.  在 **[遠端伺服器連接]** 下，選取或清除 **[允許此伺服器的遠端連接]** 核取方塊。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-remote-access-option"></a>設定 remote access 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 將 `remote access` 選項的值設定為 `0`。  
  
```sql  
EXEC sp_configure 'remote access', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="follow-up-after-you-configure-the-remote-access-option"></a><a name="FollowUp"></a> 後續操作：設定遠端存取選項之後  
 此設定在您重新啟動 SQL Server 後才會生效。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
