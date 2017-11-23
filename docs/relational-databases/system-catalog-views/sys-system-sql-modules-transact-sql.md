---
title: "sys.system_sql_modules (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- system_sql_modules_TSQL
- sys.system_sql_modules
- sys.system_sql_modules_TSQL
- system_sql_modules
dev_langs: TSQL
helpviewer_keywords: sys.system_sql_modules catalog view
ms.assetid: ad3548bc-4780-4821-b962-b421d52daed9
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66917b2a30649119ee7921f4343d79765efbb8b1
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="syssystemsqlmodules-transact-sql"></a>sys.system_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對包含 SQL 語言定義模組的每個系統物件，各傳回一個資料列。 類型是 FN、IF、P、PC、TF、V 的系統物件具有關聯的 SQL 模組。 若要識別與包含物件，您可以加入此檢視來[sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含物件的物件識別碼，在資料庫中是唯一的。|  
|**定義**|**nvarchar(max)**|定義這個模組的 SQL 文字。|  
|**uses_ansi_nulls**|**bit**|1 = 模組是在 SET ANSI_NULLS 資料庫選項為 ON 的情況下加以建立。<br /><br /> 一定會傳回 1。|  
|**uses_quoted_identifier**|**bit**|1 = 模組是以 SET QUOTED_IDENTIFIER ON 加以建立。<br /><br /> 一定會傳回 1。|  
|**is_schema_bound**|**bit**|0 = 模組不是以 SCHEMABINDING 選項加以建立。<br /><br /> 永遠傳回 0。|  
|**uses_database_collation**|**bit**|0 = 模組不會相依於資料庫的預設定序。<br /><br /> 永遠傳回 0。|  
|**is_recompiled**|**bit**|0 = 程序不是使用 WITH RECOMPILE 選項加以建立。<br /><br /> 永遠傳回 0。|  
|**null_on_null_input**|**bit**|0 = 模組建立目的不是為了因應任何 NULL 輸入而產生 NULL 輸出。<br /><br /> 永遠傳回 0。|  
|**sys.sql_modules**|**int**|一律傳回 NULL|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.all_sql_modules &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
