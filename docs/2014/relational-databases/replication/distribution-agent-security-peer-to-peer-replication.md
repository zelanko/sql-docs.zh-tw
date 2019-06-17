---
title: 散發代理程式安全性 (點對點複寫) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.DA.f1
ms.assetid: def6bf26-c640-4caf-ad30-05d1e649541d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78d8baed7783459db79bb9facb0141cc570c4127
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721377"
---
# <a name="distribution-agent-security-peer-to-peer-replication"></a>散發代理程式安全性 (點對點複寫)
  **[散發代理程式安全性]** 頁面，可以讓您指定執行散發代理程式的帳戶，並以點對點拓墣的方式連接到電腦。 如需代理程式所需權限和複寫安全性最佳做法的資訊，請參閱[複寫代理程式安全性模型](security/replication-agent-security-model.md)和[複寫安全性最佳做法](security/replication-security-best-practices.md)。  
  
> [!NOTE]  
>  如果在上一回執行此精靈時，已為訂閱設定散發代理程式，您就無法變更其在此精靈中使用的認證。 如果您指定新認證，將會忽略這些認證。 若要變更認證，請使用 **[訂閱屬性]** 對話方塊。 如需詳細資訊，請參閱 [View and Modify Replication Security Settings](security/view-and-modify-replication-security-settings.md)。  
  
## <a name="options"></a>選項。  
 按一下每個訂閱者之資料列中的屬性按鈕 ( **...** )，即可存取 **[散發代理程式安全性]** 對話方塊。 如需有關代理程式使用之帳戶所需權限的詳細資訊，請按一下 **[散發代理程式安全性]** 對話方塊上的 **[說明]** 。  
  
 在其中的一個對話方塊中輸入設定之後，訂閱者的連接資訊就會在方格中顯示。  
  
 **訂閱者的代理程式**  
 每個對等 (Peer) 的名稱。  
  
 **對等 (Peer) 資料庫**  
 對等 (Peer) 端的資料庫，會同時作為發行集資料庫與訂閱資料庫。  
  
 **散發者的連接**  
 用於連接到散發者的內容。 本機連接一律會使用執行代理程式之 Windows 帳戶的內容來進行。 此精靈會建立發送訂閱 （本機連接會連接到散發者 」），所以此欄位一律會顯示：**模擬 '\<網域 >\\< 登入\>'** 或是**模擬 '\<電腦 >\\< 登入\>'** 。  
  
 **訂閱者的連接**  
 與訂閱者進行連接的內容。 連接可以使用執行代理程式之 Windows 帳戶的內容，或使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入的內容來進行。 欄位會顯示下列其中一項：[使用登入 '\<登入>']  、[模擬 '\<網域>\\<登入\>']  或 [模擬 '\<電腦>\\<登入\>']  。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 建議使用 Windows 帳戶的內容進行所有連接。  
  
## <a name="see-also"></a>另請參閱  
 [管理點對點拓撲 &#40;複寫 Transact-SQL 程式設計&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [@loopback_detection](transactional/peer-to-peer-transactional-replication.md)  
  
  
