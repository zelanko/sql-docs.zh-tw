---
title: "ALTER SEARCH PROPERTY LIST (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SEARCH_PROPERTY_TSQL
- ALTER_SEARCH_PROPERTY_LIST_TSQL
- ALTER SEARCH PROPERTY LIST
- ALTER SEARCH PROPERTY
- ALTER_SEARCH_TSQL
- ALTER SEARCH
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search property lists [SQL Server], altering
- ALTER SEARCH PROPERTY LIST statement
ms.assetid: 0436e4a8-ca26-4d23-93f1-e31e2a1c8bfb
caps.latest.revision: 55
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c93a8382bec0746ae3cfb8f43485da53a06184f0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="alter-search-property-list-transact-sql"></a>ALTER SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將指定的搜尋屬性加入至搜尋屬性清單，或從中卸除它。  
  
## <a name="syntax"></a>語法  
  
```  
ALTER SEARCH PROPERTY LIST list_name  
{  
   ADD 'property_name'  
     WITH   
      (   
          PROPERTY_SET_GUID = 'property_set_guid'  
        , PROPERTY_INT_ID = property_int_id  
      [ , PROPERTY_DESCRIPTION = 'property_description' ]  
      )  
 | DROP 'property_name'   
}  
;  
```  
  
## <a name="arguments"></a>引數  
 *list_name*  
 這是要改變之屬性清單的名稱。 *list_name*是識別項。  
  
 若要檢視現有屬性清單的名稱，請使用[sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)目錄檢視，如下：  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
 ADD  
 將指定的搜尋屬性加入至所指定的屬性清單*list_name*。 屬性會註冊為搜尋屬性清單。 相關的全文檢索索引必須重新擴展，新加入的屬性才能用於屬性搜尋。 如需詳細資訊，請參閱 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)。  
  
> [!NOTE]  
>  若要將給定的搜尋屬性加入至搜尋屬性清單中，您必須提供其屬性集 GUID (*property_set_guid*) 和屬性 int 識別碼 (*property_int_id*)。 如需詳細資訊，請參閱本主題稍後的＜取得屬性集 GUID 和識別碼＞。  
  
 *property_name*  
 指定要用以識別全文檢索查詢中之屬性的名稱。 *property_name*必須唯一識別屬性集內的屬性。 屬性名稱可以包含內部空格。 最大長度*property_name*為 256 個字元。 這個名稱可以是使用者易記的名稱，例如作者 」 或 「 住家地址，或者它可以是 Windows 正式名稱的屬性，例如**System.Author**或**System.Contact.HomeAddress**。  
  
 開發人員必須使用您指定的值*property_name*來識別中的屬性[CONTAINS](../../t-sql/queries/contains-transact-sql.md)述詞。 因此，當加入務必指定有意義地表示指定的屬性所定義的屬性值的屬性集 GUID (*property_set_guid*) 和屬性的識別項 (*property_int_id*)。 如需有關屬性名稱的詳細資訊，請參閱本主題稍後的＜備註＞。  
  
 若要檢視目前存在之屬性的名稱在目前資料庫的搜尋屬性清單，請使用[sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)目錄檢視，如下：  
  
```  
SELECT property_name FROM sys.registered_search_properties;  
```  
  
 PROPERTY_SET_GUID ='*property_set_guid*'  
 指定屬性所屬之屬性集的識別碼。 這是全域唯一識別碼 (GUID)。 如需有關取得此值的詳細資訊，請參閱本主題稍後的＜備註＞。  
  
 若要檢視屬性，請在目前資料庫中，使用的搜尋屬性清單中設定任何存在之屬性的 GUID [sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)目錄檢視，如下：  
  
```  
SELECT property_set_guid FROM sys.registered_search_properties;  
```  
  
 PROPERTY_INT_ID =*property_int_id*  
 指定屬性集內識別屬性的整數。 如需有關取得此值的詳細資訊，請參閱＜備註＞。  
  
 若要檢視任何存在之屬性的整數識別碼在目前資料庫的搜尋屬性清單，請使用[sys.registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)目錄檢視，如下：  
  
```  
SELECT property_int_id FROM sys.registered_search_properties;  
```  
  
> [!NOTE]  
>  指定的組合*property_set_guid*和*property_int_id*必須是唯一的搜尋屬性清單中。 如果您嘗試加入現有的組合，ALTER SEARCH PROPERTY LIST 作業就會失敗並發出錯誤。 這表示您只能定義給定屬性的一個名稱。  
  
 PROPERTY_DESCRIPTION ='*property_description*'  
 指定使用者定義的屬性描述。 *property_description*是最多 512 個字元的字串。 此選項是選擇性的。  
  
 DROP  
 從所指定的屬性清單卸除指定的屬性*list_name*。 卸除屬性會取消註冊屬性，所以它不再是可搜尋的。  
  
## <a name="remarks"></a>備註  
 每個全文檢索索引只能有一個搜尋屬性清單。  
  
 若要在指定的搜尋屬性上啟用查詢，您必須將它加入至全文檢索索引的搜尋屬性清單，然後再重新擴展索引。  
  
 當指定屬性時，您可以用括號括住的逗點分隔清單，依任何順序排列 PROPERTY_SET_GUID、PROPERTY_INT_ID 和 PROPERTY_DESCRIPTION 子句，例如：  
  
```  
ALTER SEARCH PROPERTY LIST CVitaProperties  
ADD 'System.Author'   
WITH (   
      PROPERTY_DESCRIPTION = 'Author or authors of a given document.',  
      PROPERTY_SET_GUID   = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9',   
      PROPERTY_INT_ID = 4   
      );  
```  
  
> [!NOTE]  
>  這個範例使用屬性名稱 `System.Author`，類似 Windows Vista 中導入的標準屬性名稱 (Windows 標準名稱) 的概念。  
  
## <a name="obtaining-property-values"></a>取得屬性值  
 全文檢索搜尋藉由使用屬性集 GUID 和屬性整數識別碼，將搜尋屬性對應至全文檢索索引。 如需如何取得 Microsoft 所定義的屬性資訊，請參閱[尋找屬性集 Guid 與屬性整數識別碼，搜尋屬性的](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)。 如需有關獨立軟體廠商 (ISV) 所定義之屬性的詳細資訊，請參閱該廠商的文件集。  
  
## <a name="making-added-properties-searchable"></a>讓加入的屬性成為可搜尋的  
 若將搜尋屬性加入至搜尋屬性清單，會註冊屬性。 新加入的屬性可以立即在指定[CONTAINS](../../t-sql/queries/contains-transact-sql.md)查詢。 但是，直到相關的全文檢索索引重新擴展之後，新加入之屬性的屬性範圍全文檢索查詢才會傳回文件。 例如，下列屬性範圍查詢新加入之屬性*table_name*，直到與目標資料表相關聯的全文檢索索引不會傳回任何文件 (*table_name*) 重新擴展之後：  
  
```  
SELECT column_name  
FROM table_name  
WHERE CONTAINS( PROPERTY( column_name, 'new_search_property' ), 
               'contains_search_condition');  
GO   
```  
  
 若要啟動完整母體擴展，請使用下列[ALTER FULLTEXT INDEX &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)陳述式：  
  
```  
USE database_name;  
GO  
ALTER FULLTEXT INDEX ON table_name START FULL POPULATION;  
GO  
```  
  
> [!NOTE]  
>  從屬性清單卸除屬性之後不需要重新母體擴展，因為只有留在搜尋屬性清單中的屬性可用於全文檢索查詢。  
  
## <a name="related-references"></a>相關的參考資料  
 **若要建立屬性清單**  
  
-   [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)  
  
 **若要卸除屬性清單**  
  
-   [DROP SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)  
  
 **若要新增或移除全文檢索索引的屬性清單**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **若要執行全文檢索索引母體擴展**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissions  
 需要屬性清單的 CONTROL 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-adding-a-property"></a>A. 加入屬性  
 下列範例會將數個屬性 `Title`、`Author` 和 `Tags` 加入至名為 `DocumentPropertyList` 的屬性清單。  
  
> [!NOTE]  
>  如需建立範例`DocumentPropertyList`屬性清單，請參閱[CREATE SEARCH PROPERTY LIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
   ADD 'Title'   
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 2,   
      PROPERTY_DESCRIPTION = 'System.Title - Title of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Author'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 4,   
      PROPERTY_DESCRIPTION = 'System.Author - Author or authors of the item.' );  
  
ALTER SEARCH PROPERTY LIST DocumentPropertyList   
    ADD 'Tags'  
   WITH ( PROPERTY_SET_GUID = 'F29F85E0-4FF9-1068-AB91-08002B27B3D9', PROPERTY_INT_ID = 5,   
      PROPERTY_DESCRIPTION = 
          'System.Keywords - Set of keywords (also known as tags) assigned to the item.' );  
```  
  
> [!NOTE]  
>  您必須將指定的搜尋屬性清單與全文檢索索引產生關聯，才能將它用於屬性範圍查詢。 若要這樣做，請使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)陳述式並指定 SET SEARCH PROPERTY LIST 子句。  
  
### <a name="b-dropping-a-property"></a>B. 卸除屬性  
 下列範例會從 `Comments` 屬性清單卸除 `DocumentPropertyList` 屬性。  
  
```  
ALTER SEARCH PROPERTY LIST DocumentPropertyList  
DROP 'Comments' ;  
```  
  
## <a name="see-also"></a>另請參閱  
 [建立搜尋屬性清單 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [DROP SEARCH PROPERTY LIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-search-property-list-transact-sql.md)   
 [sys.registered_search_properties &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [尋找搜尋屬性的屬性集 GUID 與屬性整數識別碼](../../relational-databases/search/find-property-set-guids-and-property-integer-ids-for-search-properties.md)  
  
  

