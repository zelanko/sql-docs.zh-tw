---
title: "ALTER PARTITION SCHEME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER PARTITION SCHEME
- ALTER_PARTITION_SCHEME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ALTER PARTITION SCHEME statement
- partition schemes [SQL Server], modifying
- modifying partition schemes
- adding filegroups
- NEXT USED filegroups
ms.assetid: f01d6880-9800-4cfb-8d11-d4be21efc8ca
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 16b15945c8e6f56621516f16707d61be908e9972
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="alter-partition-scheme-transact-sql"></a>ALTER PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  將檔案群組加入至資料分割結構描述中，或是變更資料分割結構描述之 NEXT USED 檔案群組的目的地。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ALTER PARTITION SCHEME partition_scheme_name   
NEXT USED [ filegroup_name ] [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *partition_scheme_name*  
 這是要變更的資料分割結構描述名稱。  
  
 *filegroup_name*  
 指定要由資料分割結構描述標示為 NEXT USED 的檔案群組。 這表示檔案群組會接受新的資料分割所建立的使用[ALTER PARTITION FUNCTION](../../t-sql/statements/alter-partition-function-transact-sql.md)陳述式。  
  
 在資料分割結構描述中，只有一個檔案群組可以指定為 NEXT USED。 您可以指定不是空的檔案群組。 如果*filegroup_name*指定，而且目前沒有任何檔案群組標示為 NEXT USED， *filegroup_name*標示為 NEXT USED。 如果*filegroup_name*指定，且有 NEXT USED 屬性的檔案群組已經存在，從現有的檔案群組，以傳輸 NEXT USED 屬性*filegroup_name*。  
  
 如果*filegroup_name*未指定且有 NEXT USED 屬性的檔案群組已經存在，該檔案群組使中的沒有 NEXT USED 檔案群組將會遺失其 NEXT USED 狀態*partition_scheme_name*.  
  
 如果*filegroup_name*未指定，若有任何檔案群組標示為 NEXT USED，ALTER PARTITION SCHEME 傳回警告。  
  
## <a name="remarks"></a>備註  
 只要是 ALTER PARTITION SCHEME 影響所及的檔案群組都必須在線上。  
  
## <a name="permissions"></a>Permissions  
 您可以使用下列權限來執行 ALTER PARTITION SCHEME：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **系統管理員 (sysadmin)** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   建立資料分割結構描述之資料庫的 CONTROL 或 ALTER 權限。  
  
-   在建立資料分割結構描述的資料庫中，其伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
 下列範例假設資料分割結構描述 `MyRangePS1` 和檔案群組 `test5fg` 存在於目前資料庫中。  
  
```  
ALTER PARTITION SCHEME MyRangePS1  
NEXT USED test5fg;  
```  
  
 檔案群組 `test5fg` 會收到資料分割資料表或索引的其他資料分割，作為 ALTER PARTITION FUNCTION 陳述式的結果。  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [DROP PARTITION FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_schemes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
