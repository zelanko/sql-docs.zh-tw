---
title: sys.dm_db_uncontained_entities (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_uncontained_entities
- dm_db_uncontained_entities_TSQL
- sys.dm_db_uncontained_entities_TSQL
- dm_db_uncontained_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_uncontained_entities dynamic management view
ms.assetid: f417efd4-8c71-4f81-bc9c-af13bb4b88ad
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 21a11895ad0d618f9466572edc213aa0d217d8ef
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/10/2018
---
# <a name="sysdmdbuncontainedentities-transact-sql"></a>sys.dm_db_uncontained_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  顯示資料庫中使用的任何未自主物件。 未自主物件為跨越自主資料庫中之資料庫界限的物件。 這個檢視可從自主資料庫以及非自主資料庫存取。 Sys.dm_db_uncontained_entities 是空的如果您的資料庫不使用任何未自主的實體。  
  
 如果模組多次跨越資料庫界限，只會回報其第一次已發現的跨越。  
  
||||  
|-|-|-|  
|**資料行名稱**|**型別**|**說明**|  
|*class*|**int**|1 = 物件或資料行 (包含模組、XPs、檢視、同義字及資料表)。<br /><br /> 4 = 資料庫主體<br /><br /> 5 = 組件<br /><br /> 6 = 類型<br /><br /> 7 = 索引 (全文檢索索引)<br /><br /> 12 = 資料庫 DDL 觸發程序<br /><br /> 19 = 路由<br /><br /> 30 = 稽核規格|  
|*class_desc*|**nvarchar(120)**|實體類別的描述。 下列其中一種以符合類別：<br /><br /> **OBJECT_OR_COLUMN**<br /><br /> **DATABASE_PRINCIPAL**<br /><br /> **ASSEMBLY**<br /><br /> **TYPE**<br /><br /> **INDEX**<br /><br /> **DATABASE_DDL_TRIGGER**<br /><br /> **ROUTE**<br /><br /> **AUDIT_SPECIFICATION**|  
|*major_id*|**int**|實體的識別碼。<br /><br /> 如果*類別*= 1，則 object_id<br /><br /> 如果*類別*= 4，則 sys.database_principals.principal_id。<br /><br /> 如果*類別*= 5，則 sys.assemblies.assembly_id。<br /><br /> 如果*類別*= 6，則 sys.types.user_type_id。<br /><br /> 如果*類別*= 7，則 sys.indexes.index_id。<br /><br /> 如果*類別*= 12，則 sys.triggers.object_id。<br /><br /> 如果*類別*= 19，則為 sys.routes.route_id。<br /><br /> 如果*類別*= 30，則 sys。 database_audit_specifications.databse_specification_id.|  
|*statement_line_number*|**int**|如果類別為模組，將會傳回非內含使用所在的行號。  否則，此值為 Null。|  
|*statement_ offset_begin*|**int**|如果類別為模組，會指出非內含使用的起始位置 (以位元組為單位，從 0 開始)。 否則傳回值為 Null。|  
|*statement_ offset_end*|**int**|如果類別為模組，會指出非內含使用的結束位置 (以位元組為單位，從 0 開始)。 值 -1 代表模組的結尾。 否則傳回值為 Null。|  
|*statement_type*|**nvarchar(512)**|陳述式的類型。|  
|*feature_ 名稱*|**nvarchar(256)**|傳回物件的外部名稱。|  
|*feature_type_name*|**nvarchar(256)**|傳回功能類型。|  
  
## <a name="remarks"></a>備註  
 sys.dm_db_uncontained_entities 顯示可能可以跨越資料庫界限的實體。 它將傳回可能使用資料庫外之物件的任何使用者實體。  
  
 下列功能類型將會回報。  
  
-   未知的內含項目行為 (動態 SQL 或延遲的名稱解析)  
  
-   DBCC (命令)  
  
-   系統預存程序  
  
-   系統純量函數  
  
-   系統資料表值函式  
  
-   內建系統函數  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Permissions  
 sys.dm_db_uncontained_entities 只會傳回使用者具有某些權限類型的物件。 若要完整評估的資料庫的高特殊權限的使用者，例如成員應該使用這個函式的內含項目**sysadmin**固定的伺服器角色或**db_owner**角色。  
  
## <a name="examples"></a>範例  
 下列範例會建立一個名為 P1 的程序，然後查詢 `sys.dm_db_uncontained_entities`。 查詢會回報 P1 使用位於資料庫外部的 **sys.endpoints** 。  
  
```sql  
CREATE DATABASE Test;  
GO  
  
USE Test;  
GO  
CREATE PROC P1  
AS   
SELECT * FROM sys.endpoints ;  
GO  
SELECT SO.name, UE.* FROM sys.dm_db_uncontained_entities AS UE  
LEFT JOIN sys.objects AS SO  
    ON UE.major_id = SO.object_id;  
```  
  
## <a name="see-also"></a>另請參閱  
 [自主資料庫](../../relational-databases/databases/contained-databases.md)  
  
  
