---
title: "記錄讀取器代理程式安全性 (點對點複寫) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.p2pwizard.LRA.f1
ms.assetid: 6575e2a8-16bb-449c-bdca-4a4202d0972f
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7b670e48c6859dfaad38b9383fb3e2056fa47994
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="log-reader-agent-security-peer-to-peer-replication"></a>記錄讀取器代理程式安全性 (點對點複寫)
  **[記錄讀取器代理程式安全性]** 頁面，可讓您指定記錄讀取器代理程式在每個對等 (Peer) 端執行和連接的帳戶。 如需代理程式所需權限和複寫安全性的最佳做法的詳細資訊，請參閱[複寫代理程式安全性模型](../../relational-databases/replication/security/replication-agent-security-model.md)和[複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  每一個使用異動複寫發行的資料庫都有一個記錄讀取器代理程式。 如果資料庫的記錄讀取器代理程式已經完成設定 (此精靈前一次執行中的發行集，或相同資料庫中的其他交易式發行集)，則無法變更它在此精靈中使用的認證。 如果您指定新認證，將會忽略這些認證。 若要變更認證，請使用 **[發行集屬性]** 對話方塊。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)。  
  
## <a name="options"></a>選項。  
 在每個對等 (Peer) 的資料列中按一下屬性按鈕 (**...**)，即可存取 **[記錄讀取器代理程式安全性]** 對話方塊。 在啟動的 **[記錄讀取器代理程式安全性]** 對話方塊上按一下 **[說明]** ，以取得代理程式使用的帳戶所需之權限的詳細資訊。  
  
 在對話方塊中輸入設定之後，訂閱者的連接資訊會在方格中顯示。  
  
 **發行者的代理程式**  
 每個對等 (Peer) 伺服器執行個體的名稱。  
  
 **對等 (Peer) 資料庫**  
 在每個對等 (Peer) 端作為發行集資料庫和訂閱資料庫的資料庫。  
  
 **散發者的連接**  
 用於連接到散發者的內容。 散發者的本機連接一律會使用執行代理程式之 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帳戶的內容進行，所以這個欄位一律顯示 [模擬 '\<網域>\\<登入\>'] 或 [模擬 '\<電腦>\\<登入\>']。  
  
 **發行者的連接**  
 用於連接到發行者的內容。 發行者的連接可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入，或使用執行代理程式之 Windows 帳戶的內容進行。 欄位會顯示下列內容之一：[使用者登入 '\<登入>']、[模擬 '\<網域>\\<登入\>'] 或 [模擬 '\<電腦>\\<登入\>']。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議使用 Windows 帳戶的內容進行所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [點對點異動複寫](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
