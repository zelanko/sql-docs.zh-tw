---
title: 全文檢索搜尋使用者入門 | Microsoft Docs
ms.date: 08/22/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text indexes [SQL Server], creating
- full-text search [SQL Server], about
- full-text search [SQL Server], setting up
ms.assetid: 1fa628ba-0ee4-4d8f-b086-c4e52962ca4a
caps.latest.revision: 76
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 7bab5a23741c000cbc376af1b247b7575353c14d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39558798"
---
# <a name="get-started-with-full-text-search"></a>全文檢索搜尋使用者入門
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
預設會啟用 SQL Server 資料庫的全文檢索功能。 不過，您必須先建立全文檢索目錄，並在您想要搜尋的資料表或索引檢視表上建立全文檢索索引，才能執行全文檢索查詢。

## <a name="set-up-full-text-search-in-two-steps"></a>使用兩個步驟設定全文檢索搜尋
設定全文檢索搜尋有兩個基本步驟︰  
1.  建立全文檢索目錄。  
2.  在您想要搜尋的資料表或索引檢視表上建立全文檢索索引。 

每個全文檢索索引都必須屬於一個全文檢索目錄。 您可以針對每個全文檢索索引建立個別的文字目錄，也可以讓多個全文檢索索引與給定的目錄產生關聯。 全文檢索目錄是虛擬物件，而且不屬於任何檔案群組。 目錄是參考一組全文檢索索引的邏輯概念。

> [!NOTE]
> 這些步驟假設您已在安裝 SQL Server 時安裝選擇性的全文檢索搜尋元件。 否則，請重新執行 SQL Server 安裝程式予以新增。  

## <a name="set-up-full-text-search-with-a-wizard"></a>使用精靈設定全文檢索搜尋 
 
若要使用精靈設定全文檢索搜尋，請參閱[使用全文檢索索引精靈](../../relational-databases/search/use-the-full-text-indexing-wizard.md)。

## <a name="set-up-full-text-search-with-transact-sql"></a>使用 Transact-SQL 設定全文檢索搜尋 
 下列兩部分的範例會針對 AdventureWorks 範例資料庫建立名為 `AdvWksDocFTCat` 的全文檢索目錄，然後針對範例資料庫中的 `Document` 資料表建立全文檢索索引。 這個陳述式會在安裝 SQL Server 期間所指定的預設目錄中建立全文檢索目錄。 名為 `AdvWksDocFTCat` 的資料夾位於預設的目錄中。  
  
1.  為了建立名為 `AdvWksDocFTCat`的全文檢索目錄，此範例會使用 [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md) 陳述式：  
  
    ```sql
    USE AdventureWorks;  
    GO  
    CREATE FULLTEXT CATALOG AdvWksDocFTCat;  
    ```  
    如需詳細資訊，請參閱[建立及管理全文檢索目錄](../../relational-databases/search/create-and-manage-full-text-catalogs.md)。
 
2.  針對 Document 資料表建立全文檢索索引之前，請確定此資料表具有唯一、單一資料行且不可為 Null 的索引。 下列 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 陳述式會針對 Document 資料表的 DocumentID 資料行建立唯一索引 `ui_ukDoc`：  
  
    ```sql 
    CREATE UNIQUE INDEX ui_ukDoc ON Production.Document(DocumentID);  
    ```  

3.  在您擁有唯一索引鍵之後，就可以使用下列 `Document` CREATE FULLTEXT INDEX [陳述式，針對](../../t-sql/statements/create-fulltext-index-transact-sql.md) 資料表建立全文檢索索引。  
  
    ```sql  
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
  
     在這個範例中定義的 TYPE COLUMN 會在資料表中指定類型資料行，其中在 'Document' 資料行的每個資料列中包含文件類型 (二進位類型)。 這個類型資料行會在給定的資料列中儲存使用者提供的文件副檔名，例如 ".doc" 和 ".xls" 等等。 全文檢索引擎會使用給定資料列中的副檔名來叫用正確的篩選，以便用於剖析該資料列中的資料。 在此篩選已經剖析資料列的二進位資料之後，指定的斷詞工具會剖析內容 (在此範例中，將會使用英式英文的斷詞工具)。如需詳細資訊，請參閱 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)。  

    如需詳細資訊，請參閱[建立及管理全文檢索索引](../../relational-databases/search/create-and-manage-full-text-indexes.md)。

##  <a name="options"></a> 選擇全文檢索索引的選項 
  
### <a name="choose-a-language"></a>選擇語言  
 如需選擇資料行語言的資訊，請參閱 [選擇建立全文檢索索引時的語言](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)。  
  
### <a name="choose-a-filegroup"></a>選擇檔案群組  
 建置全文檢索索引的程序需要大量 I/O。 簡而言之，此程序包括從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中讀取資料，然後將篩選的資料傳播至全文檢索索引。 最佳作法是將全文檢索索引放置於最適合將 I/O 效能發揮到極致的資料庫檔案群組中，或是將全文檢索索引放置於另一個磁碟區的不同檔案群組中。
  
### <a name="choose-a-full-text-catalog"></a>選擇全文檢索目錄   
 
 我們建議您在相同的全文檢索目錄底下，將具有相同更新特性的資料表 (例如少量變更與大量變更，或在每日特定時段頻繁變更的資料表) 產生關聯。 透過設定全文檢索目錄的母體擴展排程，在高度資料庫活動期間，全文檢索索引仍然能夠保持與資料表同步，而不會對資料庫伺服器的資源使用量造成負面影響。  
  
 請考慮下列指導方針：  
  
-   如果您正在針對包含數百萬資料列的資料表建立索引，請將此資料表指派給它本身的全文檢索目錄。  
  
-   考慮正在建立全文檢索索引之資料表中發生的變更數量，以及資料列總數。 如果變更的資料列總數，與上次執行全文檢索母體擴展的資料列總和超過百萬，請將此資料表指派給它本身的全文檢索目錄。  

### <a name="associate-a-unique-index"></a>建立與唯一索引的關聯
永遠選取最小的唯一索引，做為全文檢索唯一索引鍵。 (四個位元組的整數式索引最好)。如此可大幅減少 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Search Service 在檔案系統中所需的資源。 如果主索引鍵較大 (超過 101 個位元組) 時，可考慮選擇資料表中其他的唯一索引，做為全文檢索唯一的索引鍵 (或建立另一個唯一索引)。 若全文檢索唯一索引鍵的大小超過允許的最大值 (900 個位元組) 時，將無法執行全文檢索的母體擴展作業。  
 
### <a name="associate-a-stoplist"></a>建立停用字詞表的關聯   
  *「停用字詞表」* (Stoplist) 是停用字詞 (也稱為非搜尋字) 的清單。 停用字詞表會與每個全文檢索索引相關聯，而且該停用字詞表中的字詞會套用至該索引的全文檢索查詢。 根據預設，系統停用字詞表會與新的全文檢索索引相關聯。 您也可以建立並使用自己的停用字詞表。   
  
 例如，下列 [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會透過從系統停用字詞表複製，建立名為 myStoplist 的新全文檢索停用字詞表：  
  
```sql  
CREATE FULLTEXT STOPLIST myStoplist FROM SYSTEM STOPLIST;  
GO  
```  
  
 下列 [ALTER FULLTEXT STOPLIST](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會更改名為 myStoplist 的停用字詞表，並加入 'en' 一詞 (先針對西班牙文，然後再針對法文)：  
  
```sql  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST myStoplist ADD 'en' LANGUAGE 'French';  
GO  
```  
如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。

## <a name="update-a-full-text-index"></a>更新全文檢索索引  
 如同一般 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引，當相關聯資料表中的資料變更時，就可以自動更新全文檢索索引。 這是預設行為。 或者，您也可以手動或以指定的排程間隔將全文檢索索引保持在最新狀態。 擴展全文檢索索引可能會相當耗時而且需要大量資源。 因此，索引更新通常會當作在背景中執行的非同步處理序執行並且在修改基底資料表之後，將全文檢索索引保持在最新狀態。 
 
在基底資料表每次變更之後立即更新全文檢索索引也需要大量資源。 因此，如果您設定更新/插入/刪除的高速率，可能會遇到查詢效能降低的情況。 如果發生這種情況，請考慮排程手動變更追蹤更新，以便偶爾與許多變更保持同步，而非與查詢競爭資源。  
  
如需詳細資訊，請參閱[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。 

## <a name="next-steps"></a>後續步驟
設定 SQL Server 全文檢索搜尋之後，即準備好執行全文檢索查詢。 如需詳細資訊，請參閱[使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)。
