---
title: "設定 remote query timeout 伺服器組態選項 | Microsoft Docs"
ms.custom: ""
ms.date: "03/08/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "遠端查詢的時間限制 [SQL Server]"
  - "remote query timeout 選項"
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
caps.latest.revision: 26
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# 設定 remote query timeout 伺服器組態選項
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] remote query timeout [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **remote query timeout** 選項會指定在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 逾時之前，遠端作業可以執行多久 (以秒為單位)。 此選項的預設值是 600，這允許 10 分鐘的等待。 此值可套用到由 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 啟始做為遠端查詢的傳出連接。 此值對 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 收到的查詢沒有影響。 若要停用逾時，請將值設定為 0。 查詢會等候，直到被取消。  
  
 對於異質性查詢，[遠端查詢逾時] 可指定遠端提供者在等候查詢結果集時，應等候幾秒 (使用 DBPROP_COMMANDTIMEOUT 資料列集屬性在命令物件中初始化) 後，查詢才會逾時。 這個值也用來設定 DBPROP_GENERALTIMEOUT (如果遠端提供者支援的話)。 這會使其他任何作業在指定秒數後變逾時。  
  
 對於遠端預存程序， **remote query timeout** 會指定在傳送遠端 `EXEC` 陳述式之後，遠端預存程序逾時之前必須經過的秒數。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 remote query timeout 選項：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 remote query timeout 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   設定這個數值之前必須先允許遠端伺服器連接。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 依預設，所有使用者都會取得不含參數或只含第一個參數之 **sp_configure** 的執行權限。 若要執行同時設定了兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 設定 remote query timeout 選項  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[連接]** 節點。  
  
3.  請在 **[遠端伺服器連接]**下方的 **[遠端查詢逾時]** 方塊中，輸入或選取從 0 至 2,147,483,647 的值，以設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在逾時之前要等待的最大秒數。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 設定 remote query timeout 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 將 `remote query timeout` 選項的值設定為 `0`，以停用逾時。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 如需詳細資訊，請參閱[伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)。  
  
##  <a name="FollowUp"></a> 待處理：設定 remote query timeout 選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## 另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [資料列集屬性和行為](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  