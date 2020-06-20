---
title: 全文檢索搜尋使用者入門 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: eec806bffba330ac3ab995c1b3bfd3504589ecfd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063290"
---
# <a name="get-started-with-full-text-search"></a>全文檢索搜尋使用者入門
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料庫預設會啟用全文檢索。 不過，若要針對資料表使用全文檢索索引，您必須在要以全文檢索引擎存取的資料表資料行中設定全文檢索索引功能。  
  
##  <a name="configuring-a-database-for-full-text-search"></a><a name="configure"></a>設定全文檢索搜尋的資料庫  
 在任何案例中，資料庫管理員都會執行下列基本步驟，針對全文檢索搜尋設定資料庫中的資料表資料行：  
  
1.  建立全文檢索目錄。  
  
2.  在您想要搜尋的每個資料表上，建立全文檢索索引：  
  
    1.  識別您想要包含在全文檢索索引中的每個文字資料行。  
  
    2.  如果給定的資料行包含儲存為二進位資料（ `varbinary(max)` 或 `image` 資料）的檔，您就必須指定資料表資料行（*類型資料行*），以識別要編制索引之資料行中每個檔的類型。  
  
    3.  指定您想讓全文檢索搜尋用於資料行中文件的語言。  
  
    4.  選擇您想要針對全文檢索索引使用的變更追蹤機制，以便追蹤基底資料表及其資料行中的變更。  
  
 全文檢索搜尋會透過使用下列「語言元件」**(Linguistic Component) 支援多國語言：斷詞工具和字幹分析器、包含停用字詞 (也稱為非搜尋字) 的停用字詞表，以及同義字檔案。 同義字檔案和停用字詞表 (在某些情況下) 會要求資料庫管理員進行組態設定。 給定的同義字檔案支援所有使用對應語言的全文檢索索引，而且給定的停用字詞表可以與任意數目的全文檢索索引相關聯。  
  
##  <a name="setting-up-a-full-text-catalog-and-index"></a><a name="setup"></a>設定全文檢索目錄和索引  
 這項作業包含下列基本步驟：  
  
1.  建立全文檢索目錄以儲存全文檢索索引。  
  
     每個全文檢索索引都必須屬於一個全文檢索目錄。 您可以針對每個全文檢索索引建立個別的文字目錄，也可以讓多個全文檢索索引與給定的目錄產生關聯。 全文檢索目錄是虛擬物件，而且不屬於任何檔案群組。 目錄是參考一組全文檢索索引的邏輯概念。  
  
2.  針對資料表或索引檢視表建立全文檢索索引。  
  
     全文檢索索引是一種特殊類型的 Token 式功能索引，由全文檢索引擎所建立與維護。 若要針對資料表或檢視表建立全文檢索搜尋，它必須具有唯一、單一資料行且不可為 Null 的索引。 全文檢索引擎需要使用此唯一索引，將資料表中的各資料列對應至唯一且可壓縮的索引鍵。 全文檢索索引可以包括 `char`、`varchar`、`nchar``nvarchar`、`text`、`ntext`、`image`、`xml`、`varbinary` 和 `varbinary(max)` 資料行。 如需詳細資訊，請參閱 [建立及管理全文檢索索引](create-and-manage-full-text-indexes.md)。  
  
 學習建立全文檢索索引之前，請務必了解全文檢索索引與一般 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引的差異。 下表列出差異。  
  
|全文檢索索引|一般 SQL Server 索引|  
|------------------------|--------------------------------|  
|每個資料表只允許有一個全文檢索索引。|每個資料表允許有多個一般索引。|  
|將資料加入至全文檢索索引的作業稱為「母體擴展」**(Population)，可透過排程或特定的要求來要求執行，也可在加入新的資料時自動執行。|當依據的資料有插入、更新或刪除時，會自動更新索引內容。|  
|在相同的資料庫中分組為一個或多個全文檢索目錄。|沒有分組。|  
  
  
##  <a name="choosing-options-for-a-full-text-index"></a><a name="options"></a>選擇全文檢索索引的選項  
 本節內容包括下列主題：  
  
-   選擇資料行語言  
  
-   選擇全文檢索索引的檔案群組  
  
-   將全文檢索索引指派給全文檢索目錄  
  
-   將停用字詞表與全文檢索索引產生關聯  
  
-   更新全文檢索索引  
  
### <a name="choosing-the-column-language"></a>選擇資料行語言  
 如需有關選擇資料行語言時應考慮哪些事項的詳細資訊，請參閱[選擇建立全文檢索索引時的語言](choose-a-language-when-creating-a-full-text-index.md)。  
  
### <a name="choosing-a-filegroup-for-a-full-text-index"></a>選擇全文檢索索引的檔案群組  
 建立全文檢索索引的程序需要大量 I/O (在較高層次中，此程序包括從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中讀取資料，然後將篩選的資料傳播至全文檢索索引)。 最佳作法是將全文檢索索引放置於最適合將 I/O 效能發揮到極致的資料庫檔案群組中，或是將全文檢索索引放置於另一個磁碟區的不同檔案群組中。  
  
 如果管理方便對您很重要，我們建議您將資料表資料及任何附屬的全文檢索目錄儲存在相同檔案群組中。 有時候，基於效能的考量，您可能會想要將資料表資料和全文檢索索引存放在儲存於不同磁碟區上的不同檔案群組中，以便有效發揮 I/O 平行處理原則。  
  
  
### <a name="assigning-the-full-text-index-to-a-full-text-catalog"></a>將全文檢索索引指派給全文檢索目錄  
 在全文檢索目錄中，規劃資料表之全文檢索索引的位置是相當重要的步驟。  
  
 我們建議您在相同的全文檢索目錄底下，將具有相同更新特性的資料表 (例如少量變更與大量變更，或在每日特定時段頻繁變更的資料表) 產生關聯。 透過設定全文檢索目錄的母體擴展排程，在高度資料庫活動期間，全文檢索索引仍然能夠保持與資料表同步，而不會對資料庫伺服器的資源使用量造成負面影響。  
  
 當您將資料表指派給全文檢索目錄時，請考量下列指導方針：  
  
-   永遠選取最小的唯一索引，做為全文檢索唯一索引鍵。 （4位元組、以整數為基礎的索引是最佳的）。這會 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 大幅減少搜尋服務在檔案系統中所需的資源。 如果主索引鍵較大 (超過 101 個位元組) 時，可考慮選擇資料表中其他的唯一索引，做為全文檢索唯一的索引鍵 (或建立另一個唯一索引)。 若全文檢索唯一索引鍵的大小超過允許的最大值 (900 個位元組) 時，將無法執行全文檢索的母體擴展作業。  
  
-   如果您正在針對包含數百萬資料列的資料表建立索引，請將此資料表指派給它本身的全文檢索目錄。  
  
-   考慮正在建立全文檢索索引之資料表中發生的變更數量，以及資料列總數。 如果變更的資料列總數，與上次執行全文檢索母體擴展的資料列總和超過百萬，請將此資料表指派給它本身的全文檢索目錄。  
  
  
### <a name="associating-a-stoplist-with-the-full-text-index"></a>將停用字詞表與全文檢索索引產生關聯  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 導入了停用字詞表。 *「停用字詞表」* (Stoplist) 是停用字詞 (也稱為非搜尋字) 的清單。 停用字詞表會與每個全文檢索索引相關聯，而且該停用字詞表中的字詞會套用至該索引的全文檢索查詢。 根據預設，系統停用字詞表會與新的全文檢索索引相關聯。 不過，您可以改為建立並使用自己的停用字詞表。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
 例如，下列[建立全文](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)檢索停用字詞表 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 語句會從系統停用字詞表中複製，以建立名為 myStoplist3 的新全文檢索停用字詞表：  
  
```  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 下列[ALTER 全文](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)檢索停 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 用字詞表語句會改變名為 myStoplist 的停用字詞表，並加入 ' en ' 這個字，第一個是針對西班牙文，再針對法文  
  
```  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST MyStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
  
  
### <a name="updating-a-full-text-index"></a>更新全文檢索索引  
 如同一般 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引，當相關聯資料表中的資料變更時，就可以自動更新全文檢索索引。 此為預設行為。 或者，您也可以手動或以指定的排程間隔將全文檢索索引保持在最新狀態。 擴展全文檢索索引可能會相當耗時而且需要大量資源，因此，索引更新通常會當做在背景中執行的非同步處理序執行並且在修改基底資料表之後，將全文檢索索引保持在最新狀態。 在基底資料表每次變更之後立即更新全文檢索索引可能需要大量資源。 因此，如果您設定了非常高的更新/插入/刪除速率，可能會遇到查詢效能降低的情況。 如果發生這種情況，請考慮排程手動變更追蹤更新，以便偶爾與許多變更保持同步，而非與查詢競爭資源。  
  
 若要監視母體擴展狀態，請使用 FULLTEXTCATALOGPROPERTY 函數或 OBJECTPROPERTYEX 函數。 若要取得目錄母體擴展狀態，請執行下列陳述式：  
  
```  
SELECT FULLTEXTCATALOGPROPERTY('AdvWksDocFTCat', 'Populatestatus');  
```  
  
 一般而言，如果完整母體擴展進行中，傳回的結果會是 1。  
  
  
##  <a name="example-setting-up-full-text-search"></a><a name="example"></a>範例：設定全文檢索搜尋  
 下列兩部分的範例會針對 AdventureWorks 資料庫建立名為 `AdvWksDocFTCat` 的全文檢索目錄，然後針對 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的 `Document` 資料表建立全文檢索索引。 這個陳述式會在安裝期間所指定的預設目錄中建立全文檢索目錄。 名為 `AdvWksDocFTCat` 的資料夾位於預設的目錄中。  
  
1.  為了建立名為 `AdvWksDocFTCat`的全文檢索目錄，此範例會使用 [CREATE FULLTEXT CATALOG](/sql/t-sql/statements/create-fulltext-catalog-transact-sql) 陳述式：  
  
    ```  
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
  
2.  針對 Document 資料表建立全文檢索索引之前，請確定此資料表具有唯一、單一資料行且不可為 Null 的索引。 下列 [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 陳述式會針對 Document 資料表的 DocumentID 資料行建立唯一索引 `ui_ukDoc`：  
  
    ```  
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  
  
3.  在您擁有唯一索引鍵之後，就可以使用下列 `Document` CREATE FULLTEXT INDEX [陳述式，針對](/sql/t-sql/statements/create-fulltext-index-transact-sql) 資料表建立全文檢索索引。  
  
    ```  
    CREATE FULLTEXT INDEX ON Production.Document  
    (  
        Document                         --Full-text index column name   
            TYPE COLUMN FileExtension    --Name of column that contains file type information  
            Language 2057                 --2057 is the LCID for British English  
    )  
    KEY INDEX ui_ukDoc ON AdvWksDocFTCat --Unique index  
    WITH CHANGE_TRACKING AUTO            --Population type;  
    GO  
  
    ```  
  
     在這個範例中定義的 TYPE COLUMN 會在資料表中指定類型資料行，其中在 'Document' 資料行的每個資料列中包含文件類型 (二進位類型)。 類型資料行會在給定的資料列中儲存使用者提供的副檔名-".doc"、".xls" 等等檔。 全文檢索引擎會使用給定資料列中的副檔名來叫用正確的篩選，以便用於剖析該資料列中的資料。 在此篩選已經剖析資料列的二進位資料之後，指定的斷詞工具將會剖析內容 (在此範例中，將會使用英式英文的斷詞工具)。 請注意，當全文檢索索引已啟用自動變更追蹤時，篩選程序只會在建立索引時進行，或在使用者於基底資料表中插入或更新資料行時進行。 如需詳細資訊，請參閱 [設定及管理搜尋的篩選](configure-and-manage-filters-for-search.md)。  
  
  
##  <a name="common-tasks"></a><a name="tasks"></a>一般工作  
  
### <a name="to-create-a-full-text-catalog"></a>建立全文檢索目錄  
  
-   [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)  
  
-   [建立及管理全文檢索目錄](create-and-manage-full-text-catalogs.md)  
  
### <a name="to-view-the-indexes-of-a-table-or-view"></a>檢視資料表 (或檢視表) 的索引  
  
-   [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
### <a name="to-create-a-unique-index"></a>建立唯一的索引  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [開啟資料表設計工具 &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)  
  
### <a name="to-create-a-full-text-index"></a>建立全文檢索索引  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
-   [建立及管理全文檢索索引](create-and-manage-full-text-indexes.md)  
  
### <a name="to-view-information-about-a-full-text-index"></a>檢視全文檢索索引的詳細資訊  
  
|目錄或動態管理檢視|描述|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql)|針對通往全文檢索索引參考的每個全文檢索目錄，各傳回一個資料列。|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)|屬於全文檢索索引一部分的每個資料行各有一個資料列。|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql)|全文檢索索引會使用稱為「全文檢索索引片段」的內部資料表來儲存反向索引資料。 此檢視表可用來查詢有關這些片段的中繼資料， 此檢視表針對每一個資料表內包含全文檢索索引的每一個全文檢索索引片段各包含一個資料列。|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql)|針對表格式物件的每個全文檢索索引，各包含一個資料列。|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql)|針對指定的資料表傳回全文檢索索引之內容的相關資訊。|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql)|針對指定的資料表傳回全文檢索索引之文件層級內容的相關資訊。 給定的關鍵字可能會出現在許多份文件中。|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql)|傳回有關目前進行中之全文檢索索引母體擴展的資訊。|  
  
  
## <a name="see-also"></a>另請參閱  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-catalog-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [建立全文檢索停用字詞表 &#40;Transact-sql&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [填入全文檢索索引](populate-full-text-indexes.md)   
 [FULLTEXTCATALOGPROPERTY &#40;Transact-sql&#41;](/sql/t-sql/functions/fulltextcatalogproperty-transact-sql)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)  
  
  
