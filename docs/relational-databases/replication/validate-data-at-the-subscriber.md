---
title: "驗證訂閱者端的資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "訂閱者 [SQL Server 複寫], 資料驗證"
  - "複寫 [SQL Server 複寫], 驗證資料"
  - "異動複寫, 驗證資料"
  - "驗證資料"
  - "合併式複寫資料驗證 [SQL Server 複寫], SQL Server Management Studio"
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 驗證訂閱者端的資料
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中驗證訂閱者端的資料。  
  
 驗證資料是一個三部份式的處理：  
  
1.  *「標示」* 要驗證之發行集的單個或所有訂閱。 在 [驗證單一訂閱] 、[驗證多個訂閱] 和 [驗證全部訂閱]  對話方塊 (位於 **的 [本機發行集]****資料夾和 [本機訂閱]**[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]資料夾) 中標示要驗證的訂閱。 您也可以從複寫監視器中的 **[所有訂閱]** 索引標籤、 **[訂閱監看清單]** 索引標籤和發行集節點標示訂閱。 如需啟動複寫監視器的詳細資訊，請參閱 [啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
2.  在下一次由「散發代理程式」(用於異動複寫) 或「合併代理程式」(用於合併式複寫) 進行同步時，將對訂閱進行驗證。 「散發代理程式」通常連續執行，此時可立即進行驗證；「合併代理程式」通常視需要執行，此時驗證將在執行代理程式後進行。  
  
3.  檢視驗證結果：  
  
    -   在「複寫監視器」的詳細資料視窗中：用於異動複寫的 **[散發者到訂閱者記錄]** 索引標籤和用於合併式複寫的 **[同步處理記錄]** 索引標籤上。  
  
    -   在 **的** [檢視同步處理的狀態] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]對話方塊中。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
-   **若要驗證訂閱者端的資料，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   「複寫監視器」的程序僅用於發送訂閱，因為發送訂閱無法在「複寫監視器」中同步。 但是，您可以標示要驗證的訂閱，並在「複寫監視器」中檢視發送訂閱的驗證結果。  
  
-   驗證結果會指示驗證成功或失敗，但不會在驗證失敗時指定失敗的資料列。 若要比較「發行者」和「訂閱者」端的資料，請使用 [tablediff Utility](../../tools/tablediff-utility.md)。 如需使用此公用程式與複寫資料的詳細資訊，請參閱 [比較複寫資料表差異 & #40。複寫程式設計 & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 若要驗證交易式發行集之訂閱的資料 (Management Studio)  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要驗證訂閱，然後按一下發行的集 **驗證訂閱**。  
  
4.  在 **[驗證訂閱]** 對話方塊中，選取要驗證的訂閱：  
  
    -   選取 **[驗證所有的 SQL Server 訂閱]**。  
  
    -   選取 **[驗證下列訂閱]**，然後選取一或多個訂閱。  
  
5.  若要指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型，請按一下 **驗證選項**, ，然後指定選項中的 **訂閱驗證選項** 對話方塊。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在複寫監視器或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果。 針對每個訂閱：  
  
    1.  展開的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **檢視同步處理狀態**。  
  
    2.  如果代理程式尚未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。  
  
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  
  
#### 若要驗證合併式發行集之單一訂閱的資料 (Management Studio)  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  展開您要驗證訂閱，訂閱中，按一下滑鼠右鍵，然後按一下發行的集 **驗證訂閱**。  
  
4.  在 **[驗證訂閱]** 對話方塊中，選取 **[驗證此訂閱]**。  
  
5.  若要指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型，請按一下 **選項**, ，然後指定選項中的 **訂閱驗證選項** 對話方塊。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在「複寫監視器」或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果：  
  
    1.  展開的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **檢視同步處理狀態**。  
  
    2.  如果代理程式未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。  
  
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  
  
#### 若要驗證合併式發行集之所有訂閱的資料 (Management Studio)  
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。  
  
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。  
  
3.  以滑鼠右鍵按一下您想要驗證訂閱，然後按一下發行的集 **驗證所有訂閱**。  
  
4.  在 **驗證所有訂閱** 對話方塊方塊中，指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  在複寫監視器或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果。 針對每個訂閱：  
  
    1.  展開的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **檢視同步處理狀態**。  
  
    2.  如果代理程式未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。  
  
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  
  
#### 若要驗證交易式發行集之所有發送訂閱的資料 (複寫監視器)  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。  
  
2.  以滑鼠右鍵按一下您想要驗證訂閱，然後按一下發行的集 **驗證訂閱**。  
  
3.  在 **[驗證訂閱]** 對話方塊中，選取要驗證的訂閱：  
  
    -   選取 **[驗證所有的 SQL Server 訂閱]**。  
  
    -   選取 **[驗證下列訂閱]**，然後選取一或多個訂閱。  
  
4.  若要指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型，請按一下 **驗證選項**, ，然後指定選項中的 **訂閱驗證選項** 對話方塊。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  按一下 **[所有訂閱]** 索引標籤。  
  
7.  檢視驗證結果。 針對每個發送訂閱：  
  
    1.  如果代理程式未執行，以滑鼠右鍵按一下訂閱，然後按一下 **啟動同步處理**。  
  
    2.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **檢視詳細資料**。  
  
    3.  檢視 **[所選取工作階段中的動作]** 文字區域之 **[散發者到訂閱者記錄]** 索引標籤中的資訊。  
  
#### 若要驗證合併式發行集之單一發送訂閱的資料 (複寫監視器)  
  
1.  在複寫監視器中，展開左窗格裡的發行者群組，展開發行者，然後按一下發行集。  
  
2.  按一下 **[所有訂閱]** 索引標籤。  
  
3.  以滑鼠右鍵按一下您要驗證，然後按一下 [的訂閱 **驗證訂閱**。  
  
4.  在 **[驗證訂閱]** 對話方塊中，選取 **[驗證此訂閱]**。  
  
5.  若要指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型，請按一下 **選項**, ，然後指定選項中的 **訂閱驗證選項** 對話方塊。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  按一下 **[所有訂閱]** 索引標籤。  
  
8.  檢視驗證結果：  
  
    1.  如果代理程式未執行，以滑鼠右鍵按一下訂閱，然後按一下 **啟動同步處理**。  
  
    2.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **檢視詳細資料**。  
  
    3.  在 **[同步處理記錄]** 索引標籤上的 **[所選取工作階段的最後訊息]** 測試區域中檢視資訊。  
  
#### 若要驗證合併式發行集之所有發送訂閱的資料 (複寫監視器)  
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。  
  
2.  以滑鼠右鍵按一下您想要驗證訂閱，然後按一下發行的集 **驗證所有訂閱**。  
  
3.  在 **驗證所有訂閱** 對話方塊方塊中，指定要執行 （資料列計數，或資料列計數與總和檢查碼） 的驗證類型。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  按一下 **[所有訂閱]** 索引標籤。  
  
6.  檢視驗證結果。 針對每個發送訂閱：  
  
    1.  如果代理程式未執行，以滑鼠右鍵按一下訂閱，然後按一下 **啟動同步處理**。  
  
    2.  在訂閱中，以滑鼠右鍵按一下，然後按一下 **檢視詳細資料**。  
  
    3.  在 **[同步處理記錄]** 索引標籤上的 **[所選取工作階段的最後訊息]** 測試區域中檢視資訊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 若要驗證交易式發行集中所有發行項的資料  
  
1.  在發行集資料庫的發行者，執行 [sp_publication_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)。 指定 **@publication** 和下列其中一個值 **@rowcount_only**:  
  
    -   **1** -列數檢查 （預設值）  
  
    -   **2** -資料列計數與二進位總和檢查碼。  
  
    > [!NOTE]  
    >  當您執行 [sp_publication_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), ，[sp_article_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 會針對發行集中的每個發行項執行。 若要成功地執行 [sp_publication_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), ，您必須在已發行的基底資料表中的所有資料行上 SELECT 權限。  
  
2.  (選擇性) 針對每個訂閱啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [驗證複寫資料](../../relational-databases/replication/validate-replicated-data.md)。  
  
#### 若要驗證交易式發行集中單一發行項的資料  
  
1.  在發行集資料庫的發行者，執行 [sp_article_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 **@publication**, ，針對發行項名稱 **@article**, ，和下列其中一個值 **@rowcount_only**:  
  
    -   **1** -列數檢查 （預設值）  
  
    -   **2** -資料列計數與二進位總和檢查碼。  
  
    > [!NOTE]  
    >  若要成功地執行 [sp_article_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), ，您必須在已發行的基底資料表中的所有資料行上 SELECT 權限。  
  
2.  (選擇性) 針對每個訂閱啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [驗證複寫資料](../../relational-databases/replication/validate-replicated-data.md)。  
  
#### 若要驗證交易式發行集中單一訂閱者的資料  
  
1.  在發行集資料庫的發行者，請開啟 [使用外顯交易 [BEGIN TRANSACTION & #40。TRANSACT-SQL & #41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)。  
  
2.  在發行集資料庫的發行者，執行 [sp_marksubscriptionvalidation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)。 指定的發行集 **@publication**, ，訂閱者的名稱 **@subscriber**, ，和訂閱資料庫的名稱 **@destination_db**。  
  
3.  (選擇性) 針對每個要驗證的訂閱重複步驟 2。  
  
4.  在發行集資料庫的發行者，執行 [sp_article_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 **@publication**, ，針對發行項名稱 **@article**, ，和下列其中一個值 **@rowcount_only**:  
  
    -   **1** -列數檢查 （預設值）  
  
    -   **2** -資料列計數與二進位總和檢查碼。  
  
    > [!NOTE]  
    >  若要成功地執行 [sp_article_validation & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), ，您必須在已發行的基底資料表中的所有資料行上 SELECT 權限。  
  
5.  在發行集資料庫的發行者，認可交易使用 [認可交易 & #40。TRANSACT-SQL & #41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)。  
  
6.  (選擇性) 針對每個要驗證的發行項重複步驟 1 到 5。  
  
7.  (選擇性) 啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
8.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
#### 若要驗證所有合併發行集訂閱中的資料  
  
1.  在發行集資料庫的發行者，執行 [sp_validatemergepublication & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)。 指定 **@publication** 以及下列其中一個 **@level**值：  
  
    -   **1** -僅限資料列計數驗證。  
  
    -   **3** -列數二進位總和檢查碼驗證。  
  
     這會標示所有訂閱以供驗證。  
  
2.  針對每項訂閱啟動合併代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
#### 若要驗證選取的合併發行集訂閱中的資料  
  
1.  在發行集資料庫的發行者，執行 [sp_validatemergesubscription & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)。 指定 **@publication**, ，訂閱者的名稱 **@subscriber**, ，訂閱資料庫的名稱 **@subscriber_db**, ，和下列其中一個值 **@level**:  
  
    -   **1** -僅限資料列計數驗證。  
  
    -   **3** -列數二進位總和檢查碼驗證。  
  
     這會標示選取的訂閱以供驗證。  
  
2.  針對每項訂閱啟動合併代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  檢查代理程式輸出，以取得驗證的結果。  
  
4.  針對每個要驗證的訂閱重複步驟 1 到 3。  
  
> [!NOTE]  
>  合併式發行集的訂閱也能在同步處理結束驗證的指定 **-驗證** 參數執行時 [複寫合併代理程式](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
#### 若要使用合併代理程式參數驗證訂閱中的資料  
  
1.  以下列其中一種方法，從命令提示字元啟動「合併代理程式」(在「訂閱者」端的為提取訂閱，在「散發者」端的則為發送訂閱)。  
  
    -   指定的值為 **1** （列數） 或 **3** （資料列計數與二進位總和檢查碼） 的 **-驗證** 參數。  
  
    -   指定 **資料列計數驗證** 或 **資料列計數與總和檢查碼驗證** 的 **-ProfileName** 參數。  
  
     如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
##  <a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 複寫能讓您以程式設計的方式，使用 Replication Management Objects (RMO) 驗證「訂閱者」和「發行者」兩端的資料相符。 您使用的物件依照複寫拓撲的類型而定。 異動複寫需要驗證發行集的所有訂閱。  
  
> [!NOTE]  
>  如需範例，請參閱 [範例 (RMO)](#RMOExample), ，稍後在本章節中。  
  
#### 若要驗證交易式發行集中所有發行項的資料  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別。 設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集屬性。 設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 方法。 傳遞下列項目：  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   此為布林值，指出在驗證完成後是否要停止「散發代理程式」。  
  
     這會標示要驗證的發行項。  
  
5.  如果尚未執行，請啟動「散發代理程式」以同步處理每個訂閱。 如需相關資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 或 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。 驗證作業的結果會寫入至代理程式記錄。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
#### 若要驗證所有合併發行集訂閱中的資料  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別。 設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集屬性。 設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 方法。 傳遞所要 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  為每個訂閱執行「合併代理程式」以啟動驗證，或等候下一個排程的代理程式執行。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 驗證作業的結果會寫入至代理程式記錄，您可使用「複寫監視器」來加以檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
#### 若要驗證合併發行集單一訂閱中的資料  
  
1.  建立連接到 「 發行者 」 使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別。  
  
2.  建立的執行個體 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別。 設定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 發行集屬性。 設定 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 在步驟 1 中建立的連接屬性。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法來取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 方法。 傳遞驗證訂閱者和訂閱資料庫的名稱和所需 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  為訂閱執行「合併代理程式」以啟動驗證，或等候下一個排程的代理程式執行。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 驗證作業的結果會寫入至代理程式記錄，您可使用「複寫監視器」來加以檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
###  <a name="RMOExample"></a> 範例 (RMO)  
 此範例會標示交易式發行集的所有訂閱，以進行列數驗證。  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 此範例會標示合併式發行集的特定訂閱，以進行列數驗證。  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  