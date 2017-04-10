---
title: "散發代理程式安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.security.DA.f1"
helpviewer_keywords: 
  - "散發代理程式安全性對話方塊"
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
caps.latest.revision: 25
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 25
---
# 散發代理程式安全性
  **[散發代理程式安全性]** 對話方塊，可以讓您指定散發代理程式執行用的 Windows 帳戶。 若為發送訂閱，散發代理程式會在散發者端執行；若為提取訂閱，則散發代理程式會在訂閱者端執行。 此 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶亦稱為 *處理帳戶*，因為代理程式處理序會以此帳戶執行。 對話方塊中其他可用的選項會視您存取的方式而定：  
  
-   如果是從新增訂閱精靈中存取對話方塊，它還可以讓您指定散發代理程式連接到訂閱者 (適用於發送訂閱) 或散發者 (適用於提取訂閱) 所用的內容。 此連接可以藉由模擬 Windows 帳戶，或是用您指定之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容來進行。  
  
-   如果對話方塊從 **訂閱屬性** 對話方塊方塊中，指定的內容散發代理程式連線依序按一下 [內容] 按鈕 (**...**) 中 **訂閱者連接** 或 **散發者連接** 該對話方塊的資料列。 如需有關存取 **訂閱屬性** 對話方塊中，請參閱 [檢視和修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ，以及如何︰ [檢視和修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## 選項  
 **處理帳戶**  
 輸入散發代理程式執行用的 Windows 帳戶：  
  
-   針對發送訂閱，帳戶必須：  
  
    -   至少為隸屬 **db_owner** 散發資料庫中的固定的資料庫角色。  
  
    -   是發行存取清單 (PAL) 的成員。  
  
    -   擁有快照集共用上的讀取權限。  
  
    -   如果訂閱是針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，訂閱者之 OLE DB 提供者的安裝目錄上，就要擁有讀取權限。  
  
-   對於提取訂閱，帳戶必須至少是屬於 **db_owner** 訂閱資料庫中的固定的資料庫角色。  
  
 如果是在進行連接時模擬處理帳戶，則需要其他的權限。 請參閱以下的＜ **連接到散發者** ＞和＜ **連接到訂閱者** ＞章節。  
  
 無法為**** 的提取訂閱指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，因為散發代理程式無法在 [!INCLUDE[ssExpress](../../includes/ssExpress-md.md)]。  
  
 **密碼** 和 **確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到散發者**  
 對於發送訂閱，連接到散發者一律會藉由模擬中指定的帳戶 **處理序帳戶** 文字方塊。  
  
 對於提取訂閱，選取散發代理程式是否應模擬 **[處理帳戶]** 文字方塊中所指定的帳戶，還是要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到散發者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  建議您選取模擬 Windows 帳戶，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶必須：  
  
-   為 PAL 的成員。  
  
-   擁有快照集共用上的讀取權限。  
  
 **連接到訂閱者**  
 對於提取訂閱，連接到訂閱者一律會藉由模擬中指定的帳戶 **處理序帳戶** 文字方塊。  
  
 對於發送訂閱，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者與非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者的選項並不相同：  
  
-   對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者：選取散發代理程式是否應模擬 **[處理帳戶]** 文字方塊中所指定的帳戶，還是要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到訂閱者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
    > [!NOTE]  
    >  建議您選取模擬 Windows 帳戶，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
     Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接到訂閱者所使用的帳戶必須至少是成員的 **db_owner** 訂閱資料庫中的固定的資料庫角色。  
  
-   對於非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，請指定當散發代理程式要連接到訂閱者時，應使用的訂閱者端之資料庫登入。 此登入應擁有在訂閱資料庫中建立物件的權限。 如需有關設定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，請參閱 [為非 SQL Server 訂閱者建立訂閱](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
 **其他連接選項**  
 僅限非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 以連接字串的格式，為訂閱者指定任何連接選項 (Oracle 並不需要其他選項)。 每個選項應以分號分隔。 以下為 IBM DB2 連接字串的範例 (分行符號僅為便於閱讀)：  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 字串中的大多數選項是您設定之 DB2 伺服器的專用選項，但 **將二進位當作字元處理** 選項，應一律設定為 [False] 。 需要為 **初始目錄** 選項指定值，以便識別訂閱資料庫。 如需相關資訊，請參閱 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)。  
  
## 另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  