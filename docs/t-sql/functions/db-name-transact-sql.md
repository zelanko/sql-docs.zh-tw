---
description: DB_NAME (Transact-SQL)
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67cec38e835bd12cb951bba6ee790d0815c9cd29
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96116868"
---
# <a name="db_name-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

此函式會傳回指定資料庫的名稱。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```syntaxsql
DB_NAME ( [ database_id ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
*database_id*  

`DB_NAME` 會傳回其名稱之資料庫的識別碼 (ID)。 如果 `DB_NAME` 呼叫省略 *database_id*，`DB_NAME` 會傳回目前資料庫的名稱。
  
## <a name="return-types"></a>傳回類型
**nvarchar(128)**
  
## <a name="permissions"></a>權限  

如果 `DB_NAME` 的呼叫端未擁有特定非 **master** 或非 **tempdb** 資料庫，至少需要 `ALTER ANY DATABASE` 或 `VIEW ANY DATABASE` 伺服器層級權限才能查看對應的 `DB_ID` 資料列。 針對 **master** 資料庫，`DB_ID` 至少需要 `CREATE DATABASE` 權限。 呼叫端所連線的資料庫一律會出現在 **sys.databases** 中。
  
> [!IMPORTANT]  
>  根據預設，公用角色具備 `VIEW ANY DATABASE` 權限，允許所有登入查看資料庫資訊。 若要防止登入偵測資料庫，請 `REVOKE` 公用 `VIEW ANY DATABASE` 權限，或 `DENY` 個別登入的 `VIEW ANY DATABASE` 權限。
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-current-database-name"></a>A. 傳回目前資料庫名稱  
此範例會傳回目前資料庫的名稱。
  
```sql
SELECT DB_NAME() AS [Current Database];  
GO  
```  
  
### <a name="b-returning-the-database-name-of-a-specified-database-id"></a>B. 傳回指定資料庫識別碼的資料庫名稱  
此範例會傳回資料庫識別碼 `3` 的資料庫名稱。
  
```sql
USE master;  
GO  
SELECT DB_NAME(3) AS [Database Name];  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-return-the-current-database-name"></a>C. 傳回目前資料庫的名稱  
  
```sql
SELECT DB_NAME() AS [Current Database];  
```  
  
### <a name="d-return-the-name-of-a-database-by-using-the-database-id"></a>D. 使用資料庫識別碼傳回資料庫的名稱  
此範例會傳回每個資料庫的資料庫名稱及 database_id。
  
```sql
SELECT DB_NAME(database_id) AS [Database], database_id  
FROM sys.databases;  
```  
  
## <a name="see-also"></a>請參閱
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

