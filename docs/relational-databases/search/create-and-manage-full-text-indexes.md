---
title: 建立及管理全文檢索索引 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 322b3dbc8950749fe74690c9fd375bbcf9a68332
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43076840"
---
# <a name="create-and-manage-full-text-indexes"></a>建立及管理全文檢索索引
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
本主題描述如何建立、填入和管理 SQL Server 中的全文檢索索引。
  
## <a name="prerequisite---create-a-full-text-catalog"></a>先決條件 - 建立全文檢索目錄
您需要有全文檢索目錄，才能建立全文檢索索引。 目錄是一或多個全文檢索索引的虛擬容器。 如需詳細資訊，請參閱[建立及管理全文檢索目錄](../../relational-databases/search/create-and-manage-full-text-catalogs.md)。
  
##  <a name="tasks"></a> 建立、改變或卸除全文檢索索引  
### <a name="create-a-full-text-index"></a>建立全文檢索索引  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
### <a name="alter-a-full-text-index"></a>改變全文檢索索引
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
### <a name="drop-a-full-text-index"></a>卸除全文檢索索引 
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)

## <a name="populate-a-full-text-index"></a>擴展全文檢索索引
建立與維護全文檢索索引的程序稱為「母體擴展」，也稱為「搜耙」。 全文檢索索引母體擴展有三種類型：
-   完整母體擴展
-   以變更追蹤為基礎的母體擴展
-   以時間戳記為基礎的累加母體擴展。

如需詳細資訊，請參閱[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。

##  <a name="view"></a> 檢視全文檢索索引的屬性
### <a name="view-the-properties-of-a-full-text-index-with-transact-sql"></a>使用 Transact-SQL 檢視全文檢索索引的屬性
|目錄或動態管理檢視|Description|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|針對通往全文檢索索引參考的每個全文檢索目錄，各傳回一個資料列。|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|屬於全文檢索索引一部分的每個資料行各有一個資料列。|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|全文檢索索引會使用稱為「全文檢索索引片段」的內部資料表來儲存反向索引資料。 此檢視表可用來查詢有關這些片段的中繼資料， 此檢視表針對每一個資料表內包含全文檢索索引的每一個全文檢索索引片段各包含一個資料列。|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|針對表格式物件的每個全文檢索索引，各包含一個資料列。|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|針對指定的資料表傳回全文檢索索引之內容的相關資訊。|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|針對指定的資料表傳回全文檢索索引之文件層級內容的相關資訊。 給定的關鍵字可能會出現在許多份文件中。|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|傳回有關目前進行中之全文檢索索引母體擴展的資訊。|  
 
### <a name="view-the-properties-of-a-full-text-index-with-management-studio"></a>使用 Management Studio 檢視全文檢索索引的屬性 
1.  在 Management Studio 中，於物件總管中展開伺服器。  
  
2.  展開 [資料庫]，然後展開包含全文檢索索引的資料庫。  
  
3.  展開 **[資料表]**。  
  
4.  以滑鼠右鍵按一下已定義全文檢索索引的資料表、選取 [全文檢索索引]，然後按一下 [全文檢索索引] 內容功能表上的 [屬性]。 這樣就會開啟 [全文檢索索引屬性] 對話方塊。  
  
5.  在 **[選取頁面]** 窗格中，您可以選取下列任何頁面：  
  
    |頁面|Description|  
    |----------|-----------------|  
    |**一般**|顯示全文檢索索引的基本屬性。 這些屬性包括許多可修改的屬性和一些無法變更的屬性，例如資料庫名稱、資料表名稱，以及全文檢索索引鍵資料行的名稱。 可修改的屬性包括：<br /><br /> **全文檢索索引停用字詞表**<br /><br /> **全文檢索索引已啟用**<br /><br /> **變更追蹤**<br /><br /> **搜尋屬性清單**<br /><br />如需詳細資訊，請參閱[全文檢索索引屬性 &#40;一般頁面&#41;](http://msdn.microsoft.com/library/f4dff61c-8c2f-4ff9-abe4-70a34421448f)。|  
    |**資料行**|顯示可用於全文檢索索引的資料表資料行。 系統會針對選取的資料行建立全文檢索索引。 您可以選取任意數目的可用資料行，以便包含在全文檢索索引中。 如需詳細資訊，請參閱[全文檢索索引屬性 &#40;資料行頁面&#41;](http://msdn.microsoft.com/library/75e52edb-0d07-4393-9345-8b5af4561e35)。|  
    |**排程**|您可以使用這個頁面來建立或管理 SQL Server Agent 作業的排程，以便針對全文檢索索引母體擴展啟動累加資料表母體擴展。 如需詳細資訊，請參閱[擴展全文檢索索引](../../relational-databases/search/populate-full-text-indexes.md)。<br /><br /> 注意：在您結束 [全文檢索索引屬性] 對話方塊之後，任何新建立的排程都會與 SQL Server Agent 作業 (針對 *database_name*.*table_name* 啟動 [累加資料表母體]) 相關聯。|  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 儲存任何變更並結束 [全文檢索索引屬性] 對話方塊。  
  
##  <a name="props"></a> 檢視索引資料表和資料行的屬性  
 您可以使用許多 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數 (例如 OBJECTPROPERTYEX) 以取得各種全文檢索索引屬性的值。 此資訊適用於管理和疑難排解全文檢索搜尋。  
  
 下表列出索引資料表和資料行的相關全文檢索屬性及其相關的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數。  
  
|屬性|Description|函數|  
|--------------|-----------------|--------------|  
|**FullTextTypeColumn**|在資料表中，用來保存資料行文件類型資訊的 TYPE COLUMN。|[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)|  
|**IsFulltextIndexed**|資料行是否已啟用全文檢索索引。|COLUMNPROPERTY|  
|**IsFulltextKey**|索引是否為資料表的全文檢索索引鍵。|[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)|  
|**TableFulltextBackgroundUpdateIndexOn**|資料表是否擁有全文檢索的背景更新索引。|[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)|  
|**TableFulltextCatalogId**|資料表之全文檢索索引資料所在的全文檢索目錄識別碼。|OBJECTPROPERTYEX|  
|**TableFulltextChangeTrackingOn**|資料表是否已啟用全文檢索變更追蹤。|OBJECTPROPERTYEX|  
|**TableFulltextDocsProcessed**|全文檢索索引啟動之後所處理的資料列數。|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|全文檢索搜尋未建立索引的資料列數。|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|已順利建立全文檢索索引的資料列數。|OBJECTPROPERTYEX|  
|**TableFulltextKeyColumn**|全文檢索唯一索引鍵資料行的資料行識別碼。|OBJECTPROPERTYEX|  
|**TableFullTextMergeStatus**|具有全文檢索索引的資料表目前是否正在合併。|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|要處理的暫止變更追蹤項目數。|OBJECTPROPERTYEX|  
|**TableFulltextPopulateStatus**|全文檢索資料表的母體擴展狀態。|OBJECTPROPERTYEX|  
|**TableHasActiveFulltextIndex**|資料表是否擁有使用中全文檢索索引。|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> 取得全文檢索索引鍵資料行的資訊  
 一般而言，CONTAINSTABLE 或 FREETEXTTABLE 資料列集值函數的結果必須與基底資料表聯結。 在這種情況下，您必須知道唯一索引鍵資料行名稱。 您可以查詢給定的唯一索引是否當做全文檢索索引鍵使用，而且可以取得全文檢索索引鍵資料行的識別碼。  
  
### <a name="determine-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>判斷給定的唯一索引是否當做全文檢索索引鍵資料行使用  
  
使用 [SELECT](../../t-sql/queries/select-transact-sql.md) 陳述式來呼叫 [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) 函數。 在函數呼叫中，使用 OBJECT_ID 函數，將資料表的名稱 (*table_name*) 轉換成資料表識別碼、指定資料表之唯一索引的名稱，以及指定 **IsFulltextKey** 索引屬性，如下所示：  
  
```  
SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
```  
  
 如果索引是用來強制全文檢索索引鍵資料行的唯一性，這個陳述式就會傳回 1。如果不是，便傳回 0。  
  
 **範例**  
  
 下列範例會查詢 `PK_Document_DocumentID` 索引是否用來強制全文檢索索引鍵資料行的唯一性，如下所示：  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 如果 `PK_Document_DocumentID` 索引是用來強制全文檢索索引鍵資料行的唯一性，這個範例就會傳回 1。 否則，它會傳回 0 或 NULL。 NULL 表示您正在使用無效的索引名稱、索引名稱沒有對應至資料表，或者資料表不存在等。  
  
### <a name="find-the-identifier-of-the-full-text-key-column"></a>尋找全文檢索索引鍵資料行的識別碼  
  
每個啟用全文檢索的資料表都具有一個用來強制資料表之唯一資料列的資料行 (*unique**key column*)。 從 OBJECTPROPERTYEX 函數中取得的 **TableFulltextKeyColumn** 屬性會包含唯一索引鍵資料行的資料行識別碼。  
 
若要取得這個識別碼，您可以使用 SELECT 陳述式來呼叫 OBJECTPROPERTYEX 函數。 請使用 OBJECT_ID 函數，將資料表的名稱 (*table_name*) 轉換成資料表識別碼，並且指定 **TableFulltextKeyColumn** 屬性，如下所示：  
  
```  
SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
```  
  
 **範例**  
  
 下列範例會傳回全文檢索索引鍵資料行的識別碼或 NULL。 NULL 表示您正在使用無效的索引名稱、索引名稱沒有對應至資料表，或者資料表不存在等。  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 下列範例顯示如何使用唯一索引鍵資料行的識別碼，以取得資料行的名稱。  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 這個範例會傳回名為 `Unique Key Column`的結果集資料行，其中顯示包含 Document 資料表之唯一索引鍵資料行名稱的單一資料列 DocumentID。 請注意，如果這個查詢包含無效的索引名稱、索引名稱沒有對應至資料表，或者資料表不存在等，它就會傳回 NULL。  

## <a name="index-varbinarymax-and-xml-columns"></a>索引 varbinary(max) 和 xml 資料行  
 如果已建立 **varbinary(max)**、**varbinary** 或  資料行的全文檢索索引，您就可以使用全文檢索述詞 (CONTAINS 和 FREETEXT) 與函數 (CONTAINSTABLE 和 FREETEXTTABLE) 來查詢它，就像查詢任何其他全文檢索索引資料行一樣。
   
### <a name="index-varbinarymax-or-varbinary-data"></a>索引 varbinary(max) 或 varbinary 資料  
 單一 **varbinary(max)** 或 **varbinary** 資料行可以儲存許多類型的文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援已在作業系統中安裝並提供篩選的任何文件類型。 每份文件的文件類型都是由文件的副檔名所識別。 例如，全文檢索搜尋會針對 .doc 副檔名使用支援 Microsoft Word 文件的篩選。 如需可用文件類型的清單，請查詢 [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) 目錄檢視。  
  
請注意，全文檢索引擎可以運用安裝在作業系統中的現有篩選。 您必須先將作業系統篩選、斷詞工具和字幹分析器載入伺服器執行個體中，然後才能使用它們，如下所示：  
  
```sql  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
若要針對 **varbinary(max)** 資料行建立全文檢索索引，全文檢索引擎需要 **varbinary(max)** 資料行中文件副檔名的存取權。 這項資訊必須儲存在稱為類型資料行的資料表資料行中，而此資料行必須與全文檢索索引中的 **varbinary(max)** 資料行相關聯。 建立文件的索引時，全文檢索引擎會使用類型資料行中的副檔名來識別要使用的篩選。  
   
### <a name="index-xml-data"></a>索引 xml 資料  
 **xml** 資料類型資料行只會儲存 XML 文件和片段，而且只有 XML 篩選會用於這些文件。 因此，類型資料行是不必要的。 在 **xml** 資料行上，全文檢索索引會建立 XML 元素內容的索引，但忽略 XML 標記。 屬性值是全文檢索索引的值 (除非它們是數值)。 元素標記會當做 Token 界限來使用。 系統支援包含多種語言且格式正確的 XML 或 HTML 文件和片段。  
  
 如需編製索引和查詢 **xml** 資料行的詳細資訊，請參閱[使用 XML 資料行進行全文檢索搜尋](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)。  
  
##  <a name="disable"></a> 停用或重新啟用資料表的全文檢索索引   
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，所有使用者建立的資料庫預設都會啟用全文檢索。 此外，個別資料表也會在建立全文檢索索引並將資料行加入索引中後，立即自動啟用全文檢索索引。 從全文檢索索引中卸除最後一個資料行之後，資料表便會自動停用全文檢索索引。  
  
 在具有全文檢索索引的資料表上，您可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來手動為資料表停用或重新啟用全文檢索索引。  

1.  展開伺服器群組、展開 [資料庫]，再展開包含您要啟用全文檢索索引之資料表的資料庫。  
  
2.  展開 [資料表]，然後以滑鼠右鍵按一下您想要停用或重新啟用全文檢索索引的資料表。  
  
3.  選取 [全文檢索索引]，然後按一下 [停用全文檢索索引] 或 [啟用全文檢索索引]。  
  
##  <a name="remove"></a> 移除資料表的全文檢索索引  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下含有您要移除其全文檢索索引的資料表。  
  
2.  選取 [刪除全文檢索索引]。  
  
3.  出現提示要您確認是否要刪除全文檢索索引時，按一下 [確定]。  
  
  
