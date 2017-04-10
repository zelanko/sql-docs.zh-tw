---
title: "快照集代理程式安全性 | Microsoft Docs"
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
  - "sql13.rep.security.SSA.f1"
helpviewer_keywords: 
  - "快照集代理程式安全性對話方塊"
ms.assetid: 64e84c67-acc6-4906-98d4-3451767363fe
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 快照集代理程式安全性
   **快照集代理程式安全性** 對話方塊可讓您指定︰  
  
-   在散發者端執行快照集代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 Windows 帳戶也稱為 *處理帳戶*，因為代理程式處理是在這個帳戶下執行。  
  
-   快照集代理程式連線至內容 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 可以模擬 Windows 帳戶進行連接，或者在您指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容下進行連接。  
  
    > [!NOTE]  
    >  即使發行者和散發者不在同一部電腦上，快照集代理程式也會連接到發行者。 快照集代理程式也會連接到散發者；這些連接一律會藉由模擬執行代理程式的 Windows 帳戶來進行。  
  
     Oracle 發行者指定快照集代理程式連接到 「 發行者 」 中的內容 **發行者屬性** 對話方塊 (可從 **散發者屬性** 對話方塊)。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## 選項  
 **處理帳戶**  
 輸入在散發者端執行快照集代理程式的 Windows 帳戶。 您指定的 Windows 帳戶必須：  
  
-   至少為隸屬 **db_owner** 散發資料庫中的固定的資料庫角色。  
  
-   擁有快照集共用上的寫入權限。  
  
 **密碼** 和 **確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到發行者**  
 選取快照集代理程式要連接到 「 發行者 」 藉由模擬中指定的帳戶是否 **處理序帳戶** 文字方塊或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  建議您選取模擬 Windows 帳戶，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接所使用的帳戶必須至少是成員的 **db_owner** 發行集資料庫中的固定的資料庫角色。  
  
## 另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  