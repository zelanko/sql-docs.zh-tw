---
title: "第 3 課：設定散發 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e582c5fb7853c69a083755a944bd3922d0d4c5af
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-3-configuring-distribution"></a>第 3 課：設定散發
在這一課，您將在「發行集」端設定散發，並在發行集和散發資料庫上設定所需權限。 如果您已經設定「散發者」，則必須先停用發行和散發，再開始進行本課。 如果您必須保留現有的複寫拓撲，請勿執行上述動作。  
  
利用遠端「散發者」設定「發行者」已超出本教學課程的範圍之外。  
  
### <a name="configuring-distribution-at-the-publisher"></a>在發行者端設定散發  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  以滑鼠右鍵按一下 **[複寫]** 資料夾，然後按一下 **[設定散發]**。  
  
    > [!NOTE]  
    > 如果您是使用 **localhost** 而非實際伺服器名稱連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，系統會以警告提示您 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法連接到伺服器 **'localhost'**。 在警告對話方塊中按一下 **[確定]**。 在 **[連接到伺服器]** 對話方塊中，將 **[伺服器名稱]** 從 **localhost** 變更為伺服器的名稱。 按一下 **[連接]**。  
  
    [散發組態精靈] 隨即啟動。  
  
3.  在 **[散發者]** 頁面上，選取 ['<伺服器名稱>' 將扮演本身的散發者; SQL Server 將建立散發資料庫和記錄]，然後按一下 **[下一步]**。  
  
4.  如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 未執行，請在 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**Agent 啟動]** 頁面上選取 **[是]**，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務設定為自動啟動。 按一下 **[下一步]**。  
  
5.  在 **[快照集資料夾]** 文字方塊中，輸入 **\\\\**\<*電腦名稱>***\repldata**，其中 \<*電腦名稱>* 是「發行者」的名稱，然後按一下 **[下一步]**。  
  
6.  接受精靈其餘頁面上的預設值。  
  
7.  按一下 **[完成]**，以啟用散發。  
  
### <a name="setting-database-permissions-at-the-publisher"></a>在發行者端設定資料庫權限  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中展開 **[安全性]**，並以滑鼠右鍵按一下 **[登入]**，然後選取 **[新增登入]**。  
  
2.  在 **[一般]** 頁面上，按一下 **[搜尋]**，並在 **[輸入要選取的物件名稱]** 方塊中輸入 \<*電腦名稱>***\repl_snapshot** (其中 \<*電腦名稱>* 是本機「發行者」伺服器的名稱)，按一下 **[檢查名稱]**，然後按一下 **[確定]**。  
  
3.  在 **[使用者對應]** 頁面上，從 **[已對應到此登入的使用者]** 清單中選取 **distribution** 和 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 這兩個資料庫。  
  
    在 **[資料庫角色成員資格]** 清單中，選取 **[db_owner]** 角色由這兩個資料庫的登入擔任。  
  
4.  按一下 **[確定]**，以建立登入。  
  
5.  重複執行步驟 1-4，以建立本機 repl_logreader 帳戶的登入。 此登入也必須對應至 **distribution** 和 **AdventureWorks** 資料庫中 **db_owner** 固定資料角色成員的使用者。  
  
6.  重複執行步驟 1-4，以建立本機 repl_distribution 帳戶的登入。 此登入必須對應至 **distribution** 資料庫中 **db_owner** 固定資料庫角色成員的使用者。  
  
7.  重複執行步驟 1-4，以建立本機 repl_merge 帳戶的登入。 此登入必須在 **distribution** 和 **AdventureWorks** 資料庫中有使用者對應。  
  
## <a name="see-also"></a>另請參閱  
[設定散發](../../relational-databases/replication/configure-distribution.md)  
[Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)  
  
  
  

