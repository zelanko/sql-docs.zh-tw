---
title: "卸除資料分割結構描述 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP PARTITION SCHEME
- DROP_PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP PARTITION SCHEME statement
- deleting partition schemes
- dropping partition schemes
- removing partition schemes
- partition schemes [SQL Server], removing
ms.assetid: 6efbc87c-1c92-4e43-96a7-e0f30f1db185
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c410a37aca0ad2b7c8ca662f76d9af8d9fc6d75a
ms.sourcegitcommit: 50e54dda407f362262b86941f68b7d80516db7fb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/06/2017
---
# <a name="drop-partition-scheme-transact-sql"></a>DROP PARTITION SCHEME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除資料分割結構描述。 使用建立分割區配置[CREATE PARTITION SCHEME](../../t-sql/statements/create-partition-scheme-transact-sql.md)使用和修改[ALTER PARTITION SCHEME](../../t-sql/statements/alter-partition-scheme-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP PARTITION SCHEME partition_scheme_name [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *partition_scheme_name*  
 這是您要卸除的資料分割結構描述名稱。  
  
## <a name="remarks"></a>備註  
 只有在目前沒有資料表或索引在使用資料分割結構描述時，才可以卸除資料分割結構描述。 如果有資料表或索引在使用資料分割結構描述，DROP PARTITION SCHEME 便會傳回錯誤。 DROP PARTITION SCHEME 不會移除檔案群組本身。  
  
## <a name="permissions"></a>Permissions  
 下列權限可用來執行 DROP PARTITION SCHEME：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **系統管理員 (sysadmin)** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   建立資料分割結構描述之資料庫的 CONTROL 或 ALTER 權限。  
  
-   在建立資料分割結構描述的資料庫中，其伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從目前資料庫中，卸除資料分割結構描述 `myRangePS1`：  
  
```  
DROP PARTITION SCHEME myRangePS1;  
```  
  
## <a name="see-also"></a>請參閱  
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [ALTER PARTITION SCHEME &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [sys.partition_schemes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
