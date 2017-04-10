---
title: "佇列讀取器代理程式安全性 | Microsoft Docs"
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
  - "sql13.rep.security.QRA.f1"
helpviewer_keywords: 
  - "佇列讀取器代理程式安全性對話方塊"
ms.assetid: 77938da0-2afd-4455-8826-f4a6a9440cb3
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 佇列讀取器代理程式安全性
   **佇列讀取器代理程式安全性** 對話方塊可讓您指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 佇列讀取器代理程式執行和進行本機連接到 「 散發者 」 的 Windows 帳戶。 代理程式連接到 「 發行者 」 使用指定的帳戶 **發行者屬性** 對話方塊 (可從 **散發者屬性** 對話方塊); 代理程式連接到 「 訂閱者 」 與 「 散發代理程式使用相同的內容，訂用帳戶。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 帳戶必須有效，並且要指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## 選項  
 **處理帳戶**  
 輸入在散發者端執行佇列讀取器代理程式的 Windows 帳戶。 Windows 帳戶，指定最小值必須是成員 **db_owner** 散發資料庫中的固定的資料庫角色。  
  
 **密碼** 和 **確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
## 另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  