---
title: "發行集屬性，代理程式安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.agentsecurity.f1"
ms.assetid: 03945aac-66f2-4370-b5d1-c1de694bc4c1
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 發行集屬性，代理程式安全性
  **[發行集屬性]** 對話方塊的 **[代理程式安全性]** 頁面，可以讓您存取執行下列代理程式的帳戶設定，並與複寫拓撲中的電腦建立連接：  
  
-   所有發行集的快照集代理程式。  
  
-   所有交易式發行集的記錄讀取器代理程式。 每個為異動複寫發行的資料庫，都會有一個記錄讀取器代理程式。 變更記錄讀取器代理程式會影響資料庫中的所有交易式發行集。  
  
-   允許佇列更新訂閱之交易式發行集的佇列讀取器代理程式。 每個散發資料庫都會有一個佇列讀取器代理程式。 變更佇列讀取器代理程式的設定，會影響使用相同散發資料庫之具有佇列更新訂閱的交易式發行集。 如需有關佇列讀取器代理程式安全性設定的詳細資訊，請參閱 [檢視和修改複寫安全性設定](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 如需有關每一個代理程式所需的安全性設定和權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
## 選項  
 **安全性設定** 或 **建立代理程式**  
 如果尚未建立代理程式作業，按一下 [ **安全性設定** 存取對話方塊，可讓您變更代理程式的安全性設定。 如果尚未建立代理程式作業，請按一下 **[建立代理程式]** ，即可建立代理程式並指定安全性設定。  
  
## 另請參閱  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全性和保護 & #40。複寫 & #41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  