---
title: sys.all_sql_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_sql_modules_TSQL
- sys.all_sql_modules
- all_sql_modules
- sys.all_sql_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_sql_modules catalog view
ms.assetid: 7477a3fe-afb3-44c8-bb2c-c6e1d9bdee6f
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2b5b9f84f432a0861483066f3367556b5afc1f9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47684146"
---
# <a name="sysallsqlmodules-transact-sql"></a>sys.all_sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回的聯合**sys.sql_modules**並**sys.system_sql_modules**。  
  
 此檢視會傳回每個原生編譯的純量使用者定義函式的資料列。 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函數](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|包含物件的物件識別碼。 在資料庫中，這是唯一的。|  
|**定義**|**nvarchar(max)**|定義這個模組的 SQL 文字。<br /><br /> NULL = 已加密|  
|**uses_ansi_nulls**|**bit**|模組是以 SET ANSI_NULLS ON 加以建立。|  
|**uses_quoted_identifier**|**bit**|模組是以 SET QUOTED_IDENTIFIER ON 加以建立。|  
|**is_schema_bound**|**bit**|模組是以 SCHEMABINDING 選項加以建立。|  
|**uses_database_collation**|**bit**|1 = 結構描述繫結模組定義為了正確評估，必須依據資料庫的預設定序而定；否則為 0。 這種相依性可以防止變更資料庫的預設定序。|  
|**is_recompiled**|**bit**|程序是使用 WITH RECOMPILE 選項加以建立。|  
|**null_on_null_input**|**bit**|模組宣告的目的不是為了因應任何 NULL 輸入而產生 NULL 輸出。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 資料庫主體的識別碼。<br /><br /> 在預設或 EXECUTE AS CALLER 的情況下為 NULL。<br /><br /> 識別碼指定的主體如果 EXECUTE AS SELF 或 EXECUTE AS\<主體 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
|**uses_native_compilation**|bit|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 0 = 不是原生編譯<br /><br /> 1 = 是原生編譯<br /><br /> 預設值是 0。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.system_sql_modules &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-system-sql-modules-transact-sql.md)   
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
