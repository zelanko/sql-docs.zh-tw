---
title: sys.dm_fts_parser (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_parser_TSQL
- dm_fts_parser
- dm_fts_parser_TSQL
- sys.dm_fts_parser
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_parser dynamic management function
- troubleshooting [SQL Server], full-text search
ms.assetid: 2736d376-fb9d-4b28-93ef-472b7a27623a
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c080381584a2e66634ff50517a13d54f59ffc673
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmftsparser-transact-sql"></a>sys.dm_fts_parser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  套用之後，傳回的最終 token 化結果指定[斷詞工具](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)，[同義字](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)，和[停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)組合來查詢字串輸入。 Token 化結果就相當於指定之查詢字串的全文檢索引擎輸出。  
  
 sys.dm_fts_parser 是動態管理函數。  
  
## <a name="syntax"></a>語法  
  
```  
  
sys.dm_fts_parser('query_string', lcid, stoplist_id, accent_sensitivity)  
```  
  
## <a name="arguments"></a>引數  
 *query_string*  
 您想要剖析的查詢。 *query_string*可以是您的字串鏈結[CONTAINS](../../t-sql/queries/contains-transact-sql.md)語法支援。 例如，您可以包含字形變化、同義字和邏輯運算子。  
  
 *lcid*  
 要用於剖析之斷詞工具的地區設定識別碼 (LCID) *query_string*。  
  
 *stoplist_id*  
 停用字詞表，如果所識別之斷詞工具所使用的任何識別碼*lcid*。 *stoplist_id*是**int**。如果您指定了 'NULL'，就不會使用任何停用字詞表。 如果您指定了 0，就會使用系統 STOPLIST。  
  
 停用字詞表識別碼在資料庫內是唯一的。 若要取得在指定的資料表使用全文檢索索引的停用字詞表識別碼[sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)目錄檢視。  
  
 *accent_sensitivity*  
 可控制全文檢索搜尋是否區分變音符號的布林值。 *accent_sensitivity*是**元**，使用下列值之一：  
  
|Value|是否區分腔調字…|  
|-----------|----------------------------|  
|0|不區分<br /><br /> "café" 和 "cafe" 等字會視為完全相同。|  
|1|[值]<br /><br /> "café" 和 "cafe" 等字會視為不同。|  
  
> [!NOTE]  
>  若要檢視全文檢索目錄的這個值的目前設定，執行下列命令[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式： `SELECT fulltextcatalogproperty('` *catalog_name*`', 'AccentSensitivity');`。  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|關鍵字 (keyword)|**varbinary(128)**|斷詞工具所傳回之給定關鍵字的十六進位表示法。 這個表示法是用來將關鍵字儲存在全文檢索索引中。 這個值不是人們可讀取，但它可用於傳回全文檢索索引的內容，例如其他動態管理檢視與給定的關鍵字來輸出傳回[sys.dm_fts_index_keywords](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)和[sys.dm_fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)。<br /><br /> **注意：** OxFF 代表指出檔案或資料集的結尾的特殊字元。|  
|group_id|**int**|包含可用於區分從中產生給定詞彙之邏輯群組的整數值。 例如，'`Server AND DB OR FORMSOF(THESAURUS, DB)"`' 會使用英文產生下列 group_id 值：<br /><br /> 1： 伺服器<br />2: DB<br />3: DB|  
|phrase_id|**int**|包含可用於區分斷詞工具發出複合字 (例如 full-text) 之替代形式所處情況的整數值。 有時候，如果存在複合字 ('multi-million')，斷詞工具就會發出替代形式。 這些替代形式 (片語) 有時必須加以區別。<br /><br /> 例如，'`multi-million`' 會使用英文產生下列 phrase_id 值：<br /><br /> 1。 `multi`<br />1。 `million`<br />2 `multimillion`|  
|occurrence|**int**|指出剖析結果中每個詞彙的順序。 例如，若為 "`SQL Server query processor`" 片語，occurrence 就會使用英文針對此片語中的詞彙包含下列 occurrence 值：<br /><br /> 1。 `SQL`<br />2 `Server`<br />3 `query`<br />4 個 `processor`|  
|special_term|**nvarchar(4000)**|包含斷詞工具所發出之詞彙特性的相關資訊，它有下列幾種：<br /><br /> 完全相符<br /><br /> 非搜尋字<br /><br /> 句子的結尾<br /><br /> 段落的結尾<br /><br /> 章節的結尾|  
|display_term|**nvarchar(4000)**|包含關鍵字的人們可讀取形式。 如同設計成存取全文檢索索引內容的函數，由於非正規化限制，所以這個顯示的詞彙可能不會與原始詞彙完全相同。 不過，它的精確程度應該足以協助您從原始輸入中識別出該詞彙。|  
|expansion_type|**int**|包含給定詞彙之展開本質的相關資訊，它有下列幾種：<br /><br /> 0 = 單一字詞大小寫<br /><br /> 2 = 字形展開<br /><br /> 4 = 同義字展開/取代<br /><br /> 例如，假設同義字定義當做 `jog` 之展開執行的情況：<br /><br /> `<expansion>`<br /><br /> `<sub>run</sub>`<br /><br /> `<sub>jog</sub>`<br /><br /> `</expansion>`<br /><br /> `FORMSOF (FREETEXT, run)` 一詞會產生下列輸出：<br /><br /> `run` 而且 expansion_type=0<br /><br /> `runs` 而且 expansion_type=2<br /><br /> `running` 而且 expansion_type=2<br /><br /> `ran` 而且 expansion_type=2<br /><br /> `jog` 而且 expansion_type=4|  
|source_term|**nvarchar(4000)**|從中產生或剖析給定詞彙的詞彙或片語。 例如，'"`word breakers" AND stemmers'` 的查詢會使用英文產生下列 source_term 值：<br /><br /> `word breakers` 如 display_term`word`<br />`word breakers` 如 display_term`breakers`<br />`stemmers` 如 display_term`stemmers`|  
  
## <a name="remarks"></a>備註  
 **sys.dm_fts_parser**支援的語法和功能的全文檢索述詞，例如[CONTAINS](../../t-sql/queries/contains-transact-sql.md)和[FREETEXT](../../t-sql/queries/freetext-transact-sql.md)，和函式，例如[CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)和[FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md)。  
  
## <a name="using-unicode-for-parsing-special-characters"></a>使用 Unicode 剖析特殊字元  
 當您剖析查詢字串， **sys.dm_fts_parser**會使用您所連接，資料庫的定序，除非您將查詢字串指定為 Unicode。 因此，非 Unicode 字串，其中包含特殊字元，例如 ü 或 ç，輸出可能是預期的情況下，根據資料庫的定序。 若要處理資料庫定序的查詢字串，字串前面加上`N`，也就是`N'` *query_string*`'`。  
  
 如需詳細資訊，請參閱本主題稍後的 「顯示包含特殊字元之字串的輸出」。  
  
## <a name="when-to-use-sysdmftsparser"></a>何時使用 sys.dm_fts_parser  
 **sys.dm_fts_parser**可能非常強大的偵錯之用。 某些主要的使用狀況包括：  
  
-   了解給定的斷詞工具如何處理給定的輸入  
  
     當查詢傳回非預期的結果時，可能的原因就是斷詞工具正在剖析資料和進行斷詞。 透過使用 sys.dm_fts_parser，您就可以探索斷詞工具傳遞給全文檢索索引的結果。 此外，您可以查看哪些詞彙是不會在全文檢索索引中搜尋的停用字詞。 給定的語言取決於它是否在指定的停用字詞表中某個詞彙是否停用字詞*stoplist_id*函式中宣告的值。  
  
     此外，請注意區分腔調字旗標，這個旗標會允許使用者查看斷詞工具如何在記住區分腔調字資訊時剖析輸入。  
  
-   了解字幹分析器如何針對給定的輸入運作  
  
     您可以透過指定包含下列 FORMSOF 子句的 CONTAINS 或 CONTAINSTABLE 查詢，了解斷詞工具和字幹分析器如何剖析查詢詞彙及其字幹形式：  
  
    ```  
    FORMSOF( INFLECTIONAL, query_term )  
    ```  
  
     結果將會告知您哪些詞彙正傳遞給全文檢索索引。  
  
-   了解同義字如何展開或取代所有或部分輸入  
  
     您也可以指定：  
  
    ```  
    FORMSOF( THESAURUS, query_term )  
    ```  
  
     這項查詢的結果顯示斷詞工具和同義字如何針對查詢詞彙進行互動。 您可以從同義字中查看展開或取代，而可識別實際針對全文檢索索引發出的結果查詢。  
  
     請注意，如果使用者發出：  
  
    ```  
    FORMSOF( FREETEXT, query_term )  
    ```  
  
     字形和同義字功能就會自動生效。  
  
 除了上述使用狀況以外，sys.dm_fts_parser 可以有效地協助您了解並疑難排解全文檢索查詢的許多其他問題。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定伺服器角色與存取權限指定的停用字詞表。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-the-output-of-a-given-word-breaker-for-a-keyword-or-phrase"></a>A. 針對關鍵字或片語，顯示給定之斷詞工具的輸出  
 下列範例會傳回使用英文斷詞工具 (其 LCID 為 1033) 的輸出，但是不會傳回下列查詢字串的停用字詞表：  
  
 `The Microsoft business analysis`  
  
 區分腔調字已停用。  
  
```  
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis" ', 1033, 0, 0);  
```  
  
### <a name="b-displaying-the-output-of-a-given-word-breaker-in-the-context-of-stoplist-filtering"></a>B. 在停用字詞表篩選的內容中，顯示給定之斷詞工具的輸出  
 下列範例會傳回使用英文斷詞工具 (其 LCID 為 1033) 的輸出，以及下列查詢字串的英文停用字詞表 (其識別碼為 77)：  
  
 `"The Microsoft business analysis" OR "MS revenue"`  
  
 區分腔調字已停用。  
  
```  
SELECT * FROM sys.dm_fts_parser (' "The Microsoft business analysis"  OR " MS revenue" ', 1033, 77, 0);  
```  
  
### <a name="c-displaying-the-output-of-a-string-that-contains-special-characters"></a>C. 顯示包含特殊字元之字串的輸出  
 下列範例使用 Unicode 剖析下列的法文字串:  
  
 `français`  
  
 此範例為法文指定 LCID `1036`，以及使用者定義停用字詞表的識別碼 `5`。 區分腔調字已啟用。  
  
```  
SELECT * FROM sys.dm_fts_parser(N'français', 1036, 5, 1);  
```  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋和語意搜尋動態管理檢視與函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)   
 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [設定及管理全文檢索搜尋的同義字檔案](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md)   
 [設定及管理全文檢索搜尋停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [使用全文檢索搜尋進行查詢](../../relational-databases/search/query-with-full-text-search.md)   
 [安全性實體](../../relational-databases/security/securables.md)  
  
  
