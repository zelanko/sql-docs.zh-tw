---
title: Oracle 發行者的設計考量與限制 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], design considerations and limitations
ms.assetid: 8d9dcc59-3de8-4d36-a61f-bc3ca96516b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 043bf26fb17a3433e59623b5b3bfddaaea8bc89f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022518"
---
# <a name="design-considerations-and-limitations-for-oracle-publishers"></a>Oracle 發行者的設計考量與限制
  從 Oracle 資料庫發行和從 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫發行的設計幾乎相同。 但應該注意下列限制和問題：  
  
-   Oracle Gateway 選項提供比 Oracle Complete 選項更好的效能；不過此選項不可用於多個交易式發行集內發行同一資料表。 資料表最多可以出現在單一交易式發行集，以及任意多個快照集發行集內。 若您需要在多個交易式發行集內發行同一資料表，請選擇 Oracle Complete 選項。  
  
-   複寫支援發行資料表、索引及具體化檢視， 但不會複寫其他物件。  
  
-   儲存及處理 Oracle 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫中資料的方式略有不同，這些差異會影響到複寫。  
  
-   使用「Oracle 發行者」時所支援的異動複寫功能會有一些差異。  
  
## <a name="support-for-publishing-objects-from-oracle"></a>支援從 Oracle 發行物件  
 複寫支援從 Oracle 資料庫複寫下列物件：  
  
-   資料表  
  
-   按索引組織的資料表  
  
-   索引  
  
-   具體化檢視 (複寫為資料表)  
  
 下列物件可存在於發行資料表中但不會被複寫：  
  
-   網域型索引  
  
-   功能型索引  
  
-   預設值  
  
-   檢查條件約束  
  
-   外部索引鍵  
  
-   儲存選項 (資料表空間、叢集等)  
  
 無法複寫下列物件：  
  
-   巢狀資料表  
  
-   檢視  
  
-   封裝、封裝主體、程序及觸發程序  
  
-   佇列  
  
-   序列  
  
-   同義字  
  
 如需有關支援之資料類型的資訊，請參閱＜ [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)＞。  
  
## <a name="differences-between-oracle-and-sql-server"></a>Oracle 和 SQL Server 之間的差異  
  
-   Oracle 對某些物件的大小上限限制有所不同。 在 Oracle 發行集資料庫中建立的所有物件均應遵守 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中相應物件的大小上限限制。 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中限制的資訊，請參閱 [SQL Server 的最大容量規格](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)。  
  
-   依預設，Oracle 物件名稱以大寫方式建立。 如果 Oracle 資料庫中的物件名稱為大寫，則透過「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者」發行 Oracle 物件時，請確定以大寫方式提供其名稱。 如果指定的物件名稱大小寫不正確，可能會產生錯誤訊息，提示找不到該物件。  
  
-   Oracle 的 SQL 用語和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]略有不同，應在 Oracle 相容語法中寫入資料列篩選。  
  
### <a name="considerations-for-large-objects"></a>大型物件考量  
 大型物件 (LOB) 資料並非儲存在發行項記錄資料表中，LOB 資料的更新一律從發行資料表中直接擷取。 只有當作業造成 LOB 在複寫資料表中引發複寫觸發程序時，才會在交易式發行集中複寫更新。 插入或刪除含有 LOB 的資料列時，會引發 Oracle 觸發程序，但 LOB 資料行的更新不會引發觸發程序。 僅當相同 Oracle 交易中同一資料列的非 LOB 資料行也發生更新時，才會立即複寫 LOB 資料行的更新。 如若不然，當在相同資料列的非 LOB 資料行再次發生更新時，LOB 資料行將在「訂閱者」端重新整理。 請確定您的應用程式接受此行為。  
  
 若要將更新複寫到交易式發行集的 LOB 資料行，請在寫入應用程式時考慮採用下列策略之一：  
  
-   在交易中刪除並重新插入資料列，而不是更新資料列：在重新插入資料列時指定新的 LOB。 由於刪除和插入均會引發觸發程序，因此會複寫資料列。  
  
-   在資料列更新中除 LOB 資料行之外還包含非 LOB 資料行，或做為同一 Oracle 交易的一部份更新資料列的非 LOB 資料行。 在以上兩種情況下，非 LOB 資料行的更新可確保引發觸發程序。  
  
 如需有關 LOB 的詳細資訊，請參閱＜ [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)＞。  
  
### <a name="unique-indexes-and-constraints"></a>唯一索引和條件約束  
 快照式複寫和異動複寫中，唯一索引和條件約束 (包括主索引鍵條件約束) 所包含的資料行必須遵守某些限制。 如果不遵守這些限制，便無法複寫條件約束或索引。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的索引中允許的最大資料行數為 16。  
  
-   唯一條件約束包括的所有資料行必須具有支援的資料類型。 如需有關資料類型的詳細資訊，請參閱＜ [Data Type Mapping for Oracle Publishers](data-type-mapping-for-oracle-publishers.md)＞。  
  
-   必須發行唯一條件約束包括的所有資料行 (無法篩選)。  
  
-   唯一條件約束或索引所含的資料行應為 NULL。  
  
 還需考慮下列問題：  
  
-   Oracle 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 對 NULL 的處理方式不同：對於允許 NULL 值並且包含在唯一條件約束或索引中的資料行，Oracle 允許多個資料列具有 NULL 值。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 則透過在同一資料行中只允許一個具有 NULL 值的資料列來強制其唯一性。 如果發行資料表在索引或條件約束中包含的任何資料行含有多個具有 NULL 值的資料列，則由於「訂閱者」端會發生條件約束違規，您將無法發行允許 NULL 的唯一條件約束或索引。  
  
-   測試唯一性時， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會忽略欄位的尾端空白，而 Oracle 則不會。  
  
 與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 異動複寫相同，Oracle 異動複寫發行集中的資料表也需要主索引鍵。根據以上指定的規則，主索引鍵必須唯一。 如果主索引鍵不遵守之前所述的各項規則，異動複寫將無法發行資料表。  
  
## <a name="differences-between-oracle-publishing-and-standard-transactional-replication"></a>Oracle 發行與標準異動複寫之間的差異  
  
-   「Oracle 發行者」的名稱不能與下列項目的名稱相同：其「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」、使用「散發者」的任何「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者」或任何接收發行集的「訂閱者」。 由相同散發者為其提供服務的各個發行集，都必須分別具有唯一的名稱。  
  
-   在 Oracle 發行集中發行的資料表無法接收複寫的資料。 因此，Oracle 發行不支援：含立即更新或佇列更新訂閱的發行集，或發行集資料表也做為訂閱資料表的拓撲，例如點對點及雙向複寫。  
  
-   Oracle 資料庫中主索引鍵與外部索引鍵的關聯性不會複寫到「訂閱者」中， 但當傳遞變更時，關聯性會在資料中進行維護。  
  
-   標準異動複寫支援含多達 1000 個資料行的資料表。 Oracle 交易式發行集支援 995 個資料行 (複寫會在每個發行資料表中新增五個資料行)。  
  
-   定序子句會新增到 CREATE TABLE 陳述式中以啟用大小寫比較，此功能對主索引鍵和唯一條件約束很重要。 此行為由結構描述選項 0x1000 控制，該選項使用 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 的 **@schema_option** 參數指定。  
  
-   如果使用預存程序來設定或維護「Oracle 發行者」，請勿在明確交易中使用該程序。 用於連接到「Oracle 發行者」連結伺服器不支援此功能。  
  
-   如果使用精靈建立 Oracle 發行集的提取訂閱，必須使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 和更新版本中提供的「新增訂閱精靈」。 但對於舊版的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，您可以使用預存程序和 SQL-DMO 介面來設定 Oracle 發行集的提取訂閱。  
  
-   如果使用預存程序將變更傳播至「訂閱者」(預設值)，請注意系統支援 MCALL 語法，但當發行集來自「Oracle 發行者」時，其行為有所不同。 通常，MCALL 會提供顯示已在「發行者」端更新資料行的點陣圖。 在 Oracle 發行集中，點陣圖會永遠顯示更新後的所有資料行。 如需使用預存程序的詳細資訊，請參閱[指定交易式發行項變更的傳播方式](../transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
### <a name="transactional-replication-feature-support"></a>異動複寫功能支援  
  
-   Oracle 發行集不支援 SQL Server 發行集所支援的所有結構描述選項。 如需結構描述選項的詳細資訊，請參閱 [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)。  
  
-   Oracle 發行集的「訂閱者」無法使用立即更新或佇列更新訂閱，也無法成為點對點或雙向拓撲的節點。  
  
-   Oracle 發行集的「訂閱者」無法從備份自動初始化。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援兩種類型的驗證：二進位和資料列計數。 「Oracle 發行者」支援資料列數驗證。 如需詳細資訊，請參閱[驗證複寫的資料](../validate-data-at-the-subscriber.md)。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 提供兩種快照集格式：原生 bcp 模式以及字元模式。 「Oracle 發行者」支援字元模式快照集。  
  
-   不支援已發行 Oracle 資料表的結構描述變更。 若要進行結構描述變更，請先卸除發行集，進行變更，然後再重新建立發行集和所有訂閱。  
  
    > [!NOTE]  
    >  如果在發行資料表未發生任何活動時，執行結構描述的變更以及發行集和訂閱的後續卸除及重新建立，則可為訂閱指定 [僅支援複寫] 選項。 此選項可讓上述操作同步進行，無需將快照集複製到每個「訂閱者」端。 如需詳細資訊，請參閱[不使用快照集初始化交易式訂閱](../initialize-a-transactional-subscription-without-a-snapshot.md)。  
  
### <a name="replication-security-model"></a>複寫安全性模型  
 Oracle 發行的安全性模型與標準異動複寫的安全性模型相同，但有下列例外狀況：  
  
-   「快照集代理程式」和「記錄讀取器代理程式」建立從「發散者」至「訂閱者」連接所使用的帳戶透過下列方法之一指定：  
  
    -   [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) 的 **@security_mode** 參數 (如果使用「Oracle 驗證」，還要指定 **@login** 和 **@password** 的值)  
  
    -   位於 SQL Server Management Studio 的 **[連接到伺服器]** 對話方塊中，會在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端設定「Oracle 發行者」時用到。  
  
     在標準異動複寫中，使用 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) 和 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) 指定帳戶。  
  
-   快照集代理程式和記錄讀取器代理程式建立連線所使用的帳戶無法使用 [sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql) 或透過屬性表進行變更，但可以變更密碼。  
  
-   如果將 [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql) 的 **@security_mode** 參數值指定為 1 (Windows 整合式驗證)：  
  
    -   快照集代理程式和記錄讀取器代理程式所使用的處理帳戶和密碼 ([sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) 和 [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql) 的 **@job_login** 和 **@job_password** 參數) 必須與連接到 Oracle 發行者的帳戶和密碼相同。  
  
    -   您無法透過 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql) 或 [sp_changelogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql) 來變更 **@job_login** 參數，但可以變更密碼。  
  
 如需有關複寫安全性的詳細資訊，請參閱 < [SQL Server 複寫安全性](../security/view-and-modify-replication-security-settings.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Oracle 發行者的管理考量](administrative-considerations-for-oracle-publishers.md)   
 [設定 Oracle 發行者](configure-an-oracle-publisher.md)   
 [Oracle 發行概觀](oracle-publishing-overview.md)  
  
  
