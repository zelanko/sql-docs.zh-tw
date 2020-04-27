---
title: 管理全文檢索索引 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 459bdc20c9698a8b6271092c57ed0de936c4d7f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775040"
---
# <a name="manage-full-text-indexes"></a>管理全文檢索索引
     
##  <a name="viewing-and-changing-the-properties-of-a-full-text-index"></a><a name="view"></a>查看和變更全文檢索索引的屬性  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>在 Management Studio 中檢視或變更全文檢索索引的屬性  
  
1.  在 [物件總管] 中，展開伺服器。  
  
2.  展開 [資料庫]  ，然後展開包含全文檢索索引的資料庫。  
  
3.  展開 **[資料表]** 。  
  
4.  以滑鼠右鍵按一下已定義全文檢索索引的資料表、選取 [全文檢索索引]  ，然後按一下 [全文檢索索引]  內容功能表上的 [屬性]  。 這樣就會開啟 [全文檢索索引屬性]  對話方塊。  
  
5.  在 **[選取頁面]** 窗格中，您可以選取下列任何頁面：  
  
    |頁面|描述|  
    |----------|-----------------|  
    |**一般**|顯示全文檢索索引的基本屬性。 這些屬性包括許多可修改的屬性和一些無法變更的屬性，例如資料庫名稱、資料表名稱，以及全文檢索索引鍵資料行的名稱。 可修改的屬性包括：<br /><br /> **全文檢索索引停用字詞表**<br /><br /> **全文檢索索引已啟用**<br /><br /> **變更追蹤**<br /><br /> **搜尋屬性清單**<br /><br /> <br /><br /> 如需詳細資訊，請參閱[全文檢索搜尋 &#40;一般頁面&#41;](full-text-index-properties-general-page.md)。|  
    |**資料行**|顯示可用於全文檢索索引的資料表資料行。 系統會針對選取的資料行建立全文檢索索引。 您可以選取任意數目的可用資料行，以便包含在全文檢索索引中。 如需詳細資訊，請參閱[全文檢索搜尋 &#40;資料行頁面&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md)。|  
    |**排程**|您可以使用這個頁面來建立或管理 SQL Server Agent 作業的排程，以便針對全文檢索索引母體擴展啟動累加資料表母體擴展。 如需詳細資訊，請參閱 [擴展全文檢索索引](../relational-databases/indexes/indexes.md)。<br /><br /> <strong> \* \*重要\*事項</strong>當您結束 [**全文檢索索引屬性**] 對話方塊之後，任何新建立的排程都會與 SQL Server Agent 作業相關聯（在*database_name*上啟動累加資料表擴展。*table_name*）。|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] 儲存任何變更並結束 [全文檢索索引屬性]  對話方塊。  
  
##  <a name="viewing-the-properties-of-indexed-tables-and-columns"></a><a name="props"></a>查看索引資料表和資料行的屬性  
 您可以使用許多 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數 (例如 OBJECTPROPERTYEX) 以取得各種全文檢索索引屬性的值。 此資訊適用於管理和疑難排解全文檢索搜尋。  
  
 下表列出索引資料表和資料行的相關全文檢索屬性及其相關的 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數。  
  
|屬性|描述|函式|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|在資料表中，用來保存資料行文件類型資訊的 TYPE COLUMN。|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|資料行是否已啟用全文檢索索引。|COLUMNPROPERTY|  
|`IsFulltextKey`|索引是否為資料表的全文檢索索引鍵。|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|資料表是否擁有全文檢索的背景更新索引。|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|資料表之全文檢索索引資料所在的全文檢索目錄識別碼。|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|資料表是否已啟用全文檢索變更追蹤。|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|全文檢索索引啟動之後所處理的資料列數。|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|全文檢索搜尋未建立索引的資料列數。|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|已順利建立全文檢索索引的資料列數。|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|全文檢索唯一索引鍵資料行的資料行識別碼。|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|具有全文檢索索引的資料表目前是否正在合併。|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|要處理的暫止變更追蹤項目數。|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|全文檢索資料表的母體擴展狀態。|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|資料表是否擁有使用中全文檢索索引。|OBJECTPROPERTYEX|  
  
##  <a name="getting-information-about-the-full-text-key-column"></a><a name="key"></a>取得全文檢索索引鍵資料行的相關資訊  
 一般而言，CONTAINSTABLE 或 FREETEXTTABLE 資料列集值函數的結果必須與基底資料表聯結。 在這種情況下，您必須知道唯一索引鍵資料行名稱。 您可以查詢給定的唯一索引是否當做全文檢索索引鍵使用，而且可以取得全文檢索索引鍵資料行的識別碼。  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>若要查詢給定的唯一索引是否當做全文檢索索引鍵資料行使用  
  
1.  使用 [SELECT](/sql/t-sql/queries/select-transact-sql) 陳述式來呼叫 [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql) 函數。 在函式呼叫中，使用 OBJECT_ID 函數，將資料表的名稱（*table_name*）轉換成資料表識別碼、指定資料表的唯一索引名稱，以及指定`IsFulltextKey`索引屬性，如下所示：  
  
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
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>尋找全文檢索索引鍵資料行的識別碼  
  
1.  每個啟用全文檢索的資料表都具有一個用來強制資料表之唯一資料列的資料行 (*unique**key column*)。 從 OBJECTPROPERTYEX 函數中取得的 `TableFulltextKeyColumn` 屬性會包含唯一索引鍵資料行的資料行識別碼。  
  
     若要取得這個識別碼，您可以使用 SELECT 陳述式來呼叫 OBJECTPROPERTYEX 函數。 使用 OBJECT_ID 函數，將資料表的名稱（*table_name*）轉換成資料表識別碼，並指定`TableFulltextKeyColumn`屬性，如下所示：  
  
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
  
##  <a name="disabling-or-re-enabling-a-table-for-full-text-indexing"></a><a name="disable"></a>停用或重新啟用全文檢索索引的資料表  
 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中，所有使用者建立的資料庫預設都會啟用全文檢索。 此外，個別資料表也會在建立全文檢索索引並將資料行加入索引中後，立即自動啟用全文檢索索引。 從全文檢索索引中卸除最後一個資料行之後，資料表便會自動停用全文檢索索引。  
  
 在具有全文檢索索引的資料表上，您可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]來手動為資料表停用或重新啟用全文檢索索引。  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>為資料表啟用全文檢索索引  
  
1.  展開伺服器群組、展開 [資料庫]  ，再展開包含您要啟用全文檢索索引之資料表的資料庫。  
  
2.  展開 [資料表]  ，然後以滑鼠右鍵按一下您想要停用或重新啟用全文檢索索引的資料表。  
  
3.  選取 [全文檢索索引]  ，然後按一下 [停用全文檢索索引]  或 [啟用全文檢索索引]  。  
  
##  <a name="removing-a-full-text-index-from-a-table"></a><a name="remove"></a>從資料表移除全文檢索索引  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>移除資料表的全文檢索索引  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下含有您要移除其全文檢索索引的資料表。  
  
2.  選取 [刪除全文檢索索引]  。  
  
3.  出現提示要您確認是否要刪除全文檢索索引時，按一下 [確定]  。  
  
  
