---
title: "DB_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DB_NAME
- DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database names [SQL Server], DB_NAME
- names [SQL Server], databases
- viewing database names
- displaying database names
- DB_NAME function
ms.assetid: e21fb33a-a3ea-49b0-bb6b-8f789a675a0e
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c5743ccb1374640078a77d84a140e9e5d0fdaef0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回資料庫名稱。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>引數  
*database_id*  
這是所要傳回的資料庫識別碼 (ID)。 *database_id*是**int**，沒有預設值。 如果未指定任何識別碼，則傳回目前資料庫的名稱。
  
## <a name="return-types"></a>傳回型別
**nvarchar （128)**
  
## <a name="permissions"></a>Permissions  
如果呼叫端的**DB_NAME**不是資料庫的擁有者和資料庫不是**主要**或**tempdb**，若要查看對應的資料列所需的最小權限ALTER ANY DATABASE 或 VIEW ANY DATABASE 伺服器層級權限或在 CREATE DATABASE 權限**主要**資料庫。 呼叫端所連接的資料庫，永遠可以在 **sys.databases**中進行檢視。
  
> [!IMPORTANT]  
>  根據預設，公用角色都有 VIEW ANY DATABASE 權限，讓所有的登入，以查看資料庫資訊。 若要封鎖來自能夠偵測資料庫的登入，撤銷 VIEW ANY DATABASE 權限從公用，或拒絕個別登入的 VIEW ANY DATABASE 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-current-database-name"></a>A. 傳回目前資料庫名稱  
下列範例會傳回目前資料庫的名稱。
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 傳回指定資料庫識別碼的資料庫名稱  
下列範例會傳回資料庫識別碼 `3` 的資料庫名稱。
  
```sql
USE master;  
GO  
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 傳回目前的資料庫名稱  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. 傳回資料庫的名稱使用的資料庫識別碼  
下列範例會傳回 database_id 每個資料庫與資料庫名稱。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>另請參閱
[DB_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/db-id-transact-sql.md)  
[中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  


