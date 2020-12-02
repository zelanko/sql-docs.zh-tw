---
description: 驗證複寫的資料
title: 驗證複寫的資料 | Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c83a02c9c2b0c8c22a62f1765c839a1c15534405
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "88470180"
---
# <a name="validate-replicated-data"></a>驗證複寫的資料
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 Replication Management Objects (RMO)，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中驗證訂閱者端的資料。  
  
交易式與合併式複寫可以讓您驗證訂閱者端的資料是否與發行者端的資料相符。 可以驗證特定的訂閱或發行的所有訂閱。 指定下列其中一種驗證類型，「散發代理程式」或「合併代理程式」將在下次執行時驗證資料：  
  
-   **僅限資料列計數。** 這將會驗證「訂閱者」上的資料表與「發行者」上的資料表是否具有相同數量的資料列，但無法驗證資料列內容是否相符。 資料列計數驗證提供一種輕量型驗證方法，可讓您發現資料中的問題。   
-   **資料列計數與二進位總和檢查碼。** 除了統計「發行者」與「訂閱者」上的資料列數量之外，也會使用總和檢查碼演算法計算所有資料的總和檢查碼。 如果資料列計數失敗，就不會執行總和檢查碼。  
  
 除驗證「訂閱者」與「發行者」上的資料是否相符外，合併代理程式還可以驗證是否為每個「訂閱者」正確分割資料。 如需詳細資訊，請參閱[驗證合併訂閱者的資料分割資訊](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md)。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
   
## <a name="how-data-validation-works"></a>資料驗證如何運作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 藉由計算「發行者」的資料列計數或總和檢查碼，然後將那些值與「訂閱者」所計算的資料列計數或總和檢查碼相比較，以驗證其資料。 整個發行集資料表計算一個值，整個訂閱資料表也計算一個值，但是 **text**、 **ntext** 或 **image** 資料行的資料不包含在其計算中。  
  
 在執行計算時，會暫時以共用鎖定來鎖定正在執行資料列計數或總和檢查碼的資料表，但此計算會迅速完成，並移除共用鎖定，通常只需要數秒鐘。  
  
 使用二進位總和檢查碼時，資料行會逐一發生 32 位元的 Redundancy Check (CRC)，而不是資料頁中實際資料列的 CRC。 如此可讓具有該資料表的資料行在資料頁以任何次序排序，而仍可計算資料列的相同 CRC。 發行集具有資料列或資料行篩選時，可以使用二進位總和檢查碼驗證。  

 驗證資料是一個三部份式的處理：  
  
1.  *「標示」* 要驗證之發行集的單個或所有訂閱。 在 [驗證單一訂閱] 、[驗證多個訂閱] 和 [驗證所有訂閱]  對話方塊 (位於 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 [本機發行集]資料夾和 [本機訂閱]資料夾) 中標示要驗證的訂閱。 您也可以從複寫監視器中的 **[所有訂閱]** 索引標籤、 **[訂閱監看清單]** 索引標籤和發行集節點標示訂閱。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
2.  在下一次由「散發代理程式」(用於異動複寫) 或「合併代理程式」(用於合併式複寫) 進行同步時，將對訂閱進行驗證。 「散發代理程式」通常連續執行，此時可立即進行驗證；「合併代理程式」通常視需要執行，此時驗證將在執行代理程式後進行。  
  
3.  檢視驗證結果：   
    -   在「複寫監視器」的詳細資料視窗中：用於異動複寫的 **[散發者到訂閱者記錄]** 索引標籤和用於合併式複寫的 **[同步處理記錄]** 索引標籤上。    
    -   在 **的** [檢視同步處理的狀態] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]對話方塊中。  
 
## <a name="considerations-and-restrictions"></a>考量與限制  
 在驗證資料時，請考慮下列問題：  
  
-   您必須在驗證資料之前停止「訂閱者」上的所有更新活動 (在進行驗證時不必停止「發行者」上的活動)。  
-   由於總和檢查碼與二進位總和檢查碼在驗證大型資料集時，可能需要使用大量的處理器資源，因此應該將驗證排在伺服器複寫活動最少的時間來進行。   
-   複寫僅驗證資料表；它無法驗證只有結構描述的發行項 (例如預存程序) 在「發行者」與「訂閱者」上是否相同。   
-   二進位總和檢查碼可以與任何已發行資料表一起使用。 總和檢查碼無法驗證具有資料行篩選或其中資料行位移不同 (由於 ALTER TABLE 陳述式卸除或新增資料行) 的邏輯資料表結構的資料表。   
-   複寫驗證會使用 **checksum** 和 **binary_checksum** 函數。 如需其行為的資訊，請參閱[總和檢查碼 &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) 和 [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)。   
-   如果「訂閱者」與「發行者」端的資料類型不同，則使用二進位總和檢查碼或總和檢查碼的驗證可能會誤報失敗。 如果執行下列任何一項作業，就可能發生上述情況：    
    -   將結構描述選項明確地設定為對應舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料類型。  
    -   將合併式發行集的發行集相容性層級設定為舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，而已發行的資料表則包含一或多個必須對應此版本的資料類型。    
    -   手動初始化訂閱且在「訂閱者」端使用不同的資料類型。   
-   異動複寫的可轉換訂閱不支援二進位總和檢查碼與總和檢查碼驗證。   
-   複寫給非「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者」的資料不支援驗證。    
-   「複寫監視器」的程序僅用於發送訂閱，因為發送訂閱無法在「複寫監視器」中同步。 但是，您可以標示要驗證的訂閱，並在「複寫監視器」中檢視發送訂閱的驗證結果。    
-   驗證結果會指示驗證成功或失敗，但不會在驗證失敗時指定失敗的資料列。 若要比較「發行者」和「訂閱者」端的資料，請使用 [tablediff Utility](../../tools/tablediff-utility.md)。 如需使用這個公用程式與複寫資料的詳細資訊，請參閱[比較複寫資料表的差異 &#40;複寫程式設計&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  


## <a name="data-validation-results"></a>資料驗證結果  
 當驗證完成時，「散發代理程式」或「合併代理程式」將記錄有關成功或失敗的訊息 (複寫不會報告具體是哪些資料列失敗)。 可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、「複寫監視器」和複寫系統資料表中檢視這些訊息。 以上列出的「如何」主題示範如何執行驗證並檢視結果。  
  
 若要處理驗證失敗，請考慮下列各項：  
  
-   設定名稱為 **複寫: 訂閱者資料驗證失敗** 的複寫警示，以便通知您失敗的情況。 如需詳細資訊，請參閱[設定預先定義的複寫警示 &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md)。  
  
-   您的應用程式是否有驗證失敗的問題？ 如果有驗證失敗的問題，請手動更新資料以便對其進行同步處理，或重新初始化訂閱：  
  
    -   可以使用 [tablediff 公用程式](../../tools/tablediff-utility.md)更新資料。 如需使用此公用程式的詳細資訊，請參閱[比較複寫資料表的差異 &#40;複寫程式設計&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
    -   如需詳細資訊，請參閱[重新初始化訂閱](../../relational-databases/replication/reinitialize-subscriptions.md)。  

  
  
## <a name="articles-in-transactional-replication"></a>異動複寫中的發行項 

### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。    
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。    
3.  以滑鼠右鍵按一下您要驗證訂閱的發行集，然後按一下 **[驗證訂閱]**。    
4.  在 **[驗證訂閱]** 對話方塊中，選取要驗證的訂閱：   
    -   選取 **[驗證所有的 SQL Server 訂閱]**。    
    -   選取 **[驗證下列訂閱]**，然後選取一或多個訂閱。    
5.  若要指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)，請按一下 **[驗證選項]**，然後在 **[訂閱驗證選項]** 對話方塊中指定選項。  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]   
7.  在複寫監視器或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果。 針對每個訂閱：   
    1.  展開發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[檢視同步處理的狀態]**。    
    2.  如果代理程式尚未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。    
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  

### <a name="using-transact-sql"></a>使用 TRANSACT-SQL

#### <a name="all-articles"></a>所有發行項 
  
1.  在發行集資料庫的發行者端，執行 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)。 針對 `@rowcount_only` 指定 `@publication` 和下列其中一個值：  
  
    -   **1** - 只限列數檢查 (預設值)    
    -   **2** - 列數及二進位總和檢查碼。  
  
    > [!NOTE]  
    >  當您執行 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) 時，會針對每個發行集中的發行項執行 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 若要成功地執行 [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)，您必須有已發行基底資料表之所有資料行的 SELECT 權限。    
2.  (選擇性) 針對每個訂閱啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。    
3.  檢查代理程式輸出，以取得驗證的結果。 
  
#### <a name="single-article"></a>單一發行項  
  
1.  在發行集資料庫的發行者端，執行 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 `@publication`，針對 `@article` 指定發行項名稱及針對 `@rowcount_only` 指定下列其中一個值：  
  
    -   **1** - 只限列數檢查 (預設值)    
    -   **2** - 列數及二進位總和檢查碼。  
  
    > [!NOTE]  
    >  若要成功地執行 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)，您必須有已發行基底資料表之所有資料行的 SELECT 權限。  
  
2.  (選擇性) 針對每個訂閱啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。    
3.  檢查代理程式輸出，以取得驗證的結果。
  
#### <a name="single-subscriber"></a>單一訂閱者 
  
1.  在發行集資料庫的發行者端，使用 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md) 來開啟明確交易。    
2.  在發行集資料庫的發行者端，執行 [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)。 指定 `@publication` 的發行集、`@subscriber` 的訂閱者名稱及 `@destination_db` 的訂閱資料庫名稱。    
3.  (選擇性) 針對每個要驗證的訂閱重複步驟 2。    
4.  在發行集資料庫的發行者端，執行 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 `@publication`，針對 `@article` 指定發行項名稱及針對 `@rowcount_only` 指定下列其中一個值：    
    -   **1** - 只限列數檢查 (預設值)    
    -   **2** - 列數及二進位總和檢查碼。  
  
    > [!NOTE]  
    >  若要成功地執行 [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)，您必須有已發行基底資料表之所有資料行的 SELECT 權限。  
  
5.  在發行集資料庫的發行者端，使用 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md) 來認可交易。    
6.  (選擇性) 針對每個要驗證的發行項重複步驟 1 到 5。   
7.  (選擇性) 啟動「散發代理程式」(如果尚未執行)。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。    
8.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  

## <a name="all-push-subscriptions-to-a-transactional-publication"></a>交易式發行集的所有發送訂閱 

### <a name="using-replication-monitor"></a>使用複寫監視器
  
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。   
2.  以滑鼠右鍵按一下您要驗證訂閱的發行集，然後按一下 **[驗證訂閱]**。   
3.  在 **[驗證訂閱]** 對話方塊中，選取要驗證的訂閱：  
  
    -   選取 **[驗證所有的 SQL Server 訂閱]**。    
    -   選取 **[驗證下列訂閱]**，然後選取一或多個訂閱。    
4.  若要指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)，請按一下 **[驗證選項]**，然後在 **[訂閱驗證選項]** 對話方塊中指定選項。    
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  按一下 **[所有訂閱]** 索引標籤。  
7.  檢視驗證結果。 針對每個發送訂閱：    
    1.  如果代理程式未執行，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。    
    2.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。   
    3.  檢視 **[所選取工作階段中的動作]** 文字區域之 **[散發者到訂閱者記錄]** 索引標籤中的資訊。  
  
## <a name="for-a-single-subscription-to-a-merge-publication"></a>針對合併式發行集的單一訂閱

### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio
  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。    
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。   
3.  展開要驗證訂閱的發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[驗證單一訂閱]**。    
4.  在 **[驗證訂閱]** 對話方塊中，選取 **[驗證此訂閱]**。    
5.  若要指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)，請按一下 **[選項]**，然後在 **[訂閱驗證選項]** 對話方塊中指定選項。    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
7.  在「複寫監視器」或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果：  
  
    1.  展開發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[檢視同步處理的狀態]**。    
    2.  如果代理程式未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。  
  
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  
  
## <a name="for-all-subscriptions-to-a-merge-publication"></a>針對合併式發行集的所有訂閱

### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio  
1.  連接到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的發行者，然後展開伺服器節點。    
2.  展開 **[複寫]** 資料夾，然後展開 **[本機發行集]** 資料夾。   
3.  以滑鼠右鍵按一下您要驗證訂閱的發行集，然後按一下 **[驗證所有訂閱]**。    
4.  在 **[驗證所有訂閱]** 對話方塊中，指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)。   
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
6.  在複寫監視器或 **[檢視同步處理的狀態]** 對話方塊中檢視驗證結果。 針對每個訂閱：    
    1.  展開發行集，以滑鼠右鍵按一下訂閱，然後按一下 **[檢視同步處理的狀態]**。    
    2.  如果代理程式未執行，請按一下 **[檢視同步處理的狀態]** 對話方塊中的 **[啟動]** 。 對話方塊就會顯示關於驗證的參考用訊息。  
  
     如果您未看到任何關於驗證的訊息，則代理程式已經記錄了後續訊息。 在此情況下，請在複寫監視器中檢視驗證結果。 如需詳細資訊，請參閱這個主題中＜複寫監視器＞的如何程序。  
  
 
## <a name="for-a-single-push-subscription-to-a-merge-publication"></a>針對合併式發行集的單一發送訂閱 

### <a name="using-replication-monitor"></a>使用複寫監視器  
1.  在複寫監視器中，展開左窗格裡的發行者群組，展開發行者，然後按一下發行集。    
2.  按一下 **[所有訂閱]** 索引標籤。    
3.  以滑鼠右鍵按一下您要驗證的訂閱，然後按一下 **[驗證單一訂閱]**。    
4.  在 **[驗證訂閱]** 對話方塊中，選取 **[驗證此訂閱]**。    
5.  若要指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)，請按一下 **[選項]**，然後在 **[訂閱驗證選項]** 對話方塊中指定選項。    
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
7.  按一下 **[所有訂閱]** 索引標籤。    
8.  檢視驗證結果：    
    1.  如果代理程式未執行，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。    
    2.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。    
    3.  在 **[同步處理記錄]** 索引標籤上的 **[所選取工作階段的最後訊息]** 測試區域中檢視資訊。  

### <a name="using-transact-sql"></a>使用 TRANSACT-SQL
1.  在發行集資料庫的發行者端，執行 [sp_validatemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)。 指定 `@publication`、`@subscriber` 的發行集、`@subscriber_db` 的訂閱者資料庫名稱，以及針對 `@level` 指定下列其中一個值：   
    -   **1** - 只驗證列數。    
    -   **3** - 驗證列數二進位總和檢查碼。  
  
     這會標示選取的訂閱以供驗證。  
  
2.  針對每項訂閱啟動合併代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
3.  檢查代理程式輸出，以取得驗證的結果。   
4.  針對每個要驗證的訂閱重複步驟 1 到 3。  
  
> [!NOTE]  
>  您也可以在執行 **Replication Merge Agent** 時藉由指定 [-Validate](../../relational-databases/replication/agents/replication-merge-agent.md)參數，在同步處理結束時驗證合併發行集的訂閱。  
  
## <a name="for-all-push-subscriptions-to-a-merge-publication"></a>針對合併式發行集的所有發送訂閱
  
### <a name="using-replication-monitor"></a>使用複寫監視器    
1.  在複寫監視器的左窗格中展開發行者群組，然後展開發行者。    
2.  以滑鼠右鍵按一下您要驗證訂閱的發行集，然後按一下 **[驗證所有訂閱]**。    
3.  在 **[驗證所有訂閱]** 對話方塊中，指定要執行驗證的類型 (資料列計數，或資料列計數與總和檢查碼)。    
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]    
5.  按一下 **[所有訂閱]** 索引標籤。    
6.  檢視驗證結果。 針對每個發送訂閱：    
    1.  如果代理程式未執行，請以滑鼠右鍵按一下訂閱，然後按一下 **[啟動同步處理]**。    
    2.  以滑鼠右鍵按一下訂閱，然後按一下 **[檢視詳細資料]**。    
    3.  在 **[同步處理記錄]** 索引標籤上的 **[所選取工作階段的最後訊息]** 測試區域中檢視資訊。 
  
### <a name="using-transact-sql"></a>使用 TRANSACT-SQL
1.  在發行集資料庫的發行者端，執行 [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)。 針對 `@level` 指定 `@publication` 和下列其中一個值：    
    -   **1** - 只驗證列數。   
    -   **3** - 驗證列數二進位總和檢查碼。  
  
     這會標示所有訂閱以供驗證。   
2.  針對每項訂閱啟動合併代理程式。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  檢查代理程式輸出，以取得驗證的結果。 如需詳細資訊，請參閱 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  

  
## <a name="validate-data-using-merge-agent-parameters"></a>使用合併代理程式參數來驗證資料  
  
1.  以下列其中一種方法，從命令提示字元啟動「合併代理程式」(在「訂閱者」端的為提取訂閱，在「散發者」端的則為發送訂閱)。   
    -   針對 **-Validate** 參數，指定值 **1** (列數) 或 **3** (列數和二進位總和檢查碼)。    
    -   針對 **-ProfileName** 參數，指定 **rowcount validation** 或 **rowcount and checksum validation** 。  
  
     如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用 Replication Management Objects (RMO)  
 複寫能讓您以程式設計的方式，使用 Replication Management Objects (RMO) 驗證「訂閱者」和「發行者」兩端的資料相符。 您使用的物件依照複寫拓撲的類型而定。 異動複寫需要驗證發行集的所有訂閱。  
  
> [!NOTE]  
>  如需範例，請參閱本主題稍後的 [範例 (RMO)](#RMOExample)。  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>若要驗證交易式發行集中所有發行項的資料  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.TransPublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性。 將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 方法。 傳遞下列項目：  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   此為布林值，指出在驗證完成後是否要停止「散發代理程式」。  
  
     這會標示要驗證的發行項。  
  
5.  如果尚未執行，請啟動「散發代理程式」以同步處理每個訂閱。 如需相關資訊，請參閱 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 或 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。 驗證作業的結果會寫入至代理程式記錄。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)。  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>若要驗證所有合併發行集訂閱中的資料  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性。 將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 方法。 傳遞所要的 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  為每個訂閱執行「合併代理程式」以啟動驗證，或等候下一個排程的代理程式執行。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 驗證作業的結果會寫入至代理程式記錄，您可使用「複寫監視器」來加以檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)。  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>若要驗證合併發行集單一訂閱中的資料  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別建立與發行者的連接。  
  
2.  建立 <xref:Microsoft.SqlServer.Replication.MergePublication> 類別的執行個體。 設定發行集的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 屬性。 將 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 屬性設定為在步驟 1 中建立的連接。  
  
3.  呼叫 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以取得物件的剩餘屬性。 如果此方法傳回 **false**，則表示步驟 2 中的發行集屬性定義不正確，或者該發行集不存在。  
  
4.  呼叫 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 方法。 傳遞正在進行驗證之「訂閱者」和訂閱資料庫的名稱以及所要的 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  為訂閱執行「合併代理程式」以啟動驗證，或等候下一個排程的代理程式執行。 如需相關資訊，請參閱 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 以及 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 驗證作業的結果會寫入至代理程式記錄，您可使用「複寫監視器」來加以檢視。 如需詳細資訊，請參閱 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)。  
  
###  <a name="example-rmo"></a><a name="RMOExample"></a> 範例 (RMO)  
 此範例會標示交易式發行集的所有訂閱，以進行列數驗證。  
  
 [!code-cs[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 此範例會標示合併式發行集的特定訂閱，以進行列數驗證。  
  
 [!code-cs[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
 ## <a name="see-also"></a>另請參閱  
[Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
