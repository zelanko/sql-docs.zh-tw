---
title: "&lt;AgentName&gt; 代理程式安全性 | Microsoft Docs"
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
  - "sql13.rep.newsubwizard.agentnameagentsecurity.f1"
ms.assetid: d34c7ef8-cf77-4ffd-887f-3c4214dfd71e
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# &lt;AgentName&gt; 代理程式安全性
   **\< AgentName> 代理程式安全性** 頁面可讓您指定的帳戶 （適用於交易式和快照式複寫） 的散發代理程式 」 或 「 合併代理程式 （適用於合併式複寫） 執行並連接到電腦中複寫拓樸。 代理程式和複寫安全性的最佳做法所需的權限的資訊，請參閱 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md) 和 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
## 選項  
 按一下屬性按鈕 (**...**) 來存取每一個訂閱者資料列中 **散發代理程式安全性** 或 **合併代理程式安全性** 對話方塊。 按一下 [ **協助** 在對話方塊中啟動的代理程式所使用的帳戶所需的權限的詳細資訊。  
  
 在其中的一個對話方塊中輸入設定之後，訂閱者的連接資訊就會在方格中顯示。  
  
 **訂閱者的代理程式**  
 每個訂閱者的名稱。  
  
 **散發者的連接**  
 這會針對交易式與快照式複寫顯示。 用於連接到散發者的內容。 本機連接一律會使用執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的內容來進行：  
  
-   對於發送訂閱，本機連接會連接到散發者上，所以此欄位一律會顯示︰ **模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'** 發送訂閱。  
  
-   對於提取訂閱，連接可以同樣的內容下 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 欄位會顯示下列其中之一︰ **使用登入 '\< 登入>'**, ，**模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用 Windows 帳戶的內容進行所有連接的建議。  
  
 **發行者和散發者的連接**  
 這會針對合併複寫顯示。 連接到發行者與散發者所使用的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容進行連接：  
  
-   對於發送訂閱，本機連接會連接到 「 發行者 」 與 「 散發者 」，所以此欄位一律會顯示︰ **模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'** 發送訂閱。  
  
-   對於提取訂閱，連接也可以用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列其中之一︰ **使用登入 '\< 登入>'**, ，**模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用 Windows 帳戶的內容進行所有連接的建議。  
  
 **訂閱者的連接**  
 與訂閱者進行連接的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容進行連接：  
  
-   對於提取訂閱，本機連接會連接到 「 訂閱者 」，所以此欄位一律會顯示︰ **模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'** 發送訂閱。  
  
-   對於發送訂閱，連接也可以用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列其中之一︰ **使用登入 '\< 登入>'**, ，**模擬 '\< 網域>\\< 登入\>'** 或 **模擬 '\< 電腦>\\< 登入\>'**。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 使用 Windows 帳戶的內容進行所有連接的建議。  
  
## 另請參閱  
 [檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [View and Modify Push Subscription Properties](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [安全性和保護 & #40。複寫 & #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  