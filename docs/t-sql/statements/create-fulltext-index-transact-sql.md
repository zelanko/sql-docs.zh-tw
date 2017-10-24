---
title: "CREATE FULLTEXT INDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
caps.latest.revision: 110
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 92749ed0518de83be07c6a80f9e3306741507166
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的某份資料表或索引檢視表建立全文檢索索引。 每個資料表或索引檢視表只允許有一個全文檢索索引，而且每個全文檢索索引都會套用至單一資料表或索引檢視表。 全文檢索索引最多可包含 1024 個資料行。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
## <a name="arguments"></a>引數  
 *table_name*  
 這是包括在全文檢索索引中之一個或多個資料行所在的資料表或索引檢視表名稱。  
  
 *column_name*  
 這是包含在全文檢索索引中的資料行名稱。 類型的資料行**char**， **varchar**， **nchar**， **nvarchar**，**文字**， **ntext**，**映像**， **xml**，和**varbinary （max)**可以建立全文檢索搜尋的索引。 若要指定多個資料行，重複*column_name*子句，如下所示：  
  
 CREATE FULLTEXT INDEX ON *table_name* (*column_name1* […]， *column_name2* […])...  
  
 類型資料行*type_column_name*  
 指定的資料表資料行名稱*type_column_name*，也就是用來保存的文件類型**varbinary （max)**或**映像**文件。 這個資料行 (稱為類型資料行) 包含使用者提供的副檔名 (.doc、.pdf、.xls 等等)。 類型資料行必須屬於下列類型： **char**, **nchar**, **varchar**或 **nvarchar**。  
  
 指定 TYPE COLUMN *type_column_name*才*column_name*指定**varbinary （max)**或**映像**資料行，資料儲存為二進位資料。否則，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會傳回錯誤。  
  
> [!NOTE]  
>  建立索引時，全文檢索引擎會使用縮寫中每個資料表資料列的型別資料行來識別要使用文件中的全文檢索搜尋篩選*column_name*。 篩選會將文件載入為二進位資料流、移除格式資訊，並且將文件中的文字傳送到斷詞工具元件。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)。  
  
 語言*language_term*  
 是儲存在資料的語言*column_name*。  
  
 *language_term*是選擇性的可以指定為字串、 整數或十六進位值對應的語言地區設定識別碼 (LCID)。 如果未指定任何值，就會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的預設語言。  
  
 如果*language_term*已指定，會使用它所代表的語言，索引資料儲存在**char**， **nchar**， **varchar**， **nvarchar**，**文字**，和**ntext**資料行。 此語言是如果在查詢時使用的預設語言*language_term*並未指定為針對資料行的全文檢索述詞的一部分。  
  
 當指定為字串， *language_term*對應至 syslanguages 系統資料表中的 alias 資料行值。 字串必須括在單引號中**'***language_term***'**。 當指定為整數， *language_term*是識別之語言的實際 LCID。 當指定為十六進位值， *language_term* 0x 後面接著 LCID 的十六進位值。 十六進位值不能超出 8 位數，開頭的零也包括在內。  
  
 如果這個值是雙位元組字集 (DBCS) 格式，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它轉換成 Unicode。  
  
 必須啟用為指定的語言資源，例如斷詞工具和字幹分析器， *language_term*。 如果這些資源不支援指定的語言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。  
  
 請利用 sp_configure 預存程序來存取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之預設全文檢索語言的相關資訊。 如需詳細資訊，請參閱本主題稍後的 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)的使用者閱讀。  
  
 如果是包含多種語言之文字資料的非 BLOB 和非 XML 資料行，或是資料行內所儲存的文字語言不明，您可能適合使用中性 (0x0) 語言資源。 但是，您應該先了解使用中性 (0x0) 語言資源的可能結果。 如需可能的解決方案和使用中性 (0x0) 語言資源的結果資訊，請參閱[選擇語言時建立的全文檢索索引](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
 如果是儲存在 XML 或 BLOB 類型資料行中的文件，在建立索引時，將使用文件內的語言編碼。 例如，在 XML 資料行， **xml: lang** XML 文件中的屬性會識別語言。 在查詢時，先前中指定的值*language_term*除非用於全文檢索查詢的預設語言會變成*language_term*指定做為全文檢索查詢的一部分。  
  
 STATISTICAL_SEMANTICS  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 建立其他關鍵片語以及屬於統計語意索引一部分的文件相似度索引。 如需詳細資訊，請參閱[語意搜尋 &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)。  
  
 索引鍵*index_name*  
 是唯一的索引鍵索引的名稱上*table_name*。 KEY INDEX 必須是唯一、單索引鍵，且不允許為 Null 的資料行。 請選取最小的唯一索引鍵索引來當做全文檢索唯一索引鍵。  如需最佳效能，我們建議您針對全文檢索索引鍵使用整數資料類型。  
  
 *fulltext_catalog_name*  
 這是全文檢索索引所用的全文檢索目錄。 這個目錄必須已存在於資料庫中。 這個子句是選擇性的。 如果未指定它，就會使用預設目錄。 如果沒有預設目錄，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會傳回錯誤。  
  
 檔案群組*filegroup_name*  
 在指定的檔案群組上建立全文檢索索引。 此檔案群組必須已存在。 如果未指定 FILEGROUP 子句，全文檢索索引會放在與非資料分割資料表之基底資料表或檢視表相同的檔案群組中，或是放在資料分割資料表的主要檔案群組中。  
  
 CHANGE_TRACKING [=] {手動 |**自動**|關閉 [，不進行母體擴展]}  
 指定全文檢索索引涵蓋的資料表資料行變更 (更新、刪除或插入)，是否會由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳播到全文檢索索引。 透過 WRITETEXT 和 UPDATETEXT 的資料變更並不會反映在全文檢索索引中，變更追蹤並不會收取這些變更。  
  
 MANUAL  
 指定必須手動傳播追蹤的變更 (藉由呼叫 ALTER FULLTEXT INDEX …  START UPDATE POPULATION[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式 (*手動母體擴展*)。 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來定期呼叫這個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
 **自動**  
 指定基底資料表中的資料變更，會自動傳播追蹤的變更 (*自動母體擴展*)。 雖然變更會自動傳播，但這些變更可能不會立即反映在全文檢索索引中。 預設值是 AUTO。  
  
 OFF [ `,` NO POPULATION]  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不保留索引資料的變更清單。 未指定 NO POPULATION 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在建立好索引之後完整擴展索引。  
  
 只有在 CHANGE_TRACKING 是 OFF 時，才能使用 NO POPULATION 選項。 當指定 NO POPULATION 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在建立好索引之後並不會擴展索引。 只有當使用者執行含有 START FULL POPULATION 或 START INCREMENTAL POPULATION 子句的 ALTER FULLTEXT INDEX 命令之後，才會擴展索引。  
  
 停用字詞表 [=] {關閉 |**系統** | *s* }  
 將全文檢索停用字詞表與索引產生關聯。 此索引不會填入屬於指定之停用字詞表一部分的任何 Token。 如果未指定 STOPLIST，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將系統全文檢索停用字詞表與此索引產生關聯。  
  
 OFF  
 指定沒有任何停用字詞表要與全文檢索索引產生關聯。  
  
 **系統**  
 指定預設全文檢索系統 STOPLIST 應該用於這個全文檢索索引。  
  
 *s*  
 指定要與全文檢索索引產生關聯的停用字詞表名稱。  
  
 搜尋屬性清單 [=] *property_list_name*  
 **適用於**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 將搜尋屬性清單與索引產生關聯。  
  
 OFF  
 指定沒有任何屬性清單要與全文檢索索引產生關聯。  
  
 *property_list_name*  
 指定要與全文檢索索引產生關聯的搜尋屬性清單名稱。  
  
## <a name="remarks"></a>備註  
 如需有關全文檢索索引的詳細資訊，請參閱[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。  
  
 在**xml**資料行，您可以建立全文檢索索引內容的 XML 元素，但忽略 XML 標記。 屬性值是全文檢索索引的值 (除非它們是數值)。 元素標記會當做 Token 界限來使用。 系統支援包含多種語言且格式正確的 XML 或 HTML 文件和片段。 如需詳細資訊，請參閱 [使用 XML 資料行進行全文檢索搜尋](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)。  
  
 建議索引鍵資料行最好是整數資料類型， 這樣會在查詢執行時提供最佳化。  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>變更追蹤與 NO POPULATION 參數之間的互動  
 全文檢索索引是否會擴展，將取決於是否啟用變更追蹤及是否在 ALTER FULLTEXT INDEX 陳述式中指定 WITH NO POPULATION 而定。 下表摘要列出其互動的結果。  
  
|變更追蹤|WITH NO POPULATION|結果|  
|---------------------|------------------------|------------|  
|未啟用|未指定|在索引上執行完整母體擴展。|  
|未啟用|已指定|要等到發出 ALTER FULLTEXT INDEX...START POPULATION 陳述式之後，才會進行索引的母體擴展。|  
|已啟用|已指定|引發錯誤，而且索引不會改變。|  
|已啟用|未指定|在索引上執行完整母體擴展。|  
  
 如需有關擴展全文檢索索引的詳細資訊，請參閱[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。  
  
## <a name="permissions"></a>Permissions  
 使用者必須有全文檢索目錄的 REFERENCES 權限，並具有資料表或索引檢視表的 ALTER 權限，或者是系統管理員 (sysadmin) 固定伺服器角色的成員，或是 db_owner 或 db_ddladmin 固定資料庫角色的成員。  
  
 如果指定了 SET STOPLIST，使用者在指定的停用字詞表上必須具有 REFERENCES 權限。 STOPLIST 的擁有者可以授與這個權限。  
  
> [!NOTE]  
>  一般使用者會被授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所隨附之預設停用字詞表的 REFERENCE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. 建立唯一的索引、全文檢索目錄及全文檢索索引  
 下列範例會針對 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 範例資料庫中 `JobCandidateID` 資料表上的 `HumanResources.JobCandidate` 資料行建立唯一索引。 然後此範例會建立預設全文檢索目錄 `ft`。 最後，此範例會使用 `Resume` 目錄和系統停用字詞表，針對 `ft` 資料行建立全文檢索索引。  
  
```  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. 建立數個資料表資料行的全文檢索索引  
 下列範例會在 `production_catalog` 範例資料庫中建立全文檢索目錄 `AdventureWorks`。 接著，此範例會建立使用這個新目錄的全文檢索索引。 全文檢索索引位於 `ReviewerName` 資料表的 `EmailAddress`、`Comments` 和 `Production.ProductReview` 資料行上。 此範例會針對每一個資料行指定英文的 LCID `1033`，這是資料行中資料的語言。 這個全文檢索索引會使用現有的唯一索引鍵索引 `PK_ProductReview_ProductReviewID`。 建議這個索引鍵位於整數資料行 `ProductReviewID` 上。  
  
```  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. 建立具有搜尋屬性清單但不加以擴展的全文檢索索引  
 下列範例會針對 `Title` 資料表的 `DocumentSummary`、`Document` 和 `Production.Document` 資料行建立全文檢索索引。 此範例會指定英文的 LCID `1033`，這是這些資料行中資料的語言。 這個全文檢索索引會使用預設的全文檢索目錄及現有的唯一索引鍵索引 `PK_Document_DocumentID`。 建議這個索引鍵位於整數資料行 `DocumentID` 上。  
  
 此範例會指定 SYSTEM 停用字詞表。 它也會指定搜尋屬性清單， `DocumentPropertyList`; 如需範例，建立這個屬性清單，請參閱[CREATE SEARCH PROPERTY LIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
 此範例指定關閉變更追蹤，而且無擴展。 之後在離峰時段，此範例會使用 ALTER FULLTEXT INDEX 陳述式，針對新的索引開始完整母體擴展，並啟用自動變更追蹤。  
  
```  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 之後，在離峰時段擴展索引：  
  
```  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [sys.fulltext_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  

