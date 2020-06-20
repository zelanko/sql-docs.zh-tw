---
title: 複寫識別資料行 | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c899d902e403e9f7cdbdfd1a83cde110e627ab11
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060411"
---
# <a name="replicate-identity-columns"></a>複寫識別欄位
  將 IDENTITY 屬性指派給資料行時，[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會自動為含有識別欄位之資料表的新資料列產生序號。 如需詳細資訊，請參閱 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)。 由於識別欄位可能會做為主索引鍵的一部分，因此請務必避免在識別欄位中重複值。 若要在具有多個節點更新的複寫拓撲裡使用識別欄位，複寫拓撲中的每個節點必須使用不同的識別值範圍，以免出現重複。  
  
 例如，「發行者」可指派範圍 1-100、訂閱者 A 指派範圍 101-200，訂閱者 B 則指派範圍 201-300。 如果在「發行者」插入資料列，而且識別值是 65，該值就會複寫到每個「訂閱者」。 當複寫在每個「訂閱者」端插入資料時，不會遞增「訂閱者」資料表中的識別欄位值，而是插入常值 65。 只有使用者插入會導致識別欄位值遞增，複寫代理程式插入則不會。  
  
 複寫會處理所有發行集與訂閱類型的識別欄位，讓您能夠手動管理資料行，或者讓複寫自動管理這些資料行。  
  
> [!NOTE]  
>  不支援在已發行的資料表上加入識別欄位，因為可能在資料行複寫至「訂閱者」時，導致無法聚合。 簽發者端識別欄位中的值，隨著受影響的資料表之資料列的實際儲存順序而不同。 資料列可能以不同方式儲存在訂閱者端；因此識別欄位的值可能與同資料列的不同。  
  
## <a name="specifying-an-identity-range-management-option"></a>指定識別範圍管理選項  
 複寫提供三個識別範圍管理選項：  
  
-   自動。 用於「訂閱者」端更新的合併式複寫與異動複寫。 指定「發行者」與「訂閱者」的大小範圍，複寫會自動管理新範圍的指派。 複寫還會為「訂閱者」端的識別欄位設定 NOT FOR REPLICATION 選項，以便只有使用者插入會導致值在「訂閱者」端遞增。  
  
    > [!NOTE]  
    >  「訂閱者」必須與「發行者」同步，方可接收新範圍。 由於「訂閱者」的識別範圍是自動指派的，因此如果反覆要求新範圍，任何「訂閱者」都可能用盡整個識別範圍。  
  
-   手動。 用於「訂閱者」端沒有更新的快照式與異動複寫、點對點異動複寫，或者是應用程式必須程式化控制識別範圍的情況。 如果指定手動管理，必須確定範圍指派到了「發行者」與每個「訂閱者」，並在使用初始範圍時指派新範圍。 複寫會為「訂閱者」端的識別欄位設定 NOT FOR REPLICATION 選項。  
  
-   無。 此選項僅建議用於與舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的回溯相容性，並且僅在交易式發行集的預存程序介面可用。  
  
 若要指定識別範圍管理選項，請參閱[管理識別資料行](manage-identity-columns.md)。  
  
## <a name="assigning-identity-ranges"></a>指派識別範圍  
 合併式複寫與異動複寫使用不同的方法指派範圍；這些方法在本節中均有描述。  
  
 複寫識別欄位時要考慮兩種範圍：指派至「發行者」與「訂閱者」的範圍，以及資料行中資料類型的範圍。 下表顯示識別欄位中通常使用之資料類型可用的範圍。 範圍用於拓撲中的所有節點。 例如，如果您使用 `smallint` 從1開始，增量為1，則最大的插入數為32767，代表發行者和所有訂閱者。 插入的實際數目取決於使用的值中是否有間距，以及是否使用臨界值。 如需臨界值的詳細資訊，請參閱下列的「合併式複寫」和「具有佇列更新訂閱的異動複寫」各節。  
  
 如果「發行者」在插入之後用盡了其識別範圍，則在 **db_owner** 固定資料庫角色的成員執行插入時，可自動指派新範圍。 如果執行插入的使用者並非該角色，則「記錄讀取器代理程式」、「合併代理程式」或屬於 **db_owner** 角色成員的使用者必須執行 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql)。 對於異動複寫，「記錄讀取器代理程式」必須執行才能自動配置新範圍 (預設要求該代理程式連續執行)。  
  
> [!WARNING]  
>  在大型批次插入期間，複寫觸發程序只會引發一次，而不會針對插入的每個資料列引發。 如果在大型插入 (例如 `INSERT INTO` 陳述式) 期間用盡了識別範圍，這可能會導致 Insert 陳述式失敗。  
  
|資料類型|範圍|  
|---------------|-----------|  
|`tinyint`|不支援自動管理|  
|`smallint`|-2^15 (-32,768) 到 2^15-1 (32,767)|  
|`int`|-2^31 (-2,147,483,648) 到 2^31-1 (2,147,483,647)|  
|`bigint`|-2^63 (-9,223,372,036,854,775,808) 到 2^63-1 (9,223,372,036,854,775,807)|  
|`decimal` 和 `numeric`|-10^38+1 到 10^38-1|  
  
> [!NOTE]  
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../../sequence-numbers/sequence-numbers.md)。  
  
### <a name="merge-replication"></a>合併式複寫  
 識別範圍由「發行者」管理，並由「合併代理程式」傳播至「訂閱者」(在重新發行階層中，範圍由根「發行者」與重新發行者管理)。 識別值從「發行者」端的集區指派。 您在 [新增發行集精靈] 中或使用 [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 將具有識別欄位的發行項新增至發行集時，指定下列的值：  
  
-   ** \@ Identity_range**參數，控制最初配置給「發行者」的識別範圍大小，以及具有用戶端訂閱的「訂閱者」。  
  
    > [!NOTE]  
    >  對於執行舊版的「訂閱者」 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ，此參數（而非** \@ pub_identity_range**參數）也會控制重新發行訂閱者端的識別範圍大小。  
  
-   ** \@ Pub_identity_range**參數，控制配置給具有伺服器訂閱之訂閱者的重新發行的識別範圍大小（重新發行資料所需）。 所有具有主訂閱的「訂閱者」都會收到重新發行的範圍，即使它們實際並未重新發行資料。  
  
-   ** \@ 臨界值**參數，用來判斷訂用帳戶或舊版的訂閱何時需要新的識別範圍 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
 例如，您可以指定10000做為** \@ identity_range** ，而500000用於** \@ pub_identity_range**。 執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的發行者和所有訂閱者 (包括具有主訂閱的訂閱者) 都會被指派 10000 的主要範圍。 具有伺服器訂閱的訂閱者也會被指派500000的主要範圍，這可供與重新發行訂閱者同步處理的訂閱者使用（您也必須為重新發行訂閱者端之發行集中的發行項指定** \@ identity_range**、 ** \@ pub_identity_range**和** \@ 臨界值**）。  
  
 執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本的每一個訂閱者還會收到次要識別範圍。 次要範圍的大小等於主要範圍；當主要範圍用盡時，就會使用次要範圍，並且「合併代理程式」會為「訂閱者」指派新的範圍。 新範圍隨即成為次要範圍，且當「訂閱者」使用識別值時處理會繼續。  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>具有佇列更新訂閱的異動複寫  
 識別範圍由「散發者」管理，並由「散發代理程式」傳播至「訂閱者」。 識別值從「散發者」端的集區指派。 集區大小基於資料類型的大小以及用於識別欄位的遞增值。 您在 [新增發行集精靈] 中或使用 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 將具有識別欄位的發行項新增至發行集時，指定下列的值：  
  
-   ** \@ Identity_range**參數，控制最初配置給所有訂閱者的識別範圍大小。  
  
-   ** \@ Pub_identity_range**參數，控制配置給發行者的識別範圍大小。  
  
-   ** \@ 臨界值**參數，用於判斷訂閱何時需要新的識別範圍。  
  
 例如，您可以為** \@ pub_identity_range**指定10000， ** \@ identity_range**為1000（假設在「訂閱者」端有較少的更新），並針對「 ** \@ 閾值**」的80百分比。 在「訂閱者」端執行 800 次插入 (1000 的 80%) 之後，將為「訂閱者」指派新範圍。 在「發行者」端執行 8000 次插入之後，將為「發行者」指派新範圍。 指派新範圍時，資料表裡的識別範圍值中會有一個間隔。 指定的臨界值越高間距就越小，但系統的容錯功能也就越弱：如果「散發代理程式」因某種原因無法執行，「訂閱者」可能更容易用盡識別。  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>為手動識別範圍管理指派範圍  
 如果指定手動識別範圍管理，則必須確定「發行者」與每個「訂閱者」都使用不同的識別範圍。 例如，考慮識別欄位定義為 `IDENTITY(1,1)`之「發行者」端的資料表：識別欄位從 1 開始，每插一個資料列即遞增 1。 如果「發行者」端的資料表有 5,000 個資料列，而您希望在應用程式使用期間資料表有所成長，「發行者」可以使用範圍 1-10,000。 假設有兩個「訂閱者」，「訂閱者 A」可以使用 10,001-20,000，「訂閱者 B」可以使用 20,001-30,000。  
  
 在「訂閱者」透過快照集或其他方式初始化之後，執行 DBCC CHECKIDENT 以為「訂閱者」指派識別範圍的起點。 例如，在「訂閱者 A」端，應執行 `DBCC CHECKIDENT('<TableName>','reseed',10001)`。 在「訂閱者 B」端，應執行 `CHECKIDENT('<TableName>','reseed',20001)`。  
  
 若要指派新範圍至「發行者」或「訂閱者」，請執行 DBCC CHECKIDENT 並指定新值以重設資料表的種子資料。 您應該採用某種方式來確定必須在何時指派新範圍。 例如，您的應用程式可能有一個機制，可以偵測節點將用盡其範圍的時間，並使用 DBCC CHECKIDENT 指派新範圍。 您也可以新增檢查條件約束，以確保在可能超出識別值使用範圍的情況下無法再新增資料列。  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>在資料庫還原後處理識別範圍  
 如果使用自動識別範圍管理，則「訂閱者」從備份還原時，會自動要求新的識別範圍值。 如果「發行者」從備份還原，您必須確定為該「發行者」指派了適當的範圍。 對於合併式複寫，請使用 [sp_restoremergeidentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql) 指派新的範圍。 對於異動複寫，先確定已使用的最大值，然後設定新範圍的起點。 在發行集資料庫還原後使用下列程序：  
  
1.  停止所有「訂閱者」上的所有活動。  
  
2.  對於每個包括識別欄位的已發行資料表：  
  
    1.  在每個「訂閱者」端的訂閱資料庫中，執行 `IDENT_CURRENT('<TableName>')`。  
  
    2.  記錄所有「訂閱者」中找到的最大值。  
  
    3.  在「發行者」端的發行集資料庫中，執行 `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`)。  
  
    4.  在「發行者」端的發行集資料庫中，執行 `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`。  
  
    > [!NOTE]  
    >  如果識別欄位中的值設定為遞減而非遞增，請記錄找到的最小值，然後用該值重設種子資料。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [DBCC CHECKIDENT &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)   
 [IDENT_CURRENT &#40;Transact-sql&#41;](/sql/t-sql/functions/ident-current-transact-sql)   
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql)  
  
  
