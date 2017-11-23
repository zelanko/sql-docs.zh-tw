---
title: "sys.registered_search_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs: TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
caps.latest.revision: "20"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a52fb947477e4a25cf5784ed4861071e21ba769c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysregisteredsearchproperties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫上任何搜尋屬性清單所包含的每個搜尋屬性包含一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|此屬性所屬搜尋屬性清單的識別碼。|  
|**property_set_guid**|**uniqueidentifier**|全域唯一識別碼 (GUID)，識別搜尋屬性所屬的屬性集。|  
|**property_int_id**|**int**|在屬性集內識別這個搜尋屬性的整數。 **property_int_id**屬性集內是唯一的。|  
|**property_name**|**nvarchar （64)**|搜尋屬性清單中唯一識別這個搜尋屬性的名稱。<br /><br /> 注意： 若要搜尋的屬性，這個屬性中指定名稱[CONTAINS](../../t-sql/queries/contains-transact-sql.md)述詞。|  
|**property_description**|**nvarchar(512)**|屬性的描述。|  
|**屬性識別碼**|**int**|內部屬性識別碼所識別的搜尋屬性清單內之搜尋屬性**property_list_id**值。<br /><br /> 當給定的屬性加入至給定搜尋屬性清單時，全文檢索引擎會註冊屬性，並為它指派該屬性清單特有的內部屬性識別碼。 對於給定的搜尋屬性清單來說，內部屬性識別碼 (本身為整數) 是唯一的。 如果給定屬性已在多個搜尋屬性清單中註冊，可能會為每個搜尋屬性清單指定不同的內部屬性識別碼。<br /><br /> 注意： 內部屬性識別碼是將屬性加入至搜尋屬性清單時指定的屬性整數識別碼不同。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。<br /><br /> 若要檢視全文檢索索引中的所有屬性相關的內容： <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>備註  
 如需有關搜尋屬性清單的詳細資訊，請參閱[使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="permissions"></a>Permissions  
 搜尋屬性中繼資料的可見性受限於您所擁有搜尋屬性清單中的那些屬性，或您已獲得某些 REFERENCE 權限的那些屬性。  
  
> [!NOTE]  
>  搜尋屬性清單擁有者可以授與清單的 REFERENCE 或 CONTROL 權限。 具有 CONTROL 權限的使用者也可以將 REFERENCE 權限授與其他使用者。  
  
## <a name="examples"></a>範例  
 下列範例會列出已註冊之搜尋屬性的所有中繼資料。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.registered_search_properties;   
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
