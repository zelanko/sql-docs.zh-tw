---
title: sys.sql_dependencies (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sql_dependencies
- sql_dependencies_TSQL
- sys.sql_dependencies_TSQL
- sys.sql_dependencies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_dependencies catalog view
ms.assetid: 1779aa87-a0b8-470a-a286-d7cc0b93ad2e
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cffa4e26da3de6d1e1f4d6de3bb63ca3bb94a9d0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="syssqldependencies-transact-sql"></a>sys.sql_dependencies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  依照定義某些其他參考物件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 運算式或陳述式所參考，針對受參考之實體的每個相依性，各包含一個資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)改為。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|識別受參考實體的類別：<br /><br /> 0 = 物件或資料行 (只限於非結構描述繫結參考)<br /><br /> 1 = 物件或資料行 (結構描述繫結參考)<br /><br /> 2 = 類型 (結構描述繫結參考)<br /><br /> 3 = XML 結構描述集合 (結構描述繫結參考)<br /><br /> 4 = 資料分割函數 (結構描述繫結參考)|  
|**class_desc**|**nvarchar(60)**|受參考實體之類別的描述：<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_NON_SCHEMA_BOUND**<br /><br /> **OBJECT_OR_COLUMN_REFERENCE_SCHEMA_BOUND**<br /><br /> **TYPE_REFERENCE**<br /><br /> **XML_SCHEMA_COLLECTION_REFERENCE**<br /><br /> **PARTITION_FUNCTION_REFERENCE**|  
|**object_id**|**int**|參考物件的識別碼。|  
|**column_id**|**int**|如果參考識別碼是資料行，便是參考資料行的識別碼，否則為 0。|  
|**referenced_major_id**|**int**|受參考實體的識別碼，由類別值來解譯，依據如下：<br /><br /> 0、1 = 物件或資料行的物件識別碼。<br /><br /> 2 = 類型識別碼。<br /><br /> 3 = XML 結構描述集合識別碼。|  
|**referenced_minor_id**|**int**|受參考實體的次要識別碼，由類別值來解譯，顯示如下。<br /><br /> 當類別 =：<br /><br /> 0， **referenced_minor_id**是資料行識別碼; 或如果不是資料行，則是 0。<br /><br /> 1， **referenced_minor_id**是資料行識別碼; 或如果不是資料行，則是 0。<br /><br /> 否則， **referenced_minor_id** = 0。|  
|**is_selected**|**bit**|選取物件或資料行。|  
|**is_updated**|**bit**|更新物件或資料行。|  
|**is_select_all**|**bit**|在 SELECT * 子句中使用物件 (只限物件層級)。|  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄常見問題集](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
