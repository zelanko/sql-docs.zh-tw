---
title: "複寫識別欄位 | Microsoft Docs"
ms.custom: ""
ms.date: "10/04/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "識別 [SQL Server 複寫]"
  - "識別值 [SQL Server 複寫]"
  - "合併式複寫 [SQL Server 複寫], 識別範圍管理"
  - "發行 [SQL Server 複寫], 識別欄位"
  - "異動複寫, 識別範圍管理"
  - "識別欄位 [SQL Server], 複寫"
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# 複寫識別欄位
  當您指派給資料行的 IDENTITY 屬性 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 自動產生的資料表包含識別資料行中插入新資料列的序號。 如需詳細資訊，請參閱 [身分識別 & #40。屬性 &#41;& #40。TRANSACT-SQL &#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md)。 由於識別欄位可能會做為主索引鍵的一部分，因此請務必避免在識別欄位中重複值。 若要在具有多個節點更新的複寫拓撲裡使用識別欄位，複寫拓撲中的每個節點必須使用不同的識別值範圍，以免出現重複。  
  
 例如，「發行者」可指派範圍 1-100、訂閱者 A 指派範圍 101-200，訂閱者 B 則指派範圍 201-300。 如果在「發行者」插入資料列，而且識別值是 65，該值就會複寫到每個「訂閱者」。 當複寫在每個「訂閱者」端插入資料時，不會遞增「訂閱者」資料表中的識別欄位值，而是插入常值 65。 只有使用者插入會導致識別欄位值遞增，複寫代理程式插入則不會。  
  
 複寫會處理所有發行集與訂閱類型的識別欄位，讓您能夠手動管理資料行，或者讓複寫自動管理這些資料行。  
  
> [!NOTE]  
>  不支援在已發行的資料表上加入識別欄位，因為可能在資料行複寫至「訂閱者」時，導致無法聚合。 簽發者端識別欄位中的值，隨著受影響的資料表之資料列的實際儲存順序而不同。 資料列可能以不同方式儲存在訂閱者端；因此識別欄位的值可能與同資料列的不同。  
  
## 指定識別範圍管理選項  
 複寫提供三個識別範圍管理選項：  
  
-   自動。 用於「訂閱者」端更新的合併式複寫與異動複寫。 指定「發行者」與「訂閱者」的大小範圍，複寫會自動管理新範圍的指派。 複寫還會為「訂閱者」端的識別欄位設定 NOT FOR REPLICATION 選項，以便只有使用者插入會導致值在「訂閱者」端遞增。  
  
    > [!NOTE]  
    >  「訂閱者」必須與「發行者」同步，方可接收新範圍。 由於「訂閱者」的識別範圍是自動指派的，因此如果反覆要求新範圍，任何「訂閱者」都可能用盡整個識別範圍。  
  
-   手動。 用於「訂閱者」端沒有更新的快照式與異動複寫、點對點異動複寫，或者是應用程式必須程式化控制識別範圍的情況。 如果指定手動管理，必須確定範圍指派到了「發行者」與每個「訂閱者」，並在使用初始範圍時指派新範圍。 複寫會為「訂閱者」端的識別欄位設定 NOT FOR REPLICATION 選項。  
  
-   無。 此選項僅建議用於與舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的回溯相容性，並且僅在交易式發行集的預存程序介面可用。  
  
 若要指定識別範圍管理選項，請參閱 [管理身分識別資料行](../../../relational-databases/replication/publish/manage-identity-columns.md)。  
  
## 指派識別範圍  
 合併式複寫與異動複寫使用不同的方法指派範圍；這些方法在本節中均有描述。  
  
 複寫識別欄位時要考慮兩種範圍：指派至「發行者」與「訂閱者」的範圍，以及資料行中資料類型的範圍。 下表顯示識別欄位中通常使用之資料類型可用的範圍。 範圍用於拓撲中的所有節點。 例如，如果您使用 **smallint** 從 1 開始的遞增值為 1，插入的最大數目為 32767 的 「 發行者 」 與所有訂閱者。 插入的實際數目取決於使用的值中是否有間距，以及是否使用臨界值。 如需臨界值的詳細資訊，請參閱下列的「合併式複寫」和「具有佇列更新訂閱的異動複寫」各節。  
  
 如果 「 發行者 」 耗盡後插入的識別範圍，它可以自動指派新範圍的成員執行插入 **db_owner** 固定的資料庫角色。 如果使用者不在該角色、 記錄讀取器代理程式 」、 「 合併代理程式或成員的使用者執行插入的 **db_owner** 角色必須執行 [sp_adjustpublisheridentityrange & #40。TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)。 對於異動複寫，「記錄讀取器代理程式」必須執行才能自動配置新範圍 (預設要求該代理程式連續執行)。  
  
> [!WARNING]  
>  在大型批次插入期間複寫觸發程序引發一次，不適用於每個資料列的插入。 這可能會導致 insert 陳述式失敗例如識別範圍用盡時，大量插入， **INSERT INTO** 陳述式。  
  
|[名稱]|範圍|  
|---------------|-----------|  
|**tinyint**|不支援自動管理|  
|**smallint**|-2^15 (-32,768) 到 2^15-1 (32,767)|  
|**int**|-2^31 (-2,147,483,648) 到 2^31-1 (2,147,483,647)|  
|**bigint**|-2^63 (-9,223,372,036,854,775,808) 到 2^63-1 (9,223,372,036,854,775,807)|  
|**十進位** 和 **數值**|-10^38+1 到 10^38-1|  
  
> [!NOTE]  
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱[序號](../../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
### 合併式複寫  
 識別範圍由「發行者」管理，並由「合併代理程式」傳播至「訂閱者」(在重新發行階層中，範圍由根「發行者」與重新發行者管理)。 識別值從「發行者」端的集區指派。 當您將具有識別資料行的發行項加入發行集在新增發行集精靈或使用 [sp_addmergearticle & #40。TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), ，您指定的值︰  
  
-   **@Identity_range** 參數，控制最初配置給發行者和訂閱者，具有主訂閱的識別範圍大小。  
  
    > [!NOTE]  
    >  執行舊版的 「 訂閱者 」 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ，此參數 (而非 **@pub_identity_range** 參數) 也會控制重新發行訂閱者的識別範圍大小。  
  
-    **@Pub_identity_range** 參數，控制配置給 「 訂閱者 」 具有主訂閱 （需要重新發行資料） 的識別範圍大小。 所有具有主訂閱的「訂閱者」都會收到重新發行的範圍，即使它們實際並未重新發行資料。  
  
-    **@Threshold** 參數，用於判斷何時的訂閱需要新的識別範圍 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 或舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 例如，您可以指定為 10000 **@identity_range** 500000 **@pub_identity_range**。 「 發行者 」 和所有 「 訂閱者 」 執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本，包括具有主訂閱，「 訂閱者 」 指派 10000 的主要範圍。 具有主訂閱的 「 訂閱者 」 也會被指派 500000，可供同步處理與重新發行訂閱者的訂閱者的主要範圍 (您也必須指定 **@identity_range**, ，**@pub_identity_range**, ，和 **@threshold** 重新發行訂閱者端發行集中發行項)。  
  
 每個 「 訂閱者 」 執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本也會收到次要識別範圍。 次要範圍的大小等於主要範圍；當主要範圍用盡時，就會使用次要範圍，並且「合併代理程式」會為「訂閱者」指派新的範圍。 新範圍隨即成為次要範圍，且當「訂閱者」使用識別值時處理會繼續。  
  
  
### 具有佇列更新訂閱的異動複寫  
 識別範圍由「散發者」管理，並由「散發代理程式」傳播至「訂閱者」。 識別值從「散發者」端的集區指派。 集區大小基於資料類型的大小以及用於識別欄位的遞增值。 當您將具有識別資料行的發行項加入發行集在新增發行集精靈或使用 [sp_addarticle & #40。TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), ，您指定的值︰  
  
-    **@Identity_range** 參數，控制最初配置給所有訂閱者的識別範圍大小。  
  
-    **@Pub_identity_range** 參數，控制配置給 「 發行者 」 端的識別範圍大小。  
  
-    **@Threshold** 參數，用於判斷何時訂閱需要新的識別範圍。  
  
 例如，您可以指定為 10000 **@pub_identity_range**, 、 1000年 **@identity_range** （假設較少更新 「 訂閱者 」），以及 80%的 **@threshold**。 在「訂閱者」端執行 800 次插入 (1000 的 80%) 之後，將為「訂閱者」指派新範圍。 在「發行者」端執行 8000 次插入之後，將為「發行者」指派新範圍。 指派新範圍時，資料表裡的識別範圍值中會有一個間隔。 指定的臨界值越高間距就越小，但系統的容錯功能也就越弱：如果「散發代理程式」因某種原因無法執行，「訂閱者」可能更容易用盡識別。  
  
## 為手動識別範圍管理指派範圍  
 如果指定手動識別範圍管理，則必須確定「發行者」與每個「訂閱者」都使用不同的識別範圍。 例如，考慮識別欄位定義為 `IDENTITY(1,1)` 之「發行者」端的資料表：識別欄位從 1 開始，每插一個資料列即遞增 1。 如果「發行者」端的資料表有 5,000 個資料列，而您希望在應用程式使用期間資料表有所成長，「發行者」可以使用範圍 1-10,000。 假設有兩個「訂閱者」，「訂閱者 A」可以使用 10,001–20,000，「訂閱者 B」可以使用 20,001-30,000。  
  
 在「訂閱者」透過快照集或其他方式初始化之後，執行 DBCC CHECKIDENT 以為「訂閱者」指派識別範圍的起點。 例如，在「訂閱者 A」端，應執行 `DBCC CHECKIDENT('<TableName>','reseed',10001)`。 在訂閱者 B，您應執行 `CHECKIDENT('<TableName>','reseed',20001)`。  
  
 若要指派新範圍至「發行者」或「訂閱者」，請執行 DBCC CHECKIDENT 並指定新值以重設資料表的種子資料。 您應該採用某種方式來確定必須在何時指派新範圍。 例如，您的應用程式可能有一個機制，可以偵測節點將用盡其範圍的時間，並使用 DBCC CHECKIDENT 指派新範圍。 您也可以新增檢查條件約束，以確保在可能超出識別值使用範圍的情況下無法再新增資料列。  
  
## 在資料庫還原後處理識別範圍  
 如果使用自動識別範圍管理，則「訂閱者」從備份還原時，會自動要求新的識別範圍值。 如果「發行者」從備份還原，您必須確定為該「發行者」指派了適當的範圍。 合併式複寫指派新範圍使用 [sp_restoremergeidentityrange & #40。TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql.md)。 對於異動複寫，先確定已使用的最大值，然後設定新範圍的起點。 在發行集資料庫還原後使用下列程序：  
  
1.  停止所有「訂閱者」上的所有活動。  
  
2.  對於每個包括識別欄位的已發行資料表：  
  
    1.  在每個「訂閱者」端的訂閱資料庫中，執行 `IDENT_CURRENT('<TableName>')`。  
  
    2.  記錄所有「訂閱者」中找到的最大值。  
  
    3.  在「發行者」端的發行集資料庫中，執行 `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`)。  
  
    4.  在發行者端發行集資料庫中，執行 `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`。  
  
    > [!NOTE]  
    >  如果識別欄位中的值設定為遞減而非遞增，請記錄找到的最小值，然後用該值重設種子資料。  
  
## 另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [DBCC CHECKIDENT & #40。TRANSACT-SQL &#41;](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_CURRENT & #40。TRANSACT-SQL &#41;](../../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../Topic/IDENTITY%20\(Property\)%20\(Transact-SQL\).md)   
 [sp_adjustpublisheridentityrange & #40。TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)  
  
  