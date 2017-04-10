---
title: "管理發行集存取清單中的登入 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "登入 [SQL Server 複寫], 發行集存取清單"
  - "發行集 [SQL Server 複寫], 發行集存取清單"
  - "發行集存取清單 (PAL)"
  - "PAL (publication access list)"
  - "登入 [SQL Server 複寫], 管理"
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 管理發行集存取清單中的登入
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中管理發行集存取清單內的登入。 發行集的存取是由發行集存取清單 (PAL) 所控制。 可以從 PAL 中加入及移除登入和群組。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [必要條件](#Prerequisites)  
  
-   **若要管理發行集存取清單中的登入，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   您必須先將 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登入與發行集資料庫中的資料庫使用者產生關聯，才能將該登入加入 PAL 中。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 您可以使用發行集存取清單 (PAL) 上 **發行集存取清單** 頁面 **發行集屬性-\< 發行集>** 管理登入] 對話方塊。 如需如何存取此對話方塊的詳細資訊，請參閱 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 若要在 PAL 中管理登入  
  
1.  在 **發行集存取清單** 頁面 **發行集屬性-\< 發行集>** 對話方塊中，使用 **新增**, ，**移除**, ，和 **全部移除** 按鈕來加入和移除 PAL 中登入和群組。 請勿移除 **distributor_admin** 從 PAL。 此帳戶由複寫使用。  
  
    > [!NOTE]  
    >  如果使用遠端散發者，則 PAL 中的帳戶在發行者和散發者兩端都必須是可以使用的。 該帳戶必須是在兩部伺服器都已定義的網域帳戶或本機帳戶。 與兩個登入相關聯的密碼必須是一樣的。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 檢視屬於 PAL 的群組和登入  
  
1.  在發行集資料庫的發行者，執行 [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)。 針對 **@publication**指定發行集名稱。 這樣會顯示有關 PAL 中群組和登入的資訊。  
  
#### 將群組和登入加入 PAL  
  
1.  在發行集資料庫的發行者，執行 [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)。 針對 **@publication**指定發行集名稱，並針對 **@login**指定加入的登入或群組名稱。  
  
#### 從 PAL 中移除群組和登入  
  
1.  在發行集資料庫的發行者，執行 [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)。 針對 **@publication**指定發行集名稱，並針對 **@login**指定移除的登入或群組名稱。  
  
## 另請參閱  
 [Manage Logins in the Publication Access List](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [保護複寫拓撲的安全性](../../../relational-databases/replication/security/secure-a-replication-topology.md)   
 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  