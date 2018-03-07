---
title: "SET ANSI_NULL_DFLT_ON (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- ANSI_NULL_DFLT_ON
- ANSI_NULL_DFLT_ON_TSQL
- SET ANSI_NULL_DFLT_ON
- SET_ANSI_NULL_DFLT_ON_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET ANSI_NULL_DFLT_ON statement
- ANSI_NULL_DFLT_ON option
- default nullability
- null values [SQL Server], overriding
- overriding default nullability
ms.assetid: 8c925924-a466-4c8b-aeb2-7e0d341f32db
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 82532accfe14729a0e3ccbfa7bd3f1b55d2aaa01
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="set-ansinulldflton-transact-sql"></a>SET ANSI_NULL_DFLT_ON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  修改要覆寫新資料行的預設 null 屬性的工作階段的行為時**ANSI null default**選項是資料庫**false**。 如需有關設定的值**ANSI null default**，請參閱[ALTER DATABASE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>語法

```
-- Syntax for SQL Server and Azure SQL Database

SET ANSI_NULL_DFLT_ON {ON | OFF}
```

```
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse

SET ANSI_NULL_DFLT_ON ON
```

## <a name="remarks"></a>備註  
 這項設定只在 CREATE TABLE 和 ALTER TABLE 陳述式未指定新資料行的 Null 屬性時，才會影響新資料行的 Null 屬性設定。 當 SET ANSI_NULL_DFLT_ON 是 ON 時，如果未明確指定資料行的 Null 屬性狀態，ALTER TABLE 和 CREATE TABLE 陳述式所建立的新資料行會接受 Null 值。 SET ANSI_NULL_DFLT_ON 不會影響利用明確的 NULL 或 NOT NULL 來建立的資料行。  
  
 SET ANSI_NULL_DFLT_OFF 和 SET ANSI_NULL_DFLT_ON 不能同時設為 ON。 如果一個選項設為 ON，另一個選項便設為 OFF。 因此，您可以將 ANSI_NULL_DFLT_OFF 或 ANSI_NULL_DFLT_ON 設為 ON，也可以同時將它們設為 OFF。 如果任何一個選項是 ON，這項設定 (SET ANSI_NULL_DFLT_OFF 或 SET ANSI_NULL_DFLT_ON) 就會生效。 如果這兩個選項都設為 OFF，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會使用值**is_ansi_null_default_on**中的資料行[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)目錄檢視。  
  
 如果希望在資料庫中搭配不同 Null 屬性設定來使用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼作業比較可靠，最好是在 CREATE TABLE 和 ALTER TABLE 陳述式中指定 NULL 或 NOT NULL。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB Provider for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]都會將 ANSI_NULL_DFLT_ON 設為 ON 時連接。 起始於 DB-Library 應用程式的連接之 SET ANSI_NULL_DFLT_ON 預設值是 OFF。  
  
 當 SET ANSI_DEFAULTS 是 ON 時，會啟用 SET ANSI_NULL_DFLT_ON。  
  
 SET ANSI_NULL_DFLT_ON 的設定是在執行階段進行設定，而不是在剖析階段進行設定。  
  
 使用 SELECT INTO 陳述式建立資料表時，不會套用 SET ANSI_NULL_DFLT_ON 的設定。  
  
 若要檢視此設定的目前設定，請執行下列查詢。  
  
```  
DECLARE @ANSI_NULL_DFLT_ON VARCHAR(3) = 'OFF';  
IF ( (1024 & @@OPTIONS) = 1024 ) SET @ANSI_NULL_DFLT_ON = 'ON';  
SELECT @ANSI_NULL_DFLT_ON AS ANSI_NULL_DFLT_ON;  
  
```  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例顯示的效果`SET ANSI_NULL_DFLT_ON`這兩個設定**ANSI null default**資料庫選項。  
  
```  
USE AdventureWorks2012;  
GO  
  
-- The code from this point on demonstrates that SET ANSI_NULL_DFLT_ON  
-- has an effect when the 'ANSI null default' for the database is false.  
-- Set the 'ANSI null default' database option to false by executing  
-- ALTER DATABASE.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT OFF;  
GO  
-- Create table t1.  
CREATE TABLE t1 (a TINYINT) ;  
GO   
-- NULL INSERT should fail.  
INSERT INTO t1 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to ON and create table t2.  
SET ANSI_NULL_DFLT_ON ON;  
GO  
CREATE TABLE t2 (a TINYINT);  
GO   
-- NULL insert should succeed.  
INSERT INTO t2 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to OFF and create table t3.  
SET ANSI_NULL_DFLT_ON OFF;  
GO  
CREATE TABLE t3 (a TINYINT);  
GO  
-- NULL insert should fail.  
INSERT INTO t3 (a) VALUES (NULL);  
GO  
  
-- The code from this point on demonstrates that SET ANSI_NULL_DFLT_ON   
-- has no effect when the 'ANSI null default' for the database is true.  
-- Set the 'ANSI null default' database option to true.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON  
GO  
  
-- Create table t4.  
CREATE TABLE t4 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t4 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to ON and create table t5.  
SET ANSI_NULL_DFLT_ON ON;  
GO  
CREATE TABLE t5 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t5 (a) VALUES (NULL);  
GO  
  
-- SET ANSI_NULL_DFLT_ON to OFF and create table t6.  
SET ANSI_NULL_DFLT_ON OFF;  
GO  
CREATE TABLE t6 (a TINYINT);  
GO   
-- NULL INSERT should succeed.  
INSERT INTO t6 (a) VALUES (NULL);  
GO  
  
-- Set the 'ANSI null default' database option to false.  
ALTER DATABASE AdventureWorks2012 SET ANSI_NULL_DEFAULT ON;  
GO  
  
-- Drop tables t1 through t6.  
DROP TABLE t1,t2,t3,t4,t5,t6;  
```  
  
## <a name="see-also"></a>請參閱  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [SET 陳述式 &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ANSI_DEFAULTS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-defaults-transact-sql.md)   
 [SET ANSI_NULL_DFLT_OFF &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-ansi-null-dflt-off-transact-sql.md)  
  
  
