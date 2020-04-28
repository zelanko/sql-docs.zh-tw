---
title: sys.databases registered_search_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.registered_search_properties
- registered_search_properties
- sys.registered_search_properties_TSQL
- registered_search_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- search properties [SQL Server]
- property searching [SQL Server], viewing registered properties
- search property lists [SQL Server], viewing registered properties
- sys.registered_search_properties catalog view
ms.assetid: 1b9a7a5c-8c05-4819-83c3-7487dd08fcf7
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 055e64c743c453fb6362d45587b395bf6f3d77bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68067892"
---
# <a name="sysregistered_search_properties-transact-sql"></a>sys.registered_search_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對目前資料庫上任何搜尋屬性清單所包含的每個搜尋屬性包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|此屬性所屬搜尋屬性清單的識別碼。|  
|**property_set_guid**|**uniqueidentifier**|全域唯一識別碼 (GUID)，識別搜尋屬性所屬的屬性集。|  
|**property_int_id**|**int**|在屬性集內識別這個搜尋屬性的整數。 **property_int_id**在屬性集內是唯一的。|  
|**property_name**|**Nvarchar （64）**|搜尋屬性清單中唯一識別這個搜尋屬性的名稱。<br /><br /> 注意：若要搜尋屬性，請在[CONTAINS](../../t-sql/queries/contains-transact-sql.md)述詞中指定此屬性名稱。|  
|**property_description**|**nvarchar(512)**|屬性的描述。|  
|**property_id**|**int**|**Property_list_id**值所識別的搜尋屬性清單中，搜尋屬性的內部屬性識別碼。<br /><br /> 當給定的屬性加入至給定搜尋屬性清單時，全文檢索引擎會註冊屬性，並為它指派該屬性清單特有的內部屬性識別碼。 對於給定的搜尋屬性清單來說，內部屬性識別碼 (本身為整數) 是唯一的。 如果給定屬性已在多個搜尋屬性清單中註冊，可能會為每個搜尋屬性清單指定不同的內部屬性識別碼。<br /><br /> 注意：內部屬性識別碼與將屬性加入至搜尋屬性清單時所指定的屬性整數識別碼不同。 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。<br /><br /> 若要在全文檢索索引中，查看所有屬性相關內容： <br />                  [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)|  
  
## <a name="remarks"></a>備註  
 如需搜尋屬性清單的詳細資訊，請參閱[使用搜尋屬性清單搜尋文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="permissions"></a>權限  
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
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [fulltext_indexes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
