---
title: 擴展全文檢索索引 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- index populations [full-text search]
- incremental populations [full-text search]
- populations [full-text search]
- full-text search [SQL Server], populations
- crawls [full-text search]
- automatic full-text index updates
- change tracking-based populations [full-text search]
- manual updates [full-text search]
- manual populations [full-text search]
- auto populations [full-text search]
- full-text indexes [SQL Server], key column
- full populations [full-text search]
- full-text indexes [SQL Server], populations
ms.assetid: 76767b20-ef55-49ce-8dc4-e77cb8ff618a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6f871fabba547268736dca990215b89ae84e9eb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011182"
---
# <a name="populate-full-text-indexes"></a>擴展全文檢索索引
  建立和維護全文檢索索引包括使用稱為「母體擴展」  (Population) (也稱為「搜耙」  (Crawl)) 的處理序來擴展索引。  
  
##  <a name="types-of-population"></a><a name="types"></a>填入類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援下列類型的擴展：完整擴展、以變更追蹤為基礎的自動或手動擴展，以及以累加時間戳記為基礎的人口。  
  
### <a name="full-population"></a>完整母體擴展  
 在完整母體擴展期間，系統會針對資料表或索引檢視表的所有資料列建立索引項目。 全文檢索索引的完整母體擴展會針對基底資料表或索引檢視表的所有資料列建立索引項目。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在建立新的全文檢索索引時，立即進行完整母體擴展。 不過，完整母體擴展可能會耗用大量資源。 因此，在尖峰期間建立全文檢索索引時，最佳作法通常是延遲完整母體擴展直到離峰時間為止，尤其是全文檢索索引的基底資料表很龐大時。 不過，此索引所屬的全文檢索目錄要等到所有全文檢索索引都擴展之後才能使用。 若要建立全文檢索索引，但不立即擴展，請在 CREATE FULLTEXT INDEX 陳述式中指定 CHANGE_TRACKING OFF、NO POPULATION 子句。 如果您指定 CHANGE_TRACKING MANUAL，全文檢索引擎就會使用此陳述式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]將不會填入新的全文檢索索引，直到您使用「開始完整擴展」或「啟動增量擴展」子句執行 ALTER 全文檢索索引語句為止。 如需詳細資訊，請參閱本主題稍後的範例「A. 建立全文檢索索引但不執行完整母體擴展」以及「B. 針對資料表執行完整母體擴展」。  
  

  
### <a name="change-tracking-based-population"></a>以變更追蹤為基礎的母體擴展  
 在初始完整母體擴展之後，您可以選擇性地使用變更追蹤來維護全文檢索索引。 因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會維護追蹤上一次母體擴展以來對基底資料表所做之變更的資料表，所以存在與變更追蹤相關聯的少量負擔。 使用變更追蹤時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在基底資料表或索引檢視表中維護已經由更新、刪除或插入所修改之資料列的記錄。 透過 WRITETEXT 和 UPDATETEXT 的資料變更並不會反映在全文檢索索引中，變更追蹤並不會收取這些變更。  
  
> [!NOTE]  
>  如需包含 `timestamp` 資料行的資料表，您可以使用累加母體擴展。  
  
 在建立索引期間啟用變更追蹤時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會在建立新的全文檢索索引之後，立即完整擴展新的全文檢索索引。 之後，系統會追蹤並傳播變更至全文檢索索引。 變更追蹤有兩種類型：自動 (CHANGE_TRACKING AUTO 選項) 和手動 (CHANGE_TRACKING MANUAL 選項)。 自動變更追蹤是預設的行為。  
  
 變更追蹤的類型會決定擴展全文檢索索引的方式，如下所示：  
  
-   自動母體擴展  
  
     根據預設，或者如果您指定了 CHANGE_TRACKING AUTO，全文檢索引擎就會針對全文檢索索引使用自動母體擴展。 初始完整母體擴展完成之後，系統就會追蹤變更，因為基底資料表中的資料已修改，而且追蹤的變更會自動傳播。 不過，全文檢索索引會在背景更新，所以傳播的變更可能不會立即反映在索引中。  
  
     **若要使用自動母體擴展來設定追蹤變更**  
  
    -   [建立全文檢索索引](/sql/t-sql/statements/create-fulltext-index-transact-sql).。。使用 CHANGE_TRACKING AUTO  
  
    -   [改變全文檢索索引](/sql/t-sql/statements/alter-fulltext-index-transact-sql).。。設定 CHANGE_TRACKING 自動  
  
     如需詳細資訊，請參閱本主題稍後的範例「E. 將全文檢索索引更改成使用自動變更追蹤」。  
  
-   手動母體擴展  
  
     如果您指定了 CHANGE_TRACKING MANUAL，全文檢索引擎就會針對全文檢索索引使用手動母體擴展。 初始完整母體擴展完成之後，系統就會追蹤變更，因為基底資料表中的資料已修改。 不過，在您執行 ALTER 全文檢索索引之前，它們不會傳播到全文檢索索引 .。。啟動更新填入語句。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來定期呼叫這個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
     **若要使用手動母體擴展來啟動追蹤變更**  
  
    -   [建立全文檢索索引](/sql/t-sql/statements/create-fulltext-index-transact-sql).。。CHANGE_TRACKING 手動  
  
    -   [改變全文檢索索引](/sql/t-sql/statements/alter-fulltext-index-transact-sql).。。設定 CHANGE_TRACKING 手動  
  
     如需詳細資訊，請參閱本主題稍後的範例「C. 使用手動變更追蹤來建立全文檢索索引」以及「D. 執行手動母體擴展」。  
  
 **若要關閉變更追蹤**  
  
-   [建立全文檢索索引](/sql/t-sql/statements/create-fulltext-index-transact-sql).。。CHANGE_TRACKING 關閉  
  
-   [改變全文檢索索引](/sql/t-sql/statements/alter-fulltext-index-transact-sql).。。設定 CHANGE_TRACKING 關閉  
  

  
### <a name="incremental-timestamp-based-population"></a>以時間戳記為基礎的累加母體擴展  
 累加母體擴展是手動擴展全文檢索索引的替代機制。 您可以針對將 CHANGE_TRACKING 設定為 MANUAL 或 OFF 的全文檢索索引執行累加母體擴展。 如果全文檢索索引的第一個母體擴展是累加母體擴展，它就會建立所有資料列的索引，讓它相當於完整母體擴展。  
  
 累加母體擴展的執行要件是，索引資料表必須包含 `timestamp` 資料類型資料行。 少了 `timestamp` 資料行，就無法執行累加母體擴展。 對不含 `timestamp` 資料行的資料表提出累加母體擴展要求的話，會導致執行完整母體擴展作業。 此外，如果上一次母體擴展以來，影響資料表全文檢索索引的任何中繼資料已變更，便會以完整母體擴展的方式實作累加母體擴展。 這包括由於更改任何資料行、索引或全文檢索索引定義所導致的中繼資料變更。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會使用 `timestamp` 資料行來識別上一次母體擴展以來已經變更的資料列。 然後，累加母體擴展會針對在上一次母體擴展之後或進行時加入、刪除或修改的資料列，更新全文檢索索引。 如果資料表遇到大量插入作業，使用累加母體擴展可能會比使用手動母體擴展更有效率。  
  
 母體擴展結束時，全文檢索引擎會記錄新的 `timestamp` 值。 這個值就是「SQL 收集程式」所遇過的最大 `timestamp` 值。 此值會在後續的累加母體擴展啟動時使用。  
  
 若要執行累加母體擴展，請使用 START INCREMENTAL POPULATION 子句來執行 ALTER FULLTEXT INDEX 陳述式。  
  

  
##  <a name="examples-of-populating-full-text-indexes"></a><a name="examples"></a>填入全文檢索索引的範例  
  
> [!NOTE]  
>  本節中的範例使用 `Production.Document` 範例資料庫的 `HumanResources.JobCandidate` 或 `AdventureWorks` 資料表。  
  
### <a name="a-creating-a-full-text-index-without-running-a-full-population"></a>A. 建立全文檢索索引，但不執行完整母體擴展  
 下列範例會針對 `Production.Document` 範例資料庫的 `AdventureWorks` 資料表建立全文檢索索引。 這個範例會使用 WITH CHANGE_TRACKING OFF、NO POPULATION 來延遲初始完整母體擴展。  
  
```  
CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
CREATE FULLTEXT CATALOG AW_Production_FTCat;  
CREATE FULLTEXT INDEX ON Production.Document  
(  
    Document                         --Full-text index column name   
        TYPE COLUMN FileExtension    --Name of column that contains file type information  
        Language 1033                 --1033 is LCID for the English language  
)  
    KEY INDEX ui_ukDoc  
    ON AW_Production_FTCat  
    WITH CHANGE_TRACKING OFF, NO POPULATION;  
GO  
  
```  
  
### <a name="b-running-a-full-population-on-table"></a>B. 執行資料表的完整母體擴展  
 下列範例會針對 `Production.Document` 範例資料庫的 `AdventureWorks` 資料表執行完整母體擴展。  
  
```  
ALTER FULLTEXT INDEX ON Production.Document  
   START FULL POPULATION;  
```  
  
### <a name="c-creating-a-full-text-index-with-manual-change-tracking"></a>C. 使用手動變更追蹤來建立全文檢索索引  
 下列範例會針對 `HumanResources.JobCandidate` 範例資料庫的 `AdventureWorks` 資料表建立使用變更追蹤搭配手動母體擴展的全文檢索索引。  
  
```  
USE AdventureWorks;  
GO  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH CHANGE_TRACKING=MANUAL;  
GO  
```  
  
### <a name="d-running-a-manual-population"></a>D. 執行手動母體擴展  
 下列範例會針對 `HumanResources.JobCandidate` 範例資料庫之 `AdventureWorks` 資料表的變更追蹤全文檢索索引執行手動母體擴展。  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate START UPDATE POPULATION;  
GO  
```  
  
### <a name="e-altering-a-full-text-index-to-use-automatic-change-tracking"></a>E. 將全文檢索索引更改成使用自動變更追蹤  
 下列範例會將 `HumanResources.JobCandidate` 範例資料庫之 `AdventureWorks` 資料表的全文檢索索引變更成使用變更追蹤搭配自動母體擴展。  
  
```  
USE AdventureWorks;  
GO  
ALTER FULLTEXT INDEX ON HumanResources.JobCandidate SET CHANGE_TRACKING AUTO;  
GO   
```  
  

  
##  <a name="creating-or-changing-a-schedule-for-incremental-population"></a><a name="create"></a>建立或變更增量擴展的排程  
  
#### <a name="to-create-or-change-a-schedule-for-incremental-population-in-management-studio"></a>在 Management Studio 中建立或變更累加母體擴展的排程  
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 [資料庫]  ，然後展開包含全文檢索索引的資料庫。  
  
3.  展開 **[資料表]** 。  
  
 以滑鼠右鍵按一下已定義全文檢索索引的資料表、選取 [全文檢索索引]  ，然後按一下 [全文檢索索引]  內容功能表上的 [屬性]  。 這樣就會開啟 [全文檢索索引屬性]  對話方塊。  
  
1.  在 [**選取頁面**] 窗格中，選取 [排程]。  
  
     您可以使用這個頁面來建立或管理 SQL Server Agent 作業的排程，以便針對全文檢索索引的基底資料表或索引檢視表啟動累加資料表母體擴展。  
  
    > [!IMPORTANT]  
    >  如果基底資料表或檢視表沒有包含 `timestamp` 資料類型的資料行，就會執行完整母體擴展。  
  
     選項如下：  
  
    -   若要**建立**新的排程，請按一下 [新增]。  
  
         這樣就會開啟 [新增全文檢索索引資料表排程]**** 對話方塊，可讓您建立排程。 若要儲存排程，請按一下 [確定]****。  
  
        > [!IMPORTANT]  
        >  在您結束 [全文檢索索引屬性]**** 對話方塊之後，SQL Server Agent 作業 (針對 <資料庫名稱>**.<資料表名稱>** 啟動累加資料表母體擴展) 就會與新的排程相關聯。 如果您針對全文檢索索引建立多個排程，它們都會使用相同的作業。  
  
    -   若要變更排程，請選取它並按一下 [編輯]****。  
  
         這樣就會開啟 [新增全文檢索索引資料表排程]**** 對話方塊，可讓您修改排程。  
  
        > [!NOTE]  
        >  如需修改作業的詳細資訊，請參閱 [修改作業](../../ssms/agent/modify-a-job.md)。  
  
    -   若要移除排程，請選取它並按一下 [刪除]****。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  

  
##  <a name="troubleshooting-errors-in-a-full-text-population-crawl"></a><a name="crawl"></a>針對全文檢索擴展中的錯誤進行疑難排解（爬網）  
 搜耙發生錯誤時，「全文檢索搜尋」搜耙記錄功能會建立並維護搜耙記錄檔，此記錄檔是一個純文字檔。 每個搜耙記錄檔都對應至特定的全文檢索目錄。 根據預設，指定之執行個體的搜耙記錄檔 (在此範例中為第一個執行個體) 位於 %ProgramFiles%\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\LOG 資料夾中。 搜耙記錄檔會遵循下列命名結構：  
  
 SQLFT0000500008.2\<DatabaseID>\<FullTextCatalogID>。記錄檔\<[n>]  
  
 <`DatabaseID`>  
 資料庫的識別碼。 <`dbid`> 是前面加上零的五位數數位。  
  
 <`FullTextCatalogID`>  
 全文檢索目錄識別碼。 <`catid`> 是前面加上零的五位數數位。  
  
 <`n`>  
 是一個整數，指示相同全文檢索目錄的搜耙記錄檔數目。  
  
 例如，SQLFT0000500008.2 是指資料庫識別碼 = 5 而且全文檢索目錄識別碼 = 8 之資料庫的搜耙記錄檔。 位於檔案名稱結尾的 2 表示此資料庫/目錄組有兩個搜耙記錄檔。  
  

  
## <a name="see-also"></a>另請參閱  
 [dm_fts_index_population &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)   
 [全文檢索搜尋使用者入門](get-started-with-full-text-search.md)   
 [建立及管理全文檢索索引](create-and-manage-full-text-indexes.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
