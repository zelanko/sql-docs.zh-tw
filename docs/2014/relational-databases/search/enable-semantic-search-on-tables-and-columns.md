---
title: 在資料表和資料行上啟用語意搜尋 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], enabling
ms.assetid: 895d220c-6749-4954-9dd3-2ea4c6a321ff
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2cd0ea9764007784fb6f999c3115e0a2997d8e2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011376"
---
# <a name="enable-semantic-search-on-tables-and-columns"></a>在資料表和資料行上啟用語意搜尋
  描述如何針對包含文件或文字的選取資料行啟用或停用統計語意索引。  
  
 統計語意搜尋會使用全文檢索搜尋所建立的索引，並且建立其他索引。 由於全文檢索搜尋存在這種相依性，因此您可以在定義新的全文檢索索引或改變現有的全文檢索索引時，建立新的語意索引。 您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的 [全文檢索索引精靈] 和其他對話方塊來建立新的語意索引 (如本主題所述)。  
  
##  <a name="BasicEnabling"></a> 建立語意索引  
  
###  <a name="reqenable"></a> 建立語意索引的需求和限制  
  
-   您可以針對支援全文檢索索引的任何資料庫物件建立索引，包括資料表和索引檢視表。  
  
-   必須具有下列必要條件，才能啟用特定資料行的語意索引。  
  
    -   資料庫必須具有全文檢索目錄。  
  
    -   資料表必須具有全文檢索索引。  
  
    -   選取的資料行必須參與全文檢索索引。  
  
     您可以同時建立並啟用所有這些需求。  
  
-   您可以針對具有支援全文檢索索引之任何資料類型的資料行建立語意索引。 如需詳細資訊，請參閱 [建立及管理全文檢索索引](create-and-manage-full-text-indexes.md)。  
  
-   您可以指定支援 `varbinary(max)` 資料行之全文檢索索引的任何文件類型。 如需詳細資訊，請參閱本主題中的[如何：決定可以建立索引的文件類型](#doctypes)。  
  
-   語意索引會針對您所選取的資料行建立兩種索引類型：主要片語的索引，以及文件相似度的索引。 當您啟用語意索引時，無法單獨選取其中一種索引類型。 不過，您可以個別查詢這兩個索引。 如需詳細資訊，請參閱 [使用語意搜尋找到文件中的主要片語](find-key-phrases-in-documents-with-semantic-search.md) 和 [使用語意搜尋尋找相似及相關的文件](find-similar-and-related-documents-with-semantic-search.md)。  
  
-   如果您沒有明確指定語意索引的 LCID，則只有主要語言及其相關聯的語言統計資料會用於語意索引。  
  
-   如果您針對語言模型無法使用的資料行指定了語言，索引的建立作業就會失敗並且傳回錯誤訊息。  
  
###  <a name="HowToEnableCreate"></a> 如何：沒有全文檢索索引時建立語意索引  
 當您使用 **CREATE FULLTEXT INDEX** 陳述式來建立新的全文檢索索引時，可以透過指定 **STATISTICAL_SEMANTICS** 關鍵字當作資料行定義的一部分，在資料行層級中啟用語意索引。 此外，當您使用 [全文檢索索引精靈] 來建立新的全文檢索索引時，也可以啟用語意索引。  
  
 **使用 TRANSACT-SQL 建立新的語意索引**  
 您可以針對想要建立語意索引的每個資料行呼叫 **CREATE FULLTEXT INDEX** 陳述式並指定 **STATISTICAL_SEMANTICS**。 如需此陳述式之所有選項的詳細資訊，請參閱 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)。  
  
 **範例 1：建立唯一索引、全文檢索索引及語意索引**  
  
 下列範例會建立預設全文檢索目錄 **ft**。接著，此範例會針對 AdventureWorks2012 範例資料庫中 **HumanResources.JobCandidate** 資料表的 **JobCandidateID** 資料行建立唯一索引。 這個唯一索引需要做為全文檢索索引的索引鍵資料行。 接著，此範例會針對 **Resume** 資料行建立全文檢索索引和語意索引。  
  
```sql  
CREATE FULLTEXT CATALOG ft AS DEFAULT  
GO  
  
CREATE UNIQUE INDEX ui_ukJobCand  
    ON HumanResources.JobCandidate(JobCandidateID)  
GO  
  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate  
    (Resume  
        Language 1033  
        Statistical_Semantics  
    )   
    KEY INDEX JobCandidateID   
    WITH STOPLIST = SYSTEM  
GO  
```  
  
 **範例 2：針對許多資料行建立全文檢索和語意索引並延遲索引母體擴展**  
  
 下列範例會在 AdventureWorks2012 範例資料庫中建立全文檢索目錄 **documents_catalog**。 接著，此範例會建立使用這個新目錄的全文檢索索引。 全文檢索索引是針對 **Production.Document**資料表的 **Title**、 **DocumentSummary** 及 **Document** 資料行而建立，而語意索引則只針對 **Document** 資料行而建立。 這個全文檢索索引會使用新建的全文檢索目錄和現有的唯一索引鍵索引 **PK_Document_DocumentID**。 根據建議，此索引鍵是建立於整數資料行 **DocumentID**上。 此範例會指定英文的 LCID (1033)，這是這些資料行中資料的語言。  
  
 此範例也會指定關閉變更追蹤，而且不進行母體擴展。 之後在離峰時段，此範例會使用 **ALTER FULLTEXT INDEX** 陳述式，針對新的索引啟動完整母體擴展，並啟用自動變更追蹤。  
  
```sql  
CREATE FULLTEXT CATALOG documents_catalog  
GO  
  
CREATE FULLTEXT INDEX ON Production.Document  
    (   
    Title  
        Language 1033,   
    DocumentSummary  
        Language 1033,   
    Document   
        TYPE COLUMN FileExtension  
        Language 1033  
        Statistical_Semantics  
    )  
    KEY INDEX PK_Document_DocumentID  
        ON documents_catalog  
        WITH CHANGE_TRACKING OFF, NO POPULATION  
GO  
```  
  
 之後，在離峰時段擴展索引：  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO  
GO  
```  
  
 **使用 SQL Server Management Studio 建立新的語意索引**  
 您可以針對想要建立語意索引的每個資料行執行 [全文檢索索引精靈]，並在 [選取資料表資料行]  頁面上啟用 [統計語意]  。 如需詳細資訊，包含如何啟動 [全文檢索索引精靈] 的相關資訊，請參閱 [使用全文檢索索引精靈](use-the-full-text-indexing-wizard.md)。  
  
###  <a name="HowToEnableAlter"></a> 如何：使用現有的全文檢索索引時建立語意索引  
 當您使用 **ALTER FULLTEXT INDEX** 陳述式來改變現有的全文檢索索引時，可以加入語意索引。 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的各種對話方塊來加入語意索引。  
  
 **使用 TRANSACT-SQL 加入語意索引**  
 您可以針對想要加入語意索引的每個資料行，使用下面所述的選項來呼叫 **ALTER FULLTEXT INDEX** 陳述式。 如需此陳述式之所有選項的詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)。  
  
 除非您指定其他選項，否則在呼叫 **ALTER** 之後，全文檢索和語意索引都會重新擴展。  
  
-   若只要將全文檢索索引加入資料行，請使用 **ADD** 語法。  
  
-   若要將全文檢索和語意索引都加入資料行，請使用 **ADD** 語法搭配 **STATISTICAL_SEMANTICS** 選項。  
  
-   若要將語意索引加入已啟用全文檢索索引的資料行，請使用 **ADD STATISTICAL_SEMANTICS** 選項。 在單一 **ALTER** 陳述式中，您只能將語意索引加入至一個資料行。  
  
 **範例：將語意索引新增至已經具有全文檢索索引的資料行**  
  
 下列範例會針對 AdventureWorks2012 範例資料庫中的 **Production.Document** 資料表改變現有的全文檢索索引。 此範例會針對 **Production.Document** 資料表的 **Document** 資料行 (已經具有全文檢索索引) 加入語意索引。 此範例會指定不要自動重新擴展索引。  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document  
    ALTER COLUMN Document  
        ADD Statistical_Semantics  
    WITH NO POPULATION  
GO  
```  
  
 **使用 SQL Server Management Studio 加入語意索引**  
 您可以在 [全文檢索索引屬性]  對話方塊的 [全文檢索索引資料行]  頁面上變更已啟用語意和全文檢索索引的資料行。 如需詳細資訊，請參閱 [管理全文檢索索引](../../database-engine/manage-full-text-indexes.md)。  
  
###  <a name="addreq"></a> 改變現有索引的需求和限制  
  
-   當現有索引的母體擴展正在進行時，您無法改變該索引。 如需監視索引母體擴展之進度的詳細資訊，請參閱 [管理及監視語意搜尋](manage-and-monitor-semantic-search.md)。  
  
-   您無法在 **ALTER FULLTEXT INDEX** 陳述式的單一呼叫中，將索引加入至資料行，以及改變或卸除相同資料行的索引。  
  
##  <a name="dropping"></a> 卸除語意索引  
  
###  <a name="drophow"></a> 如何：卸除語意索引  
 當您使用 **ALTER FULLTEXT INDEX** 陳述式來改變現有的全文檢索索引時，可以卸除語意索引。 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的各種對話方塊來卸除語意索引。  
  
 **使用 TRANSACT-SQL 卸除語意索引**  
 -   若只要從一或多個資料行卸除語意索引，請使用 **ALTER COLUMN***column_name***DROP STATISTICAL_SEMANTICS** 選項呼叫 **ALTER FULLTEXT INDEX** 陳述式。 在單一 **ALTER** 陳述式中，您可以從多個資料行中卸除索引。  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP STATISTICAL_SEMANTICS  
    GO  
    ```  
  
-   若要從某個資料行同時卸除全文檢索和語意索引，請使用 **ALTER COLUMN***column_name***DROP**選項呼叫 **ALTER FULLTEXT INDEX** 陳述式。  
  
    ```sql  
    USE database_name  
    GO  
  
    ALTER FULLTEXT INDEX  
        ALTER COLUMN column_name  
        DROP  
    GO  
    ```  
  
 **使用 SQL Server Management Studio 卸除語意索引**  
 您可以在 [全文檢索索引屬性]  對話方塊的 [全文檢索索引資料行]  頁面上變更已啟用語意和全文檢索索引的資料行。 如需詳細資訊，請參閱 [管理全文檢索索引](../../database-engine/manage-full-text-indexes.md)。  
  
###  <a name="dropreq"></a> 卸除語意索引的需求和限制  
  
-   您無法從資料行中卸除全文檢索索引，而保留語意索引。 語意索引相依於全文檢索索引的文件相似度結果。  
  
-   在已啟用語意索引的資料表中，當您從最後一個資料行中卸除語意索引時，就無法指定 **NO POPULATION** 選項。 若要移除先前已建立索引的結果，則需要使用母體擴展循環。  
  
## <a name="checking-whether-semantic-search-is-enabled-on-database-objects"></a>檢查資料庫物件上是否啟用語意搜尋  
  
###  <a name="HowToCheckEnabled"></a> 如何：檢查資料庫物件上是否啟用語意搜尋  
 **資料庫是否已啟用語意搜尋？**  
 查詢 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/databasepropertyex-transact-sql) 中繼資料函數的 **IsFullTextEnabled** 屬性。  
  
 傳回值 1 表示已針對資料庫啟用全文檢索搜尋和語意搜尋，傳回值 0 表示未啟用這兩個搜尋。  
  
```sql  
SELECT DATABASEPROPERTYEX('database_name', 'IsFullTextEnabled')  
GO  
```  
  
 **資料表是否已啟用語意搜尋？**  
 查詢 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql) 中繼資料函數的 **TableFullTextSemanticExtraction** 屬性。  
  
 傳回值 1 表示已針對資料表啟用語意搜尋，傳回值 0 表示未啟用此搜尋。  
  
```scr  
SELECT OBJECTPROPERTYEX(OBJECT_ID('table_name'), 'TableFullTextSemanticExtraction')  
GO  
```  
  
 **資料行是否已啟用語意搜尋？**  
 若要判斷是否已針對特定資料行啟用語意搜尋：  
  
-   查詢 [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql) 中繼資料函數的 **StatisticalSemantics** 屬性。  
  
     傳回值 1 表示已針對資料行啟用語意搜尋，傳回值 0 表示未啟用此搜尋。  
  
    ```sql  
    SELECT COLUMNPROPERTY(OBJECT_ID('table_name'), 'column_name', 'StatisticalSemantics')  
    GO  
    ```  
  
-   查詢目錄檢視 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql) 找出全文檢索索引。  
  
     **statistical_semantics** 資料行中的值 1 表示指定的資料行除了啟用全文檢索索引以外，也啟用了語意索引。  
  
    ```sql  
    SELECT * FROM sys.fulltext_index_columns WHERE object_id = OBJECT_ID('table_name')  
    GO  
    ```  
  
-   在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管中，以滑鼠右鍵按一下資料行，然後選取 [屬性]  。 在 **[資料行屬性]** 對話方塊的 **[一般]** 頁面上，檢查 **[Statistical Semantics]** 屬性的值。  
  
     True 值表示指定的資料行除了啟用全文檢索索引以外，也啟用了語意索引。  
  
## <a name="determining-what-can-be-indexed-for-semantic-search"></a>判斷可建立索引供語意搜尋使用的項目  
  
###  <a name="HowToCheckLanguages"></a> 如何：檢查語意搜尋所支援的語言  
  
> [!IMPORTANT]  
>  支援語意索引的語言比支援全文檢索索引的語言要少。 因此，可能會有可建立索引供全文檢索搜尋，但無法用於語意搜尋的資料行。  
  
 查詢目錄檢視 [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql)。  
  
```sql  
SELECT * FROM sys.fulltext_semantic_languages  
GO  
```  
  
 下列是語意索引所支援的語言。 此清單代表 [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql) 目錄檢視的輸出 (依據 LCID 排序)。  
  
|語言|LCID|  
|--------------|----------|  
|德文|1031|  
|英文 (美國)|1033|  
|法文|1036|  
|義大利文|1040|  
|葡萄牙文 (巴西)|1046|  
|俄文|1049|  
|瑞典文|1053|  
|英文 (英國)|2057|  
|葡萄牙文 (葡萄牙)|2070|  
|西班牙文|3082|  
  
###  <a name="doctypes"></a> 如何：決定可以進行索引的文件類型  
 查詢目錄檢視 [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql)。  
  
 如果您想要索引的文件類型不在支援的類型清單中，則可能必須尋找、下載並安裝其他篩選。 如需詳細資訊，請參閱 [檢視或變更已註冊的篩選與斷詞工具](view-or-change-registered-filters-and-word-breakers.md)。  
  
##  <a name="BestPracticeFilegroup"></a> 最佳做法：考慮針對全文檢索和語意索引建立個別的檔案群組  
 如果您有磁碟空間配置的顧慮，請考慮針對全文檢索和語意索引建立個別的檔案群組。 語意索引與全文檢索索引會建立在相同的檔案群組中。 完整擴展的語意索引可能會包含大量資料。  
  
##  <a name="BestPracticeUnderstand"></a>   
##  <a name="IssueNoResults"></a> 問題：針對特定資料行搜尋未傳回任何結果  
 **您是否針對 Unicode 語言指定了非 Unicode LCID？**  
 您可以針對 LCID 代表只有 Unicode 字詞之語言 (例如俄文 LCID 1049) 的非 Unicode 資料行類型啟用語意索引。 在此情況下，這個資料行的語意索引永遠不會傳回任何結果。  
  
  
