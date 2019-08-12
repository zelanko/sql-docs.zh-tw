---
title: 發行資料和資料庫物件 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7c0e87750bb408e617a94185ad85b101e8893711
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769896"
---
# <a name="publish-data-and-database-objects"></a>發行資料和資料庫物件
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
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
  
## <a name="creating-publications"></a>建立發行集  
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
-   [檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)    
-   [檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)    
-   [刪除發行集](../../../relational-databases/replication/publish/delete-a-publication.md)    
-   [刪除發行項](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  刪除發行項或發行集不會從「訂閱者」移除物件。  
  
## <a name="publishing-tables"></a>發行資料表  
 最常見的已發行物件是資料表。 下列連結提供發行資料表相關方面的其他資訊：  
  
-   [篩選發行的資料](../../../relational-databases/replication/publish/filter-published-data.md)    
-   [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)
-   [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)    
-   [複寫識別資料行](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 在為複寫發行資料表時，您可以指定應複製到「訂閱者」的結構描述物件，例如宣告參考完整性 (主索引鍵條件約束、參考條件約束、唯一條件約束)、索引、使用者 DML 觸發程序 (無法複寫 DDL 觸發程序)、擴充屬性和定序。 只在發行者與訂閱者之間的初始同步處理中複寫擴充屬性。 如果您在初始同步處理之後加入或修改擴充屬性，就不會複寫這項變更。  
  
 若要指定結構描述選項，請參閱[指定結構描述選項](../../../relational-databases/replication/publish/specify-schema-options.md)或 <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>。  
  
### <a name="partitioned-tables-and-indexes"></a>分割資料表與索引  
 複寫支援分割區資料表和索引的發行。 支援的層級取決於所使用的複寫類型，以及您針對與分割區資料表有關的發行集和發行項所指定的選項。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。  
  
## <a name="publishing-stored-procedures"></a>發行預存程序  
 所有類型的複寫都允許您複寫預存程序定義：CREATE PROCEDURE 會複製到每個訂閱者。 在使用 Common Language Runtime (CLR) 預存程序時，還將複製相關組件。 對程序所作的變更會被複寫到「訂閱者」；而對相關組件所作的變更則不會。  
  
 除複寫預存程序的定義外，異動複寫還可讓您複寫預存程序的執行。 針對會影響大量資料的維護導向預存程序複寫結果時很有用。 如需詳細資訊，請參閱 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
## <a name="publishing-views"></a>發行檢視表  
 所有類型的複寫都可讓您複寫檢視。 檢視 (及其隨附的索引，如果它是索引檢視表的話) 可被複製到「訂閱者」，但必須同時複寫基底資料表。  
  
 對於索引檢視表，異動複寫也可讓您以資料表而不是檢視複寫索引檢視表，不需要複寫基底資料表。 若要執行此操作，請為 [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 的 *\@type* 參數指定 "indexed view logbased" 選項之一。 如需使用 **sp_addarticle** 的詳細資訊，請參閱[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)。  
  
## <a name="publishing-user-defined-functions"></a>發行使用者自訂函數  
 CLR 函數和 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 函數的 CREATE FUNCTION 陳述式會複製到每一個訂閱者。 如果使用 CLR 函數，還將複製相關組件。 對函數所作的變更會被複寫到「訂閱者」；而對相關組件所作的變更則不會。  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>發行使用者自訂類型和別名資料類型  
 使用使用者自訂類型或別名資料類型的資料行，同其他資料行一樣都會被複寫到「訂閱者」。 每個複寫類型的 CREATE TYPE 陳述式都會在建立資料表之前於訂閱者端執行。 如果使用使用者自訂類型，相關組件還將被複製到每個「訂閱者」。 對使用者自訂類型與別名資料類型所作的變更將不會被複寫到「訂閱者」。  
  
 如果類型在資料庫中定義，但它在建立發行集時未在任何資料行中參考，則不會將此類型複製到「訂閱者」。 如果您後續將在資料庫中建立該類型的資料行並且想要複寫它，則必須先手動將此類型 (以及使用者自訂類型的相關組件) 複製到每個「訂閱者」。  
  
## <a name="publishing-full-text-indexes"></a>發行全文檢索索引  
 CREATE FULLTEXT INDEX 陳述式會被複製到每個訂閱者，且全文檢索索引會在訂閱者上建立。 使用 ALTER FULLTEXT INDEX 所做的全文檢索索引變更則不會複寫。  
  
## <a name="making-schema-changes-to-published-objects"></a>對已發行物件進行結構描述變更  
 複寫支援對已發行物件進行大範圍的結構描述變更。 當您對「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行者」端適當的已發行物件進行下列任何結構描述變更時，依預設，該變更會傳播給所有的「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者」：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。  
  
## <a name="considerations-for-publishing"></a>發行考量  
 在發行資料庫物件時，注意下列問題：  
  
-   在建立發行集和初始快照集時使用者可以存取資料庫，但建議在「發行者」上的活動較少時建立發行集。  
  
-   在資料庫中建立發行集後，就無法重新命名資料庫。 若要重新命名，您必須先從資料庫中移除複寫。  
  
-   如果您發行的資料庫物件相依於一或多個其他資料庫物件，就必須發行所有參考物件。 例如，如果您發行相依於資料表的檢視表，同時也必須發行該資料表。  
  
    > [!NOTE]  
    >  如果您將發行項新增至合併式發行集且現有某發行項相依於新的發行項，則您必須使用 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 的 **\@processing_order** 參數來指定兩個發行項的處理順序。 請考慮下列狀況：您發行資料表但未發行該資料表所參考的函數。 如果您未發行該函數，該資料表就無法在「訂閱者」端建立。 當您將函式新增至發行集時：請將 **sp_addmergearticle** 的 **\@processing_order** 參數值指定為 **1**；並將 **sp_changemergearticle** 的 **\@processing_order** 參數值指定為 **2**，指定 **\@article** 參數的資料表名稱。 此處理順序可確保您先在「訂閱者」端建立函數之後才建立相依於此函數的資料表。 您可對每個發行項使用不同的編號，只要函數的編號低於資料表的編號即可。  
  
-   發行集名稱不能包含下列字元：% * [ ] | : " ? \ / < >.  
  
### <a name="limitations-on-publishing-objects"></a>發行物件的限制  
  
-   可發行的發行項和資料行數目上限，會因發行集類型而異。 如需詳細資訊，請參閱 [SQL Server 的最大容量規格](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)的＜複寫物件＞一節。  
  
-   定義為 WITH ENCRYPTION 的預存程序、檢視表、觸發程序及使用者定義函數無法當做 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫的一部分發行。  
  
-   可以複寫 XML 結構描述集合，但無法在初始快照集後複寫變更。  
  
-   為異動複寫發行的資料表必須有一個主索引鍵。 如果資料表在異動複寫發行集中，您便無法停用關聯於主索引鍵資料行的任何索引。 複寫需要這些索引。 若要停用索引，您必須先從發行集中卸除資料表。  
  
-   不會複寫使用 [sp_bindefault &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) 建立的繫結預設值 (繫結預設值已經棄用，以支援使用 ALTER TABLE 或 CREATE TABLE 的 DEFAULT 關鍵字建立的預設值)。  
  
-   因為散發代理程式傳遞順序的關係，索引檢視表上含有 **NOEXPAND** 提示的函數，不能發行在與參考資料表和索引檢視表相同的發行集中。 若要解決此問題，請將資料表和索引檢視表的建立放在第一個發行集中，然後再將索引檢視表上含有 **NOEXPAND** 提示的函數加入在第一個發行集完成後發行的第二個發行集。 或者，使用 **sp_addpublication** 的 *\@post_snapshot_script* 參數，為這些函式建立指令碼並傳遞指令碼。  
  
### <a name="schemas-and-object-ownership"></a>結構描述和物件擁有權  
 針對結構描述和物件擁有權，複寫在新增複寫精靈中具有下列預設行為：  
  
-   針對合併式發行集內相容性層級等於或超過 90 的發行項、快照集發行集以及交易式發行集：依預設，訂閱者的物件擁有者與發行者內對應物件的擁有者相同。 若擁有物件的結構描述不存在於訂閱者中，則會自動建立。  
  
-   針對相容性層級小於 90 之合併式發行集內的發行項：依預設，會將擁有者保留空白，並在訂閱者上建立物件期間，將其指定為 **dbo** 。  
  
-   針對 Oracle 發行集內的發行項：依預設，會將擁有者指定為 **dbo**。  
  
-   針對使用字元模式快照集之發行集內的發行項 (用於非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 訂閱者和 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 訂閱者)：依預設，會將擁有者保留空白。 擁有者預設為與散發代理程式或合併代理程式用於連接到訂閱者之帳戶相關聯的擁有者。  
  
 物件擁有者可以透過 **[發行項屬性 -\<** <發行項>  **>]** 對話方塊和透過下列預存程序變更︰**sp_addarticle**、**sp_addmergearticle**、**sp_changearticle** 和 **sp_changemergearticle**。 如需詳細資訊，請參閱[檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)、[定義發行項](../../../relational-databases/replication/publish/define-an-article.md)和[檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>將資料發行給執行舊版 SQL Server 的訂閱者  
  
-   如果您要發行到執行舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的「訂閱者」，則在複寫特定功能以及產品整體功能方面都將受該版本的功能限制。  
  
-   合併式發行集使用相容性層級，用於判斷可在發行集中使用的功能，並可讓您支援執行舊版 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的「訂閱者」。  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>在多個發行集中發行資料表  
 複寫支援下列限制下的在多個發行集中發行資料項 (包括重新發行資料)：  
  
-   如果發行項在交易式發行集與合併式發行集中發行，則對於合併發行項，要確保 *\@published_in_tran_pub* 屬性設定為 TRUE。 如需設定屬性的詳細資訊，請參閱[檢視和修改發行集屬性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)和[檢視和修改發行項屬性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
     此外，如果發行項是交易式訂閱的一部分且包含在合併式發行集，您也必須設定 *\@published_in_tran_pub* 屬性。 在此情況下，請留意，依預設異動複寫預期訂閱者端的資料表是唯讀的；如果合併式複寫對交易式訂閱中的資料表進行資料變更，資料可能會無法聚合。 若要避免此可能性，建議合併式發行集中的任何此類資料表應指定為僅限下載。 這會防止合併式訂閱者將資料變更上傳至資料表。 如需詳細資訊，請參閱[使用僅限下載的發行項最佳化合併式複寫效能](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。  
  
-   無法在合併式發行集與交易式發行集中發行具有佇列更新訂閱的發行項。  
  
-   無法重新發行包含於支援更新訂閱之交易式發行集中的發行項。  
  
-   如果在支援佇列更新訂閱的多個交易式發行集中發行發行項，則在所有發行集中之發行項的下列屬性值必須相同：  
  
    |屬性|sp_addarticle 中的參數|  
    |--------------|---------------------------------|  
    |識別範圍管理|**\@auto_identity_range** (已淘汰) 與 **\@identityrangemangementoption**|  
    |發行者識別範圍|**\@pub_identity_range**|  
    |識別範圍|**\@identity_range**|  
    |識別範圍臨界值|**\@threshold**|  
  
     如需這些參數的詳細資訊，請參閱 [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
-   如果在多個合併式發行集中發行發行項，則在所有發行集中之發行項的下列屬性值必須相同：  
  
    |屬性|sp_addmergearticle 中的參數|  
    |--------------|--------------------------------------|  
    |資料行追蹤|**\@column_tracking**|  
    |結構描述選項|**\@schema_option**|  
    |資料行篩選|**\@vertical_partition**|  
    |訂閱者上傳選項|**\@subscriber_upload_options**|  
    |條件式刪除追蹤|**\@delete_tracking**|  
    |錯誤補償|**\@compensate_for_errors**|  
    |識別範圍管理|**\@auto_identity_range** (已淘汰) 與 **\@identityrangemangementoption**|  
    |發行者識別範圍|**\@pub_identity_range**|  
    |識別範圍|**\@identity_range**|  
    |識別範圍臨界值|**\@threshold**|  
    |資料分割選項|**\@partition_options**|  
    |Blob 資料行資料流|**\@stream_blob_columns**|  
    |篩選類型|**\@filter_type** ( **sp_addmergefilter** 中的參數)|  
  
     如需這些參數的詳細資訊，請參閱 [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 和 [sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)。  
  
-   異動複寫和未篩選的合併式複寫支援在多個發行集中發行資料表，然後在訂閱資料庫中的單一資料表內進行訂閱 (通常稱為積存狀況)。 積存通常用於從中央訂閱者端一個資料表中的多個位置彙總資料子集。 篩選的合併式發行集不支援中央「訂閱者」狀況。 對於合併式複寫，積存通常透過具有參數化資料列篩選器的單一發行集實作。 如需詳細資訊，請參閱＜ [參數化資料列篩選器](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [在現有發行集中新增和卸除發行項](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [[設定散發]](../../../relational-databases/replication/configure-distribution.md)   
 [初始化訂閱](../../../relational-databases/replication/initialize-a-subscription.md)   
 [編寫複寫指令碼](../../../relational-databases/replication/scripting-replication.md)   
 [保護發行者](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [訂閱發行集](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
