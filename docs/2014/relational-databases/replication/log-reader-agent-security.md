---
title: 記錄讀取器代理程式安全性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.security.LRA.f1
helpviewer_keywords:
- Log Reader Agent Security dialog box
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c55292aff126d1955c438c9417ce0651cc6afc94
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63162249"
---
# <a name="log-reader-agent-security"></a>記錄讀取器代理程式安全性
  [**記錄讀取器代理程式安全性**] 對話方塊可讓您指定：  
  
-   記錄讀取器代理程式在散發者端執行所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 Windows 帳戶也稱為*處理帳戶*，因為代理程式進程會在此帳戶下執行。  
  
-   記錄讀取器代理程式用來連接到[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者的內容。 可以模擬 Windows 帳戶進行連接，或者在您指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容下進行連接。  
  
    > [!NOTE]  
    >  即使發行者與散發者都是在同一部電腦上，記錄讀取器代理程式仍會連接到發行者。 記錄讀取器代理程式也會連接到散發者；這些連接都會模擬代理程式執行所用的 Windows 帳戶來進行。  
  
     對於 Oracle 發行者，請在 **[發行者屬性]** 對話方塊 (可以從 **[散發者屬性]** 對話方塊中存取) 中，指定記錄讀取器代理程式連接到發行者所用的內容。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## <a name="options"></a>選項。  
 **處理帳戶**  
 輸入記錄讀取器代理程式在散發者端執行所用的 Windows 帳戶。 您指定的 Windows 帳戶，至少必須是散發資料庫中之 **db_owner** 固定資料庫角色的成員。  
  
 **密碼**和**確認密碼**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到發行者**  
 選擇記錄讀取器代理程式是否應模擬 **[處理帳戶]** 文字方塊中所指定的帳戶，還是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您選取模擬 Windows 帳戶，而非使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶至少必須是發行集資料庫內 **db_owner** 固定資料庫角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [管理複寫的登入與密碼](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [複寫代理程式安全性模型](security/replication-agent-security-model.md)   
 [複寫代理程式總覽](agents/replication-agents-overview.md)   
 [複寫安全性最佳作法](security/replication-security-best-practices.md)  
  
  
