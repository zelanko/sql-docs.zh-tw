---
title: sys.registered_search_property_lists (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36761417e5be68ef9da7c28464562ada75af088d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47617786"
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對目前資料庫上的每個搜尋屬性清單，各包含一個資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|屬性清單的識別碼。|  
|**name**|**sysname**|屬性清單的名稱。|  
|**create_date**|**datetime**|建立屬性清單的日期。|  
|**modify_date**|**datetime**|上次利用任何 ALTER 陳述式修改屬性清單的日期。|  
|**principal_id**|**int**|屬性清單的擁有者。|  
  
## <a name="remarks"></a>備註  
 如需詳細資訊，請參閱 [使用搜索屬性清單搜索文件屬性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="permissions"></a>Permissions  
 搜尋屬性清單內中繼資料的可見性受限於您所擁有，或您已獲得某些 REFERENCE 權限的那些搜尋屬性清單。  
  
> [!NOTE]  
>  搜尋屬性清單擁有者可以授與清單的 REFERENCE 或 CONTROL 權限。 具有 CONTROL 權限的使用者也可以將 REFERENCE 權限授與其他使用者。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫中搜尋屬性清單的識別碼和名稱。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
