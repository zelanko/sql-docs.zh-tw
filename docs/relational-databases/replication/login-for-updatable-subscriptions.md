---
title: "可更新訂閱的登入 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# 可更新訂閱的登入
  立即更新時，如果您選取 **複寫** 上 **可更新訂閱** 頁面的此精靈中，您必須指定帳戶與訂閱者連接到 「 發行者 」 進行。 
  
 在 「 訂閱者 」 引發，並將變更傳播到 「 發行者 」 端的觸發程序會使用連接。 即使您已選取，就需要此帳戶 **佇列變更且儘可能認可** 上 **可更新訂閱** 頁面。 新增訂閱精靈 」，依預設會設定佇列更新切換到立即更新，如有必要的功能。  
  
> **重要！！** 指定應該只是連線的帳戶授與權限來插入、 更新和刪除檢視表上的資料複寫建立發行集資料庫中。 它應該不會提供任何額外的權限。 授與權限檢視表單中名為發行集資料庫中的 **syncobj_***\< HexadecimalNumber>* 您設定每個訂閱者端的帳戶。  
  
 此連接類型有三個選項可用：  
  
-   您已定義的連結伺服器或遠端伺服器。  
  
-   複寫建立的連結伺服器；以您在此精靈中指定的認證來建立連接。  
  
-   複寫建立的連結伺服器；以在訂閱者端執行變更的使用者認證來建立連接。  
  
 此精靈中可以指定前兩個選項。 最後一個選項只能指定使用 [sp_link_publication & #40。TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md);指定的值為 **1** 參數 **@security_mode**。  
  
## 選項。  
 **建立使用下列 SQL Server 驗證登入進行連接的連結伺服器：**  
 複寫會建立連結的伺服器使用的認證中指定 **登入** 和 **密碼** 欄位。  
  
 **登入**  
 輸入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有此主題中所述的權限的登入。  
  
 **密碼**  
 在指定的登入輸入增強式密碼 **登入**。  
    
 **使用您已定義的連結伺服器或遠端伺服器。**  
 此選項需要您已定義的連結伺服器或遠端伺服器。 如需詳細資訊，請參閱 [連結的伺服器 #40，Database Engine &#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) 和 [遠端伺服器](../../database-engine/configure-windows/remote-servers.md)。 請確定連結伺服器或遠端伺服器使用的登入具有增強式密碼，且只具有此主題所描述的權限。  
  
## 另請參閱  
 [建立交易式發行集的可更新訂閱](https://msdn.microsoft.com/library/ms152769.aspx)   
 [檢視及修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  