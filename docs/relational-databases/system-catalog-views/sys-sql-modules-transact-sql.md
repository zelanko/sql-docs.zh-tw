---
title: sys.sql_modules (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 01/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 39c8e18600d075f4f5b7c1e39135291416cd025c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回一個資料列的是 SQL 語言定義模組中的每個物件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，包括原生編譯純量使用者定義函數。 類型 P、RF、V、TR、FN、IF、TF 和 R 的物件，各有一個相關聯的 SQL 模組。 獨立預設值，即類型 D 的物件，在這份檢視中也有 SQL 模組定義。 如需這些類型的說明，請參閱**類型**中的資料行[sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)目錄檢視。  
  
 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函數](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含物件的物件識別碼。 在資料庫中，這是唯一的。|  
|**定義**|**nvarchar(max)**|定義這個模組的 SQL 文字。 這個值也可以取得使用[OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)內建函式。<br /><br /> NULL = 已加密。|  
|**uses_ansi_nulls**|**bit**|模組是以 SET ANSI_NULLS ON 加以建立。<br /><br /> 如果是規則和預設值，則永遠 = 0。|  
|**uses_quoted_identifier**|**bit**|模組是以 SET QUOTED_IDENTIFIER ON 加以建立。|  
|**is_schema_bound**|**bit**|模組是以 SCHEMABINDING 選項加以建立。<br /><br /> 如果是原生編譯預存程序，一定包含 1 值。|  
|**uses_database_collation**|**bit**|1 = 結構描述繫結模組定義為了正確評估，必須依據資料庫的預設定序而定；否則為 0。 這種相依性可以防止資料庫的預設定序變更。|  
|**is_recompiled**|**bit**|程序是以 WITH RECOMPILE 選項加以建立。|  
|**null_on_null_input**|**bit**|模組宣告的目的不是為了因應任何 NULL 輸入而產生 NULL 輸出。|  
|**execute_as_principal_id**|**整數**|EXECUTE AS 資料庫主體的識別碼。<br /><br /> 在預設或 EXECUTE AS CALLER 的情況下為 NULL。<br /><br /> 指定主體 if 識別碼 EXECUTE AS SELF 或 EXECUTE AS\<主體 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**uses_native_compilation**|**bit**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。<br /><br /> 0 = 不是原生編譯<br /><br /> 1 = 是原生編譯<br /><br /> 預設值是 0。|  
  
## <a name="remarks"></a>備註  
 預設條件約束類型 D、 物件的 SQL 運算式中找到[sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md)目錄檢視。 檢查條件約束類型 C、 物件的 SQL 運算式中找到[sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)目錄檢視。  
  
 這項資訊也述[sys.dm_db_uncontained_entities &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
 下列範例會傳回目前資料庫中每個模組的名稱、類型和定義。  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查詢 SQL Server 系統目錄 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
