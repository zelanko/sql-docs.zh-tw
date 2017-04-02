---
title: "設定 scan for startup procs 伺服器組態選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "scan for startup procs 選項"
ms.assetid: 6bf9d252-e766-458d-9dcd-23d895f032a2
caps.latest.revision: 27
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 27
---
# 設定 scan for startup procs 伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] scan for startup procs [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 您可以使用 **scan for startup procs** 選項，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動期間掃描預存程序的自動執行。 如果這個選項設定為 1，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會掃描及執行伺服器上所定義的所有自動執行預存程序。 **掃描啟動程序**的預設值是 0 (不掃描)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 scan for startup procs 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 scan for startup procs 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   您可以使用 **sp_configure** 來設定這個選項的值；然而如果您使用 **sp_procoption** (用以標示或取消標示自動執行的預存程序)，這個選項的值就會自動設定。 當 **sp_procoption** 用來將第一個預存程序標示為 autoproc 時，這個選項會自動設定為值 1。 當 **sp_procoption** 用來將最後一個預存程序取消標示 autoproc 時，這個選項會自動設定為值 0。 如果您使用 **sp_procoption** 標示和取消標示 autoproc，而且固定在捨棄 autoproc 之前取消其標示，則不需要手動設定這個選項。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 依預設，所有使用者都會取得不含參數或只含第一個參數之 **sp_configure** 的執行權限。 若要執行同時設定了兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要設定 scan for startup procs 選項  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 [其他] 下方，從下拉式清單方塊中選取所需的值，將 [掃描啟動程序] 選項的值變更為 True 或 False。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要設定 scan for startup procs 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 將 `scan for startup procs` 選項的值設定為 `1`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'scan for startup procs', 1 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
##  <a name="FollowUp"></a> 待處理：設定 scan for startup procs 選項之後  
 伺服器必須重新啟動之後，設定才能生效。  
  
## 另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_procoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)  
  
  