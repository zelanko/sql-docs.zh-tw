---
title: "連接到伺服器 (Oracle)，登入 | Microsoft Docs"
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
  - "sql13.rep.oracleconnection.login.f1"
helpviewer_keywords: 
  - "[連接到伺服器] 對話方塊, 複寫"
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 連接到伺服器 (Oracle)，登入
  使用 **登入** ] 索引標籤的 **連接到伺服器** ] 對話方塊中，指定帳戶的連接建立從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到 Oracle 發行者的散發者。 您必須使用在發行者組態期間，為複寫管理的使用者結構描述指定之相同帳戶。 如需詳細資訊，請參閱 [設定 Oracle 發行者](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
## 選項  
 **伺服器執行個體**  
 Oracle 發行者的透明網路基質 (Transparent Network Substrate，TNS) 名稱，是安裝在散發者上的 Oracle 用戶端軟體於組態期間指定的。  
  
 **驗證**  
 選取 **Oracle 標準驗證** （建議） 或 **Windows 驗證**。 如果您選取 **Windows 驗證**:  
  
-   Oracle 伺服器必須設定為允許使用 Windows 認證進行連接。 如需詳細資訊，請參閱 Oracle 文件集。  
  
-   您目前必須是使用與複寫管理的使用者結構描述所指定的相同 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶登入的。  
  
 **登入** 和 **密碼**  
 如果您選取 **Oracle 標準驗證** 的 **驗證** 選項，請指定登入和密碼，才能使用，它必須與所指定的複寫管理使用者結構描述相同。  
  
## 另請參閱  
 [Oracle 發行相關術語字彙](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  