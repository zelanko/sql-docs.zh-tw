---
title: "建立全文檢索停用字詞表 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STOPLIST_TSQL
- FULLTEXT STOPLIST
- STOPLIST
- FULLTEXT_STOPLIST_TSQL
- CREATE FULLTEXT STOPLIST
- CREATE_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- CREATE FULLTEXT STOPLIST statement
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 0669b1d0-46cc-4fac-8df7-5f7fa7af5db4
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c6877dccd56d4f90a5600b095b1294ec1ccd6eb3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-fulltext-stoplist-transact-sql"></a>CREATE FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  在目前資料庫中建立新的全文檢索停用字詞表。  
  
 停用字詞在資料庫中使用管理的物件稱為*停用字詞表*。 停用字詞表是停用字詞的清單，當它與全文檢索索引相關聯時，會套用至該索引上的全文檢索查詢。 如需詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
> [!IMPORTANT]  
>  只有在相容性層級 100 底下才支援 CREATE FULLTEXT STOPLIST、ALTER FULLTEXT STOPLIST 和 DROP FULLTEXT STOPLIST。 在相容性層級 80 和 90 底下，則不支援這些陳述式。 不過，在所有相容性層級底下，系統停用字詞表都會自動與新的全文檢索索引產生關聯。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
CREATE FULLTEXT STOPLIST stoplist_name  
[ FROM { [ database_name.]source_stoplist_name } | SYSTEM STOPLIST ]  
[ AUTHORIZATION owner_name ]  
;  
```  
  
## <a name="arguments"></a>引數  
 *s*  
 這是停用字詞表的名稱。 *s*最多可有 128 個字元。 *s*必須在目前資料庫中，所有停用字詞表之間是唯一的且符合識別碼的規則。  
  
 *s*將在建立全文檢索索引時使用。  
  
 *database_name*  
 停用字詞表其中所指定的資料庫名稱*source_stoplist_name*所在。 如果未指定， *database_name*預設為目前的資料庫。  
  
 *source_stoplist_name*  
 指定新的停用字詞表是藉由複製現有的停用字詞表所建立。 如果*source_stoplist_name*不存在，或資料庫使用者沒有正確的權限，CREATE FULLTEXT STOPLIST 失敗並發生錯誤。 如果來源停用字詞表中停用字詞內指定的任何語言未在目前資料庫中註冊，則 CREATE FULLTEXT STOPLIST 會成功，但是會傳回警告，而且不會加入對應的停用字詞。  
  
 SYSTEM STOPLIST  
 指定新的停用字詞表建立存在停用字詞表，預設會在[Resource 資料庫](../../relational-databases/databases/resource-database.md)。  
  
 授權*owner_name*  
 指定擁有停用字詞表的資料庫主體名稱。 *owner_name*必須是其中目前的使用者是成員，或目前使用者必須具有 IMPERSONATE 權限的主體名稱*owner_name*。 若未指定，擁有權便歸目前使用者。  
  
## <a name="remarks"></a>備註  
 停用字詞表的建立者就是它的擁有者。  
  
## <a name="permissions"></a>Permissions  
 建立 STOPLIST 需要 CREATE FULLTEXT CATALOG 權限。 停用字詞表擁有者可明確授與停用字詞表的 CONTROL 權限，好讓使用者可加入及移除字詞，以及卸除停用字詞表。  
  
> [!NOTE]  
>  搭配全文檢索索引使用停用字詞表需要 REFERENCE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-new-full-text-stoplist"></a>A. 建立新的全文檢索停用字詞表  
 下列範例會建立名為 `myStoplist` 的新全文檢索停用字詞表。  
  
```  
CREATE FULLTEXT STOPLIST myStoplist;  
GO  
```  
  
### <a name="b-copying-a-full-text-stoplist-from-an-existing-full-text-stoplist"></a>B. 從現有的全文檢索停用字詞表複製全文檢索停用字詞表  
 下列範例會藉由複製名為 `myStoplist2` 的現有 AdventureWorks 停用字詞表來建立名為 `Customers.otherStoplist` 的新全文檢索停用字詞表。  
  
```  
CREATE FULLTEXT STOPLIST myStoplist2 FROM AdventureWorks.otherStoplist;  
GO  
```  
  
### <a name="c-copying-a-full-text-stoplist-from-the-system-full-text-stoplist"></a>C. 從系統的全文檢索停用字詞表複製全文檢索停用字詞表  
 下列範例會藉由複製系統的停用字詞表來建立名為 `myStoplist3` 的新全文檢索停用字詞表。  
  
```  
CREATE FULLTEXT STOPLIST myStoplist3 FROM SYSTEM STOPLIST;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT STOPLIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [卸除全文檢索停用字詞表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [設定及管理全文檢索搜尋停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  

