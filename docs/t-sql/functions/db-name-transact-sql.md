---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1c2a2e92fdef5cae1b2404d18c2c5fb18b3de1ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
這是所要傳回的資料庫識別碼 (ID)。 *database_id* 為沒有預設值的 **int**。 如果未指定任何識別碼，則傳回目前資料庫的名稱。
  
## <a name="return-types"></a>傳回類型
**nvarchar(128)**
  
## <a name="permissions"></a>Permissions  
如果 **DB_NAME** 的呼叫者不是資料庫的擁有者，而且該資料庫不是 **master** 或 **tempdb**，那麼要查看對應資料列所需具備的最低權限，就是 ALTER ANY DATABASE 或 VIEW ANY DATABASE 伺服器層級權限，或是 **master** 資料庫中的 CREATE DATABASE 權限。 呼叫端所連接的資料庫，永遠可以在 **sys.databases**中進行檢視。
  
> [!IMPORTANT]  
>  根據預設，公用角色具備 VIEW ANY DATABASE 權限，允許所有登入查看資料庫資訊。 若要封鎖登入，使其不具備偵測資料庫的能力，請撤銷公用的 VIEW ANY DATABASE 權限，或拒絕個別登入的 VIEW ANY DATABASE 權限。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 傳回目前資料庫的名稱  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. 使用資料庫識別碼傳回資料庫的名稱  
下列範例會傳回每個資料庫的資料庫名稱及 database_id。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>另請參閱
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

