---
description: 記錄讀取器代理程式安全性
title: 記錄讀取器代理程式安全性 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.LRA.f1
helpviewer_keywords:
- Log Reader Agent Security dialog box
ms.assetid: d6981e74-ddb8-41b8-9ea1-56c2ece63b8a
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 19bd3e83dbac4222dcdb476c5d952c0773a623e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493961"
---
# <a name="log-reader-agent-security"></a>記錄讀取器代理程式安全性
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **[記錄讀取器代理程式安全性]** 對話方塊可以讓您指定：  
  
-   記錄讀取器代理程式在散發者端執行所用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 Windows 帳戶也稱為 *處理帳戶*，因為代理程式處理是在這個帳戶下執行。  
  
-   記錄讀取器代理程式連線到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者所用的內容。 可以模擬 Windows 帳戶進行連接，或者在您指定之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容下進行連接。  
  
    > [!NOTE]  
    >  即使發行者與散發者都是在同一部電腦上，記錄讀取器代理程式仍會連接到發行者。 記錄讀取器代理程式也會連接到散發者；這些連接都會模擬代理程式執行所用的 Windows 帳戶來進行。  
  
     對於 Oracle 發行者，請在 **[發行者屬性]** 對話方塊 (可以從 **[散發者屬性]** 對話方塊中存取) 中，指定記錄讀取器代理程式連接到發行者所用的內容。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## <a name="options"></a>選項。  
 **處理帳戶**  
 輸入記錄讀取器代理程式在散發者端執行所用的 Windows 帳戶。 您指定的 Windows 帳戶，至少必須是散發資料庫中之 **db_owner** 固定資料庫角色的成員。  
  
 **[密碼]** 與 **[確認密碼]**  
 輸入 Windows 帳戶的密碼。  
  
 **連接到發行者**  
 選擇記錄讀取器代理程式是否應模擬 **[處理帳戶]** 文字方塊中所指定的帳戶，還是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您選取模擬 Windows 帳戶，而非使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶至少必須是發行集資料庫內 **db_owner** 固定資料庫角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [複寫中的身分識別和存取控制 ](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [複寫安全性最佳作法](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
