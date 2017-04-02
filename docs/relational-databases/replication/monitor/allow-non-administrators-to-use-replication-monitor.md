---
title: "允許非管理員使用複寫監視器 | Microsoft Docs"
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
  - "複寫監視器, 非管理員存取"
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 允許非管理員使用複寫監視器
  本主題描述如何允許非管理員藉由使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中使用複寫監視器。 「複寫監視器」可供身為下列角色成員的使用者使用：  
  
-   **系統管理員 (sysadmin)** 固定伺服器角色。  
  
     這些使用者可監視複寫，並且擁有變更複寫屬性的完全控制，例如，代理程式排程、代理程式設定檔等。  
  
-   散發資料庫中的 **replmonitor** 資料庫角色。  
  
     這些使用者可監視複寫，但無法變更任何複寫屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要允許非管理員使用複寫監視器，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 若要允許非系統管理員使用複寫監視器] 的成員 **sysadmin** 固定的伺服器角色必須將使用者新增到散發資料庫，並指派給該使用者以 **replmonitor** 角色。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 允許非管理員使用複寫監視器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中連接到散發者，然後展開伺服器節點。  
  
2.  展開 **資料庫**, ，依序展開 **系統資料庫**, ，然後展開 [散發資料庫 (名為 **發佈** 預設情況下)。  
  
3.  展開 **安全性**, ，以滑鼠右鍵按一下 **使用者**, ，然後按一下 [ **新使用者**。  
  
4.  輸入使用者名稱及使用者的登入。  
  
5.  選取 **[replmonitor]**的預設結構描述。  
  
6.  在 **[資料庫角色成員資格]** 方格中選取 **[replmonitor]** 。  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要將使用者加入至 replmonitor 固定資料庫角色  
  
1.  在散發資料庫的散發者端，執行 [sp_helpuser & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)。 如果使用者未列在 **UserName** 結果集中，使用者必須被授與存取散發資料庫使用 [建立使用者 & #40。TRANSACT-SQL & #41;](../../../t-sql/statements/create-user-transact-sql.md) 陳述式。  
  
2.  在散發資料庫的散發者端，執行 [sp_helprolemember & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), ，指定的值為 **replmonitor** 的 **@rolename** 參數。 如果使用者列於結果集中的 **MemberName** ，則該使用者已屬於此角色。  
  
3.  如果使用者不屬於 **replmonitor** 角色、 執行 [sp_addrolemember & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) 在散發資料庫的散發者端。 針對 **replmonitor** @rolename **@rolename** 的值，並指定資料庫使用者的名稱或針對 [!INCLUDE[msCoName](。。/Token/msCoName_md。md)] Windows login being added @rolename **所加入的**。  
  
#### 若要從 replmonitor 固定資料庫角色移除使用者  
  
1.  若要確認使用者屬於 **replmonitor** 角色、 執行 [sp_helprolemember & #40;TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) 在散發資料庫中，「 散發者和指定的值為 **replmonitor** 的 **@rolename**。 如果使用者未列於結果集中的 **MemberName** ，則該使用者目前不屬於此角色。  
  
2.  如果使用者確實屬於 **replmonitor** 角色、 執行 [sp_droprolemember & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) 在散發資料庫的散發者端。 針對 **@rolename** 指定 **replmonitor** 的值，並指定資料庫使用者的名稱或針對 **@membername**所移除的 Windows 登入。  
  
  