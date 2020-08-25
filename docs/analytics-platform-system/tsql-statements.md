---
title: T-SQL 陳述式
description: 分析平臺系統 (AP) SQL Server 平行處理資料倉儲 (PDW) 的 t-sql 語句。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 078c0364e64ddca8974544734e8e5a45950e14e0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778397"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>平行處理資料倉儲的 t-sql 語句
Transact-sql (T-sql) 語句，適用于分析平臺系統 (AP) SQL Server () 的平行資料倉儲。

## <a name="data-definition-language-ddl-statements"></a>資料定義語言 (DDL) 陳述式
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ALTER SCHEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREATE COLUMNSTORE INDEX](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREATE DATABASE](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016)
* [CREATE DATABASE SCOPED CREDENTIAL](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE FUNCTION](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CREATE SCHEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [DROP EXTERNAL DATA SOURCE](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [DROP EXTERNAL FILE FORMAT](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [DROP EXTERNAL TABLE](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP PROCEDURE](../t-sql/statements/drop-procedure-transact-sql.md)
* [DROP STATISTICS](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [DROP SCHEMA](../t-sql/statements/drop-schema-transact-sql.md)
* [DROP VIEW](../t-sql/statements/drop-view-transact-sql.md)
* [重 命名](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>資料操作語言 (DML) 陳述式
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>資料庫主控台命令
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](/previous-versions/sql/sql-server-2016/mt204018(v=sql.130))
* [DBCC SHRINKLOG](../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWEXECUTIONPLAN](../t-sql/database-console-commands/dbcc-pdw-showexecutionplan-transact-sql.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWPARTITIONSTATS](../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md?view=sql-server-ver15)

## <a name="query-statements"></a>查詢陳述式
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT 和 INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [EXPLAIN](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [使用 PIVOT 和 UNPIVOT](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [返回頁首](../t-sql/queries/top-transact-sql.md)
* [鋸齒化](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [搜尋條件](../t-sql/queries/search-condition-transact-sql.md)
* [子查詢](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>安全性陳述式
* 權限：[GRANT](../t-sql/statements/grant-transact-sql.md)、[DENY](../t-sql/statements/deny-transact-sql.md)、[REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [ALTER CERTIFICATE](../t-sql/statements/alter-certificate-transact-sql.md)
* [ALTER DATABASE ENCRYPTION KEY](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [ALTER MASTER KEY](../t-sql/statements/alter-master-key-transact-sql.md)
* [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)
* [ALTER USER](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
* [CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)
* [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)
* [CREATE USER](../t-sql/statements/create-user-transact-sql.md)
* [DROP CERTIFICATE](../t-sql/statements/drop-certificate-transact-sql.md)
* [DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [DROP LOGIN](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [DROP ROLE](../t-sql/statements/drop-role-transact-sql.md)
* [DROP USER](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>後續步驟
如需詳細的參考資訊，請參閱 [t-sql 語言元素](tsql-language-elements.md) 和 [t-sql 系統檢視](tsql-system-views.md)。

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
