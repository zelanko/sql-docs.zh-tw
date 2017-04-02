---
title: "記錄讀取器代理程式安全性 | Microsoft Docs"
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
  - "sql13.rep.security.LRA.f1"
helpviewer_keywords: 
  - "記錄讀取器代理程式安全性對話方塊"
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 記錄讀取器代理程式安全性
   **記錄讀取器代理程式安全性** 對話方塊可讓您指定︰  
  
-   記錄讀取器代理程式在散發者端執行所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 Windows 帳戶也稱為 *處理帳戶*，因為代理程式處理是在這個帳戶下執行。  
  
-   記錄讀取器代理程式連線至內容 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 可以模擬 Windows 帳戶進行連接，或者在您指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容下進行連接。  
  
    > [!NOTE]  
    >  即使發行者與散發者都是在同一部電腦上，記錄讀取器代理程式仍會連接到發行者。 記錄讀取器代理程式也會連接到散發者；這些連接都會模擬代理程式執行所用的 Windows 帳戶來進行。  
  
     Oracle 發行者，指定記錄讀取器代理程式連接到 「 發行者 」 中的內容 **發行者屬性** 對話方塊 (可從 **散發者屬性** 對話方塊)。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## 選項  
 **處理帳戶**  
 輸入記錄讀取器代理程式在散發者端執行所用的 Windows 帳戶。 Windows 帳戶，指定最小值必須是成員 **db_owner** 散發資料庫中的固定的資料庫角色。  
  
 **密碼** 和 **確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到發行者**  
 選擇是否要記錄讀取器代理程式應該藉由模擬中指定的帳戶到 「 發行者 」 中建立連線 **處理序帳戶** 文字方塊或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您選取模擬 Windows 帳戶，而不是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接所使用的帳戶必須至少是成員的 **db_owner** 發行集資料庫中的固定的資料庫角色。  
  
## 另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  