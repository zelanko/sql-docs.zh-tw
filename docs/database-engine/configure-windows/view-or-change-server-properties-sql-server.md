---
title: 檢視或變更伺服器屬性 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.connectionproperties.f1
helpviewer_keywords:
- viewing server properties
- server properties [SQL Server]
- displaying server properties
- servers [SQL Server], viewing
- Connection Properties dialog box
ms.assetid: 55f3ac04-5626-4ad2-96bd-a1f1b079659d
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7f451695c66eb15916ba5eb415b2cce159df4569
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40406708"
---
# <a name="view-or-change-server-properties-sql-server"></a>檢視或變更伺服器屬性 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 SQL Server 組態管理員檢視或變更 [!INCLUDE[tsql](../../includes/tsql-md.md)]執行個體的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要檢視或變更伺服器屬性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SQL Server 組態管理員](#PowerShellProcedure)  
  
-   **後續操作：**[變更伺服器屬性之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   使用 sp_configure 時，您必須在設定組態選項之後，執行 RECONFIGURE 或 RECONFIGURE WITH OVERRIDE。 RECONFIGURE WITH OVERRIDE 陳述式通常是保留給應該非常小心使用的組態選項。 但是 RECONFIGURE WITH OVERRIDE 對所有組態選項都有效，所以它可以取代 RECONFIGURE。  
  
    > [!NOTE]  
    >  RECONFIGURE 會在交易中執行。 如果任何重新設定作業失敗，所有重新設定作業都不會生效。  
  
-   有些屬性頁面會透過 Windows Management Instrumentation (WMI) 取得資訊。 若要顯示這些頁面，您必須將 WMI 安裝在執行 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的電腦上。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 如需詳細資訊，請參閱 [伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)。  
  
 依預設，所有使用者都會取得不含參數或只含第一個參數之 **sp_configure** 的執行權限。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-change-server-properties"></a>檢視或變更伺服器屬性  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在 **[伺服器屬性]** 對話方塊中，按一下頁面以檢視或變更有關該頁面的伺服器資訊。 部分屬性是唯讀的。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-server-properties-by-using-the-serverproperty-built-in-function"></a>若要使用 SERVERPROPERTY 內建函數檢視伺服器屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會在 [陳述式中使用](../../t-sql/functions/serverproperty-transact-sql.md) SERVERPROPERTY `SELECT` 內建函數傳回目前伺服器的相關資訊。 當 Windows 伺服器安裝了多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，且用戶端必須開啟另一項連接來連到目前連接所用的相同執行個體時，這個狀況非常有用。  
  
    ```sql  
    SELECT CONVERT( sysname, SERVERPROPERTY('servername'));  
    GO  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysservers-catalog-view"></a>若要使用 sys.servers 類別目錄檢視表檢視伺服器屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會查詢 [sys.servers](../../relational-databases/system-catalog-views/sys-servers-transact-sql.md) 目錄檢視，以傳回目前伺服器的名稱 (`name`) 和識別碼 (`server_id`)，以及用來連接到連結之伺服器的 OLE DB 提供者名稱 (`provider`)。  
  
    ```sql  
    USE AdventureWorks2012;   
    GO  
    SELECT name, server_id, provider  
    FROM sys.servers ;   
    GO  
  
    ```  
  
#### <a name="to-view-server-properties-by-using-the-sysconfigurations-catalog-view"></a>若要使用 sys.configurations 類別目錄檢視表檢視伺服器屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例會查詢 [sys.configurations](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md) 類別目錄檢視，以傳回目前伺服器上每個伺服器組態選項的相關資訊。 此範例會傳回選項的名稱 (`name`) 和描述 (`description`)，以及選項是否為進階選項 (`is_advanced`)。  
  
    ```wmimof  
    USE AdventureWorks2012;   
    GO  
    SELECT name, description, is_advanced  
    FROM sys.configurations ;   
    GO  
  
    ```  
  
#### <a name="to-change-a-server-property-by-using-spconfigure"></a>使用 sp_configure 變更伺服器屬性  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 變更伺服器屬性。 此範例會將 `fill factor` 選項的值變更為 `100`。 伺服器必須重新啟動，變更才會生效。  
  
```sql  
Use AdventureWorks2012;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'fill factor', 100;  
GO  
RECONFIGURE;  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)的電腦上。  
  
##  <a name="PowerShellProcedure"></a> 使用 SQL Server 組態管理員  
 部分伺服器屬性可以使用 SQL Server 組態管理員檢視或變更。 例如，您可以檢視 SQL Server 執行個體的版本和版別，或是變更錯誤記錄檔儲存的位置。 您也可以藉由查詢 [伺服器相關的動態管理檢視與函數](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)的方式檢視這些屬性。  
  
#### <a name="to-view-or-change-server-properties"></a>檢視或變更伺服器屬性  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
2.  在 **[SQL Server 組態管理員]** 中，按一下 **[SQL Server 服務]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server (\<執行個體名稱>)]****，然後按一下 [屬性]。  
  
4.  在 [SQL Server (\<執行個體名稱>) 屬性]**** 對話方塊中，變更 [服務] 索引標籤或 [進階] 索引標籤上的伺服器屬性，然後按一下 [確定]。  
  
##  <a name="FollowUp"></a> 待處理：變更伺服器屬性之後  
 對於某些屬性，伺服器可能必須重新啟動，變更才會生效。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [設定 WMI 在 SQL Server 工具中顯示伺服器狀態](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)   
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)   
 [組態函式 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [伺服器相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
