---
title: "設定預先定義的複寫警示 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "警示 [SQL Server 複寫]"
  - "預先定義的複寫警示 [SQL Server 複寫]"
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# 設定預先定義的複寫警示 (SQL Server Management Studio)
  複寫提供下列預先定義的警示，這些警示可設定為回應複寫事件：  
  
-   **複寫: 代理程式成功**  
  
-   **複寫: 代理程式失敗**  
  
-   **複寫: 代理程式重試**  
  
-   **複寫: 已卸除逾期的訂閱**  
  
-   **複寫: 驗證失敗後重新初始化訂閱**  
  
-   **複寫: 訂閱者資料驗證失敗**  
  
-   **複寫: 訂閱者已經通過資料驗證**  
  
-   **複寫: 代理程式自訂關閉**  
  
 從這些警示設定 **警示** 資料夾中的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 **警告** 複寫監視器 」 中的索引標籤。 如需存取此索引標籤的詳細資訊，請參閱 [檢視資訊並執行工作訂閱 & #40。複寫監視器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)。  
  
 除了這些警示外，複寫監視器還提供與狀態和效能相關的警告與警示集合。 如需詳細資訊，請參閱 [設定臨界值和複寫監視器 」 中的警告](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。 您也可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 警示基礎結構，為其他複寫事件定義警示。 如需詳細資訊，請參閱 [建立使用者定義事件](../../../ssms/agent/create-a-user-defined-event.md)。  
  
### 若要在 Management Studio 中設定預先定義的複寫警示  
  
1.  連接到 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中的散發者，然後展開伺服器節點。  
  
2.  展開 **SQL Server Agent** 資料夾，然後展開 **警示** 資料夾。  
  
3.  複寫警示，以滑鼠右鍵按一下，然後按一下 **屬性**。  
  
4.  設定選項 **\< AlertName> 警示屬性** ] 對話方塊中︰  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]**；指定警示應套用至哪個資料庫。  
  
    -   在 **回應** 頁面上，指定是否應傳送電子郵件和/或應執行的作業。  
  
         如果警示為 **複寫︰ 訂閱者資料驗證失敗**, ，您可以指定回應作業複寫提供這項警示︰ 選取 **執行作業**, ，然後按一下 [瀏覽按鈕 (**...**)。 在 **尋找作業** 對話方塊中，按一下 [ **瀏覽**。 在 **瀏覽物件** 對話方塊中，選取 **重新初始化資料驗證失敗的訂閱**。 按一下 [ **確定** 在兩個開啟的對話方塊。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### 若要在複寫監視器中設定臨界值的警示  
  
1.  在 **警告** 索引標籤處按一下 **設定警示**。  
  
2.  在 **[設定複寫警示]** 對話方塊中選取一個警示，然後按一下 **[設定]**。  
  
3.  設定選項 **\< AlertName> 警示屬性** ] 對話方塊中︰  
  
    -   在 **[一般]** 頁面上，按一下 **[啟用]**；指定警示應套用至哪個資料庫。  
  
    -   在 **回應** 頁面上，指定是否應傳送電子郵件和/或應執行的作業。  
  
         如果警示為 **複寫︰ 訂閱者資料驗證失敗**, ，您可以指定回應作業複寫提供這項警示︰ 選取 **執行作業**, ，然後按一下 [瀏覽按鈕 (**...**)。 在 **尋找作業** 對話方塊中，按一下 [ **瀏覽**。 在 **瀏覽物件** 對話方塊中，選取 **重新初始化資料驗證失敗的訂閱**。 按一下 [ **確定** 在兩個開啟的對話方塊。 執行作業時，它會使用對預存程序的遠端程序呼叫 (RPC) 重新初始化訂閱。 如果「發行者」使用遠端「散發者」，則必須定義「發行者」端的遠端伺服器登入，以便建立從「散發者」到「發行者」的 RPC。  
  
    -   在 **[選項]** 頁面上，自訂回應的文字。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  按一下 [ **關閉**]。  
  
## 另請參閱  
 [使用複寫代理程式事件的警示](../../../relational-databases/replication/agents/use-alerts-for-replication-agent-events.md)  
  
  