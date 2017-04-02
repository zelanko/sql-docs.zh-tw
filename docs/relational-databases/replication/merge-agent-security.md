---
title: "合併代理程式安全性 | Microsoft Docs"
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
  - "sql13.rep.security.MA.f1"
helpviewer_keywords: 
  - "合併代理程式安全性對話方塊"
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 合併代理程式安全性
  **[合併代理程式安全性]** 對話方塊可讓您指定執行合併代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 合併代理程式會在發送訂閱的散發者端和提取訂閱的訂閱者端執行。 Windows 帳戶也稱為 *處理帳戶*，因為代理程式處理是在這個帳戶下執行。 對話方塊中其他可用的選項會視您存取的方式而定：  
  
-   如果從新增訂閱精靈存取此對話方塊，就也可以指定合併代理程式用於連接到訂閱者 (適用於發送訂閱) 或發行者和散發者 (適用於提取訂閱) 的內容。 可以使用 Windows 帳戶或在您指定之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容之下建立連接。  
  
-   如果對話方塊從 **訂閱屬性** 對話方塊方塊中，指定的內容合併代理程式連線依序按一下 [內容] 按鈕 (**...**) 中 **訂閱者連接** 或 **發行者連接** 該對話方塊的資料列。 如需有關存取 **訂閱屬性** 對話方塊中，請參閱 [檢視和修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) ，以及如何︰ [檢視和修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## 選項  
 **處理帳戶**  
 輸入要在其下執行合併代理程式的 Windows 帳戶。  
  
-   針對發送訂閱，帳戶必須：  
  
    -   至少為隸屬 **db_owner** 散發資料庫中的固定的資料庫角色。  
  
    -   為 PAL 的成員。  
  
    -   為與發行集資料庫中使用者相關聯的登入。  
  
    -   擁有快照集共用上的讀取權限。  
  
-   對於提取訂閱，帳戶必須至少是屬於 **db_owner** 訂閱資料庫中的固定的資料庫角色。  
  
 如果是在進行連接時模擬處理帳戶，則需要其他的權限。 請參閱下面的 **[連接到發行者與散發者]** 和 **[連接到訂閱者]** 章節。  
  
 **處理序帳戶** 的提取訂閱不能指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], ，因為合併代理程式不會執行的執行個體上 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]。  
  
 **密碼** 和 **確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到發行者與散發者**  
 對於發送訂閱，連接到發行者與散發者一律會藉由模擬中指定的帳戶 **處理序帳戶** 文字方塊。  
  
 針對提取訂閱，選取合併代理程式是否應藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者與散發者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您選取模擬 Windows 帳戶，而不是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶必須：  
  
-   為 PAL 的成員。  
  
-   為與發行集資料庫中使用者相關聯的登入。  
  
-   為與散發資料庫中之使用者相關聯的登入 (使用者可為 Guest 使用者)。  
  
-   擁有快照集共用上的讀取權限。  
  
 **連接到訂閱者**  
 對於提取訂閱，連接到訂閱者一律會藉由模擬中指定的帳戶 **處理序帳戶** 文字方塊。  
  
 針對發送訂閱，選取合併代理程式是否應藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者與散發者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  建議您選取模擬 Windows 帳戶，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接到訂閱者所使用的帳戶必須至少是成員的 **db_owner** 訂閱資料庫中的固定的資料庫角色。  
  
## 另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  