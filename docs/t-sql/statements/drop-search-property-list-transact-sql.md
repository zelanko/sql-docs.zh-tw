---
title: "DROP SEARCH PROPERTY LIST (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SEARCH_PROPERTY_LIST_TSQL
- DROP SEARCH PROPERTY LIST
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- DROP SEARCH PROPERTY LIST statement
- search property lists [SQL Server], dropping
- search property lists [SQL Server], deleting
ms.assetid: 7c7ce52a-6b77-4a1c-9abf-d5feb664bea8
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 970fd636239f6de212d667ef6ec22edfa182859c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-search-property-list-transact-sql"></a>DROP SEARCH PROPERTY LIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  如果搜尋屬性清單目前沒有與資料庫中的任何全文檢索索引相關聯，從目前資料庫中卸除屬性清單。  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP SEARCH PROPERTY LIST property_list_name  
;  
```  
  
## <a name="arguments"></a>引數  
 *property_list_name*  
 這是要卸除之搜尋屬性清單的名稱。 *property_list_name*是識別項。  
  
 若要檢視現有屬性清單的名稱，請使用[sys.registered_search_property_lists](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)目錄檢視，如下：  
  
```  
SELECT name FROM sys.registered_search_property_lists;  
```  
  
## <a name="remarks"></a>備註  
 當搜尋屬性清單與任何全文檢索索引相關聯時，您無法從資料庫中卸除該清單，嘗試這樣做會失敗。 從指定的全文檢索索引中卸除搜尋屬性清單，請使用[ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md)陳述式，並指定 SET SEARCH PROPERTY LIST 子句以 OFF 或另一個名稱搜尋屬性清單。  
  
 **若要檢視屬性列出的伺服器執行個體**  
  
-   [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
 **若要檢視的屬性清單與全文檢索索引產生關聯**  
  
-   [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
 **若要移除全文檢索索引的屬性清單**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
##  <a name="Permissions"></a> Permissions  
 需要搜尋屬性清單的 CONTROL 權限。  
  
> [!NOTE]  
>  屬性清單擁有者可以授與此清單的 CONTROL 權限。 根據預設，建立搜尋屬性清單的使用者就是它的擁有者。 來變更擁有者，請使用[ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式。  
  
## <a name="examples"></a>範例  
 下列範例會從 `JobCandidateProperties` 資料庫卸除 `AdventureWorks2012` 屬性清單。  
  
```  
DROP SEARCH PROPERTY LIST JobCandidateProperties;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER SEARCH PROPERTY LIST &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-search-property-list-transact-sql.md)   
 [建立搜尋屬性清單 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_properties &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)  
  
  

