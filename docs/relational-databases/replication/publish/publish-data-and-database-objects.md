---
title: "發行資料和資料庫物件 | Microsoft Docs"
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
  - "使用者定義型別 [SQL Server 複寫]"
  - "發行項 [SQL Server 複寫], 卸除"
  - "物件 [SQL Server 複寫]"
  - "發行集 [SQL Server 複寫], 建立"
  - "合併式複寫 [SQL Server 複寫], 發行集"
  - "僅限結構描述發行項 [SQL Server 複寫]"
  - "發行 [SQL Server 複寫], 資料庫物件"
  - "發行項 [SQL Server 複寫], 定義"
  - "發行 [SQL Server 複寫], 函數"
  - "複寫 [SQL Server 複寫], 發行集"
  - "發行 [SQL Server 複寫], 檢視"
  - "資料表 [SQL Server 複寫]"
  - "結構描述 [SQL Server 複寫]"
  - "發行 [SQL Server 複寫], 資料"
  - "結構描述 [SQL Server 複寫], 發行"
  - "發行項 [SQL Server 複寫], 預存程序和"
  - "發行 [SQL Server 複寫], 資料表"
  - "別名資料類型 [SQL Server 複寫]"
  - "發行集 [SQL Server 複寫], 刪除"
  - "快照式複寫 [SQL Server 複寫], 發行集"
  - "發行項 [SQL Server 複寫], 修改"
  - "異動複寫, 發行集"
  - "發行 [SQL Server 複寫], 預存程序"
  - "發行 [SQL Server 複寫]"
  - "檢視 [SQL Server 複寫]"
  - "預存程序 [SQL Server 複寫], 發行"
  - "發行集 [SQL Server 複寫], 結構描述選項"
  - "發行項 [SQL Server 複寫], 加入"
  - "發行集 [SQL Server 複寫]，修改"
  - "使用者自訂函數 [SQL Server 複寫]"
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 83
---
# 發行資料和資料庫物件
  在建立發行集時，您可以選擇想要發行的資料表和其他資料庫物件。 您可以使用複寫發行下列資料庫物件。  
  
|資料庫物件|快照式複寫和異動複寫|合併式複寫|  
|---------------------|--------------------------------------------------------|-----------------------|  
|資料表|X|X|  
|分割區資料表|X|X|  
|預存程序 – 定義 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR)|X|X|  
|預存程序 – 執行 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR)|X|否|  
|檢視|X|X|  
|索引檢視表|X|X|  
|將索引檢視表做為資料表|X|否|  
|使用者自訂類型 (CLR)|X|X|  
|使用者定義函數 ([!INCLUDE[tsql](../../../includes/tsql-md.md)] 和 CLR)|X|X|  
|別名資料類型|X|X|  
|全文檢索索引|X|X|  
|結構描述物件 (條件約束、索引、使用者 DML 觸發程序、擴充屬性和定序)|X|X|  
  
## 建立發行集  
 若要建立發行集，您需提供下列資訊：  
  
-   散發者。  
  
-   快照集檔案的位置。  
  
-   發行集資料庫。  
  
-   要建立之發行集的類型 (快照式、交易式、具有可更新訂閱的交易式，或合併式)。  
  
-   發行集中的資料及資料庫物件 (發行項)。  
  
-   所有發行集類型的靜態資料列篩選和資料行篩選，以及參數化資料列篩選器與合併式發行集的聯結篩選。  
  
-   快照集代理程式排程。  
  
-   將執行下列代理程式的帳戶：所有發行集的快照集代理程式；所有交易式發行集的記錄讀取器代理程式；可允許更新訂閱之交易式發行集的佇列讀取器代理程式  
  
-   發行集的名稱及描述。  
  
 如需有關如何使用發行集的資訊，請參閱下列主題：  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [檢視及修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [刪除發行集](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [刪除發行項](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  刪除發行項或發行集不會從「訂閱者」移除物件。  
  
## 發行資料表  
 最常見的已發行物件是資料表。 下列連結提供發行資料表相關方面的其他資訊：  
  
-   [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [異動複寫的發行項選項](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [合併式複寫的發行項選項](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [複寫識別欄位](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 在為複寫發行資料表時，您可以指定應複製到「訂閱者」的結構描述物件，例如宣告參考完整性 (主索引鍵條件約束、參考條件約束、唯一條件約束)、索引、使用者 DML 觸發程序 (無法複寫 DDL 觸發程序)、擴充屬性和定序。 只在發行者與訂閱者之間的初始同步處理中複寫擴充屬性。 如果您在初始同步處理之後加入或修改擴充屬性，就不會複寫這項變更。  
  
 若要指定結構描述選項，請參閱 [指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md) 或 <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>。  
  
### 分割資料表與索引  
 複寫支援分割區資料表和索引的發行。 支援的層級取決於所使用的複寫類型，以及您針對與分割區資料表有關的發行集和發行項所指定的選項。 如需詳細資訊，請參閱 [複寫資料分割資料表和索引](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
## 發行預存程序  
 所有類型的複寫都允許您複寫預存程序定義：CREATE PROCEDURE 會複製到每個訂閱者。 在使用 Common Language Runtime (CLR) 預存程序時，還將複製相關組件。 對程序所作的變更會被複寫到「訂閱者」；而對相關組件所作的變更則不會。  
  
 除複寫預存程序的定義外，異動複寫還可讓您複寫預存程序的執行。 針對會影響大量資料的維護導向預存程序複寫結果時很有用。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
## 發行檢視表  
 所有類型的複寫都可讓您複寫檢視。 檢視 (及其隨附的索引，如果它是索引檢視表的話) 可被複製到「訂閱者」，但必須同時複寫基底資料表。  
  
 對於索引檢視表，異動複寫也可讓您以資料表而不是檢視複寫索引檢視表，不需要複寫基底資料表。 若要這樣做，請指定"indexed 的 view logbased"選項的其中一個 *@type* 參數 [sp_addarticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 如需有關使用 **sp_addarticle**, ，請參閱 [定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## 發行使用者自訂函數  
 CLR 函數和 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 函數的 CREATE FUNCTION 陳述式會複製到每一個訂閱者。 如果使用 CLR 函數，還將複製相關組件。 對函數所作的變更會被複寫到「訂閱者」；而對相關組件所作的變更則不會。  
  
## 發行使用者自訂類型和別名資料類型  
 使用使用者自訂類型或別名資料類型的資料行，同其他資料行一樣都會被複寫到「訂閱者」。 建立 TYPEstatement 每個複寫類型會在建立資料表之前，執行 「 訂閱者 」。 如果使用使用者自訂類型，相關組件還將被複製到每個「訂閱者」。 對使用者自訂類型與別名資料類型所作的變更將不會被複寫到「訂閱者」。  
  
 如果類型在資料庫中定義，但它在建立發行集時未在任何資料行中參考，則不會將此類型複製到「訂閱者」。 如果您後續將在資料庫中建立該類型的資料行並且想要複寫它，則必須先手動將此類型 (以及使用者自訂類型的相關組件) 複製到每個「訂閱者」。  
  
## 發行全文檢索索引  
 CREATE FULLTEXT INDEX 陳述式會被複製到每個訂閱者，且全文檢索索引會在訂閱者上建立。 使用 ALTER FULLTEXT INDEX 所做的全文檢索索引變更則不會複寫。  
  
## 對已發行物件進行結構描述變更  
 複寫支援對已發行物件進行大範圍的結構描述變更。 當您對「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者」端適當的已發行物件進行下列任何結構描述變更時，依預設，該變更會傳播給所有的「[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 如需詳細資訊，請參閱 [對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## 發行考量  
 在發行資料庫物件時，注意下列問題：  
  
-   在建立發行集和初始快照集時使用者可以存取資料庫，但建議在「發行者」上的活動較少時建立發行集。  
  
-   在資料庫中建立發行集後，就無法重新命名資料庫。 若要重新命名，您必須先從資料庫中移除複寫。  
  
-   如果您發行的資料庫物件相依於一或多個其他資料庫物件，就必須發行所有參考物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
    > [!NOTE]  
    >  如果您將發行項加入至合併式發行集現有的發行項新的發行項而定，您必須指定兩個發行項使用的處理順序 **@processing_order** 參數 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。 請考慮下列狀況：您發行資料表但未發行該資料表所參考的函數。 如果您未發行該函數，該資料表就無法在「訂閱者」端建立。 當您將函數加入發行集︰ 指定的值為 **1** 的 **@processing_order** 參數 **sp_addmergearticle**; 並指定其值為 **2** 的 **@processing_order** 參數 **sp_changemergearticle**, ，指定參數的資料表名稱 **@article**。 此處理順序可確保您先在「訂閱者」端建立函數之後才建立相依於此函數的資料表。 您可對每個發行項使用不同的編號，只要函數的編號低於資料表的編號即可。  
  
-   發行集名稱不能包含下列字元：% * [ ] | : " ? \ / \< >.  
  
### 發行物件的限制  
  
-   可發行的發行項和資料行數目上限，會因發行集類型而異。 如需詳細資訊，請參閱 「 複寫物件 」 一節 [適用於 SQL Server 的最大容量規格](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)。  
  
-   定義為 WITH ENCRYPTION 的預存程序、檢視表、觸發程序及使用者定義函數無法當做 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫的一部分發行。  
  
-   可以複寫 XML 結構描述集合，但無法在初始快照集後複寫變更。  
  
-   為異動複寫發行的資料表必須有一個主索引鍵。 如果資料表在異動複寫發行集中，您便無法停用關聯於主索引鍵資料行的任何索引。 複寫需要這些索引。 若要停用索引，您必須先從發行集中卸除資料表。  
  
-   繫結預設值，以建立 [sp_bindefault & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) 不會複寫 （繫結預設值已經棄用使用 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 關鍵字建立）。  
  
-   函式包含 **NOEXPAND** 索引檢視表上的提示內，無法發行同一個發行集，做為參考的資料表和索引檢視表，由於中散發代理程式傳送的順序。 若要解決這個問題，將資料表和索引檢視表建立放在第一個發行集，並加入函式包含 **NOEXPAND** 第二個發行集後第一個發行集發行索引檢視表上的提示完成。 或者，建立這些函式的指令碼和指令碼使用傳遞 *@post_snapshot_script* 參數 **sp_addpublication**。  
  
### 結構描述和物件擁有權  
 針對結構描述和物件擁有權，複寫在新增複寫精靈中具有下列預設行為：  
  
-   針對合併式發行集內相容性層級等於或超過 90 的發行項、快照集發行集以及交易式發行集：依預設，訂閱者的物件擁有者與發行者內對應物件的擁有者相同。 若擁有物件的結構描述不存在於訂閱者中，則會自動建立。  
  
-   在合併式發行集相容性層級低於 90 的發行項︰ 根據預設，擁有者保留空白並指定為 **dbo** 期間建立的 「 訂閱者 」 上的物件。  
  
-   在 Oracle 發行集的發行項︰ 根據預設，擁有者指定為 **dbo**。  
  
-   針對使用字元模式快照集之發行集內的發行項 (用於非 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者和 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 訂閱者)：依預設，會將擁有者保留空白。 擁有者預設為與散發代理程式或合併代理程式用於連接到訂閱者之帳戶相關聯的擁有者。  
  
 物件擁有者可以透過變更 **發行項屬性-\<***文章***>** ] 對話方塊中，透過下列預存程序︰ **sp_addarticle**, ，**sp_addmergearticle**, ，**sp_changearticle**, ，和 **sp_changemergearticle**。 如需詳細資訊，請參閱 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), ，[定義發行項](../../../relational-databases/replication/publish/define-an-article.md), ，和 [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
### 將資料發行給執行舊版 SQL Server 的訂閱者  
  
-   如果您要發行到執行舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的「訂閱者」，則在複寫特定功能以及產品整體功能方面都將受該版本的功能限制。  
  
-   合併式發行集使用相容性層級，用於判斷可在發行集中使用的功能，並可讓您支援執行舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的「訂閱者」。  
  
### 在多個發行集中發行資料表  
 複寫支援下列限制下的在多個發行集中發行資料項 (包括重新發行資料)：  
  
-   如果發行項在交易式發行集和合併式發行集，請確認 *@published_in_tran_pub* 的合併發行項屬性設定為 TRUE。 如需設定屬性的詳細資訊，請參閱 [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) 和 [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
     您也應該設定 *@published_in_tran_pub* 如果發行項是交易式訂閱的一部分，且包含在合併式發行集的屬性。 在此情況下，請留意，依預設異動複寫預期訂閱者端的資料表是唯讀的；如果合併式複寫對交易式訂閱中的資料表進行資料變更，資料可能會無法聚合。 若要避免此可能性，建議合併式發行集中的任何此類資料表應指定為僅限下載。 這會防止合併式訂閱者將資料變更上傳至資料表。 如需詳細資訊，請參閱 [最佳化合併式複寫效能的 「 文章](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   無法在合併式發行集與交易式發行集中發行具有佇列更新訂閱的發行項。  
  
-   無法重新發行包含於支援更新訂閱之交易式發行集中的發行項。  
  
-   如果在支援佇列更新訂閱的多個交易式發行集中發行發行項，則在所有發行集中之發行項的下列屬性值必須相同：  
  
    |屬性|sp_addarticle 中的參數|  
    |--------------|---------------------------------|  
    |識別範圍管理|**@auto_identity_range** （已過時） 和 **@identityrangemangementoption**|  
    |發行者識別範圍|**@pub_identity_range**|  
    |識別範圍|**@identity_range**|  
    |識別範圍臨界值|**@threshold**|  
  
     如需有關這些參數的詳細資訊，請參閱 [sp_addarticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
-   如果在多個合併式發行集中發行發行項，則在所有發行集中之發行項的下列屬性值必須相同：  
  
    |屬性|sp_addmergearticle 中的參數|  
    |--------------|--------------------------------------|  
    |資料行追蹤|**@column_tracking**|  
    |結構描述選項|**@schema_option**|  
    |資料行篩選|**@vertical_partition**|  
    |訂閱者上傳選項|**@subscriber_upload_options**|  
    |條件式刪除追蹤|**@delete_tracking**|  
    |錯誤補償|**@compensate_for_errors**|  
    |識別範圍管理|**@auto_identity_range** （已過時） 和 **@identityrangemangementoption**|  
    |發行者識別範圍|**@pub_identity_range**|  
    |識別範圍|**@identity_range**|  
    |識別範圍臨界值|**@threshold**|  
    |資料分割選項|**@partition_options**|  
    |Blob 資料行資料流|**@stream_blob_columns**|  
    |篩選類型|**@filter_type** (參數 **sp_addmergefilter**)|  
  
     如需有關這些參數的詳細資訊，請參閱 [sp_addmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。  
  
-   異動複寫和未篩選的合併式複寫支援在多個發行集中發行資料表，然後在訂閱資料庫中的單一資料表內進行訂閱 (通常稱為積存狀況)。 積存通常用於從中央訂閱者端一個資料表中的多個位置彙總資料子集。 篩選的合併式發行集不支援中央「訂閱者」狀況。 對於合併式複寫，積存通常透過具有參數化資料列篩選器的單一發行集實作。 如需詳細資訊，請參閱 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md)。  
  
## 另請參閱  
 [在現有發行集中加入和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [設定散發](../../../relational-databases/replication/configure-distribution.md)   
 [初始化訂閱](../../../relational-databases/replication/initialize-a-subscription.md)   
 [編寫複寫指令碼](../../../relational-databases/replication/scripting-replication.md)   
 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  