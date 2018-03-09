---
title: "合併代理程式安全性 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.security.MA.f1
helpviewer_keywords: Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d6f95cce617a490f37f4f8171ebf0e67e1d781d5
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="merge-agent-security"></a>合併代理程式安全性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [合併代理程式安全性] 對話方塊可讓您指定執行合併代理程式的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶。 合併代理程式會在發送訂閱的散發者端和提取訂閱的訂閱者端執行。 Windows 帳戶也稱為 *處理帳戶*，因為代理程式處理是在這個帳戶下執行。 對話方塊中其他可用的選項會視您存取的方式而定：  
  
-   如果從新增訂閱精靈存取此對話方塊，就也可以指定合併代理程式用於連接到訂閱者 (適用於發送訂閱) 或發行者和散發者 (適用於提取訂閱) 的內容。 可以使用 Windows 帳戶或在您指定之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶的內容之下建立連接。  
  
-   如果從 **[訂閱屬性]** 對話方塊存取此對話方塊，請按一下該對話方塊的**[訂閱者連接]**或 **[發行者連接]** 資料列中的屬性按鈕 ( **...** )，來指定合併代理程式要在其下建立連接的內容。 如需存取 [訂閱屬性] 對話方塊的詳細資訊，請參閱[檢視及修改發送訂閱屬性](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)[檢視及修改提取訂閱屬性](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
 所有帳戶都必須有效，並且每個帳戶皆有指定正確的密碼。 等到代理程式執行時，才會驗證帳戶與密碼。  
  
## <a name="options"></a>選項。  
 **Process Account**  
 輸入要在其下執行合併代理程式的 Windows 帳戶。  
  
-   針對發送訂閱，帳戶必須：  
  
    -   至少是散發資料庫中 **db_owner** 固定資料庫角色的成員。  
  
    -   為 PAL 的成員。  
  
    -   為與發行集資料庫中使用者相關聯的登入。  
  
    -   擁有快照集共用上的讀取權限。  
  
-   針對提取訂閱，帳戶至少必須是訂閱資料庫中之 **db_owner** 固定資料庫角色的成員。  
  
 如果是在進行連接時模擬處理帳戶，則需要其他的權限。 請參閱下面的 **[連接到發行者與散發者]** 和 **[連接到訂閱者]** 章節。  
  
 **Process Account** 不可以指定發送訂閱至 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]，因為合併代理程式無法在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]＞。  
  
 **[密碼]** 與 **[確認密碼]**  
 輸入 Windows 帳戶的密碼。  
  
 **[連接到發行者與散發者]**  
 針對發送訂閱，一律會藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶，來連接到發行者與散發者。  
  
 針對提取訂閱，選取合併代理程式是否應藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者與散發者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議您選取模擬 Windows 帳戶，而非使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶必須：  
  
-   為 PAL 的成員。  
  
-   為與發行集資料庫中使用者相關聯的登入。  
  
-   為與散發資料庫中之使用者相關聯的登入 (使用者可為 Guest 使用者)。  
  
-   擁有快照集共用上的讀取權限。  
  
 **連接到訂閱者**  
 針對提取訂閱，一律會藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶連接到訂閱者。  
  
 針對發送訂閱，選取合併代理程式是否應藉由模擬 **[處理帳戶]** 文字方塊中指定的帳戶或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，來連接到發行者與散發者。 如果您選取使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入和密碼。  
  
> [!NOTE]  
>  建議您選取模擬 Windows 帳戶，而不要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶。  
  
 用於連接到訂閱者的 Windows 帳戶或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 帳戶至少必須是訂閱資料庫中之 **db_owner** 固定資料庫角色的成員。  
  
## <a name="see-also"></a>另請參閱  
 [管理複寫的登入與密碼](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [複寫代理程式概觀](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
