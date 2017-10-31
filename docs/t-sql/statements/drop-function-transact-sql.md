---
title: "卸除函式 (TRANSACT-SQL) |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b85cb68749cdcf88d62d9d8fbf136a37e845519
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-_md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  從目前資料庫移除一或多個使用者自訂函數。 使用者定義函式會建立使用[CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)使用和修改[ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md)。  
  
 卸除函式支援原生編譯純量使用者定義函數。 如需詳細資訊，請參閱[記憶體內部 OLTP 的純量使用者定義函式](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>引數  
 *如果存在*    
 只有當它已經存在有條件地卸除函式。 從[!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)]2016年和[!INCLUDE[sssds_md](../../includes/sssds_md.md)]。
  
 *schema_name*  
 這是使用者定義函數所屬的結構描述名稱。  
  
 *function_name*  
 這是要移除的使用者自訂函數名稱。 您可以選擇性地指定結構描述名稱。 不能指定伺服器名稱和資料庫名稱。  
  
## <a name="remarks"></a>備註  
 如果資料庫中有 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數或檢視參考這個函數，並且是利用 SCHEMABINDING 加以建立；或者如果有計算資料行、CHECK 條件約束或 DEFAULT 條件約束參考這個函數，DROP FUNCTION 就不會成功。  
  
 如果有計算資料行參考這個函數，而且已經產生索引，DROP FUNCTION 就不會成功。  
  
## <a name="permissions"></a>Permissions  
 若要執行 DROP FUNCTION，使用者至少必須對該函數所屬的結構描述具備 ALTER 權限，或是對該函數具備 CONTROL 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-a-function"></a>A. 卸除函數  
 下列範例會卸除`fn_SalesByStore`使用者定義函數從`Sales`結構描述中的[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]範例資料庫。 若要建立此函式，請參閱範例 B 中[CREATE FUNCTION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  

