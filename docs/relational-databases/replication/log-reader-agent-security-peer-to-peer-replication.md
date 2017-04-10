---
title: "記錄讀取器代理程式安全性 (點對點複寫) | Microsoft Docs"
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
  - "sql13.rep.p2pwizard.LRA.f1"
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# 記錄讀取器代理程式安全性 (點對點複寫)
   **記錄讀取器代理程式安全性** 頁面可讓您指定的每一個對等 「 記錄讀取器代理程式執行和連接的帳戶。 代理程式和複寫安全性的最佳做法所需的權限的資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md) 和 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  每一個使用異動複寫發行的資料庫都有一個記錄讀取器代理程式。 如果資料庫的記錄讀取器代理程式已經完成設定 (此精靈前一次執行中的發行集，或相同資料庫中的其他交易式發行集)，則無法變更它在此精靈中使用的認證。 如果您指定新認證，將會忽略這些認證。 若要變更認證，請使用 **發行集屬性** 對話方塊。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## 選項  
 按一下屬性按鈕 (**...**) 來存取每個對等的資料列中 **記錄讀取器代理程式安全性** 對話方塊。 按一下 [ **協助** 上 **記錄讀取器代理程式安全性** 啟動的代理程式所使用的帳戶所需的權限的詳細資訊] 對話方塊。  
  
 在對話方塊中輸入設定之後，訂閱者的連接資訊會在方格中顯示。  
  
 **發行者的代理程式**  
 每個對等 (Peer) 伺服器執行個體的名稱。  
  
 **對等 (Peer) 資料庫**  
 在每個對等 (Peer) 端作為發行集資料庫和訂閱資料庫的資料庫。  
  
 **散發者的連接**  
 用於連接到散發者的內容。 本機連接到散發者一定會使用的內容 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶執行代理程式，所以此欄位一律會顯示 **模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。  
  
 **發行者的連接**  
 用於連接到發行者的內容。 連接到 「 發行者 」 可使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或使用執行代理程式的 Windows 帳戶的內容。 欄位會顯示下列其中之一︰ **使用登入 '\< 登入>'**, ，**模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用 Windows 帳戶的內容進行所有連接的建議。  
  
## 另請參閱  
 [管理等式拓樸 & #40。複寫 TRANSACT-SQL 程式設計 & #41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [點對點異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  