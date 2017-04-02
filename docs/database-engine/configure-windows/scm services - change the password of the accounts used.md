---
title: "變更 SQL Server 所使用之帳戶的密碼 (SQL Server 組態管理員) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "過期的密碼 [SQL Server], SQL Server Agent"
  - "密碼 [SQL Server], SQL Server Agent 服務"
  - "密碼 [SQL Server], 變更"
  - "過期的密碼 [SQL Server], Database Engine"
  - "密碼 [SQL Server], SQL Server 服務"
  - "Database Engine [SQL Server], 密碼"
  - "變更 SQL Server 所使用的密碼"
  - "修改密碼"
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 變更 SQL Server 所使用之帳戶的密碼 (SQL Server 組態管理員)
  此主題描述如何使用 SQL Server 組態管理員，在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 中變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Agent 所使用之帳戶的密碼。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 會使用安裝過程中最初提供的認證，在電腦上當做服務執行。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在網域帳戶下執行，而且該帳戶的密碼已變更時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所使用的密碼就必須更新為新的密碼。 如果沒有更新密碼， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會喪失某些網域資源的存取權，而且如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 停止，服務就要等到密碼更新後才會重新啟動。  
  
 若要變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 驗證的密碼，請參閱[密碼已過期](../../ssms/f1-help/password-expired.md)。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是已獲授權專供變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務各項設定而設計的工具。 使用 Windows 服務控制管理員 (**services.msc**) 應用程式變更 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務時，不一定能變更所有必要的設定，而且可能導致服務無法正常運作。 不過，在叢集環境的使用中節點上透過 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員變更密碼之後，必須在被動節點上使用服務控制管理員變更密碼。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須是電腦的系統管理員才能變更服務所使用的密碼。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### 變更 SQL Server Agent (Database Engine) 服務所使用的密碼  
  
1.  按一下 **[開始]** 按鈕，然後依序指向 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
    > [!NOTE]  
    >  由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理主控台程式的嵌入式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。  
    >   
    >  -   **Windows 10**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請在 [開始畫面] 上輸入 SQLServerManager13.msc (適用於 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)])。 若為舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則以較小的數字取代 13。 按一下 [SQLServerManager13.msc] 即可開啟組態管理員。 若要將組態管理員釘選到 [開始畫面] 或 [工作列]，請在 [SQLServerManager13.msc] 上按一下滑鼠右鍵，然後按一下 [開啟檔案位置]。 在 Windows 檔案總管中，在 [SQLServerManager13.msc] 上按一下滑鼠右鍵，然後按一下 [釘選到開始畫面] 或 [釘選到工作列]。  
    > -   **Windows 8**：  
    >          若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請在 [搜尋] 常用鍵的 [應用程式]  下，輸入 **SQLServerManager\<版本>.msc** (例如 **SQLServerManager13.msc**)，然後按 **Enter**。  
  
2.  在 [SQL Server 組態管理員] 中，按一下 **[SQL Server 服務]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server (\<執行個體名稱>)]，然後按一下 [屬性]。  
  
4.  在 [SQL Server (\<執行個體名稱>) 屬性] 對話方塊的 [登入] 索引標籤上，針對列於 [帳戶名稱] 方塊的帳戶，在 [密碼] 和 [確認密碼] 方塊中輸入新密碼，然後按一下 [確定]。  
  
     密碼會立即生效，不需重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
#### 變更 SQL Server Agent 服務所使用的密碼  
  
1.  按一下 **[開始]** 按鈕，然後依序指向 **[所有程式]**、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
2.  在 [SQL Server 組態管理員] 中，按一下 **[SQL Server 服務]**。  
  
3.  在詳細資料窗格中，以滑鼠右鍵按一下 [SQL Server Agent (\<執行個體名稱>)]，然後按一下 [屬性]。  
  
4.  在 [SQL Server Agent (\<執行個體名稱>) 屬性] 對話方塊的 [登入] 索引標籤上，針對列於 [帳戶名稱] 方塊的帳戶，在 [密碼] 和 [確認密碼] 方塊中輸入新密碼，然後按一下 [確定]。  
  
     在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 獨立執行個體上，密碼會立即生效，不需要重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在叢集執行個體上，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源離線，而且需要重新啟動。  
  
## 另請參閱  
 [管理服務的如何主題 &#40;SQL Server 組態管理員&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)  
  
  