---
title: DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 573f8036d1e28f18e89597ae4bd71b00796c66af
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/04/2018
ms.locfileid: "37786529"
---
# <a name="dbname-transact-sql"></a>DB_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

此函式會傳回指定資料庫的名稱。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DB_NAME ( [ database_id ] )  
```  
  
## <a name="arguments"></a>引數  
*database_id*  

`DB_NAME` 會傳回其名稱之資料庫的識別碼 (ID)。 如果 `DB_NAME` 呼叫省略 *database_id*，`DB_NAME` 會傳回目前資料庫的名稱。
  
## <a name="return-types"></a>傳回類型
**nvarchar(128)**
  
## <a name="permissions"></a>Permissions  

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
SELECT DB_NAME(3)AS [Database Name];  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
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
  
## <a name="see-also"></a>另請參閱
[DB_ID &#40;Transact-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)  
[中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)
  
  

