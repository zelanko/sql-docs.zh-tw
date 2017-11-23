---
title: "卸除資料分割函數 (TRANSACT-SQL) |Microsoft 文件"
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
- DROP PARTITION FUNCTION
- DROP_PARTITION_FUNCTION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- deleting partition functions
- DROP PARTITION FUNCTION statement
- partition functions [SQL Server], removing
- dropping partition functions
- removing partition functions
ms.assetid: a4bb055a-a538-4db9-a6fb-550d1eabfa18
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7bd6d0d21ce398784c2baf047bef81282f59465e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-partition-function-transact-sql"></a>DROP PARTITION FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除資料分割函數。 資料分割函數是以 CREATE PARTITION FUNCTION 建立，並且以 ALTER PARTITION FUNCTION 修改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP PARTITION FUNCTION partition_function_name [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *partition_function_name*  
 這是要卸除的資料分割函數名稱。  
  
## <a name="remarks"></a>備註  
 只有在沒有目前使用資料分割函數的資料分割結構描述時，才可以卸除資料分割函數。 如果有使用資料分割函數的資料分割結構描述，DROP PARTITION FUNCTION 就會傳回錯誤。  
  
## <a name="permissions"></a>Permissions  
 下列任何一個權限，都可以用來執行 DROP PARTITION FUNCTION：  
  
-   ALTER ANY DATASPACE 權限。 這個權限預設會授與 **sysadmin** 固定伺服器角色以及 **db_owner** 和 **db_ddladmin** 固定資料庫角色的成員。  
  
-   對於建立資料分割函數之資料庫的 CONTROL 或 ALTER 權限。  
  
-   對於建立資料分割函數之資料庫伺服器的 CONTROL SERVER 或 ALTER ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
 下列範例假設目前資料庫中已建立了資料分割函數 `myRangePF`。  
  
```  
DROP PARTITION FUNCTION myRangePF;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-partition-function-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.partition_functions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-parameters-transact-sql.md)   
 [sys.partition_range_values &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)   
 [sys.partitions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
