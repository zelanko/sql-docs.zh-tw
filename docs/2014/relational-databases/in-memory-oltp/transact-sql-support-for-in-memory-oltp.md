---
title: 記憶體內部 OLTP 的 Transact-SQL 支援 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db4c6895fb499458c198008319302a25b8cd34b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63156221"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>記憶體中 OLTP 的 Transact-SQL 支援
  您可以使用任何 Transact-SQL 查詢或 DML 陳述式 (SELECT、INSERT、UPDATE 或 DELETE)、特定陳述式及 SQL 模組 (例如預存程序、資料表值函數、純量函數、觸發程序和檢視表) 來存取記憶體最佳化的資料表。 如需詳細資訊，請參閱[使用已解讀的 Transact-sql 存取記憶體優化資料表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)。  
  
 只參考記憶體最佳化資料表的預存程序，可以原生方式編譯為機器碼，且通常能夠為解譯的 (以磁碟為基礎的) 預存程序，帶來顯著的效能提升。 若要最佳化記憶體最佳化資料表的存取，請使用原生編譯的預存程序。 如需詳細資訊，請參閱原生[編譯的預存程式](natively-compiled-stored-procedures.md)。  
  
 建立與修改資料庫物件 (DDL 陳述式) 前，需修改下列陳述式：  
  
-   [ALTER Database File 和 Filegroup 選項 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) （請參閱`MEMORY_OPTIMIZED_DATA`）  
  
-   [建立資料庫 &#40;SQL Server transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql) （請參閱`MEMORY_OPTIMIZED_DATA`）  
  
-   [CREATE PROCEDURE &#40;transact-sql&#41;](/sql/t-sql/statements/create-procedure-transact-sql) `NATIVE_COMPILATION`（請參閱`SCHEMABINDING`、 `EXECUTE AS`、和） `BEGIN ATOMIC`  
  
-   [CREATE TABLE &#40;transact-sql&#41;](/sql/t-sql/statements/create-table-transact-sql) （請`MEMORY_OPTIMIZED`參閱、 `DURABILITY` `BUCKET_COUNT` `INDEX`、、和） `HASH`  
  
-   [CREATE TYPE &#40;transact-sql&#41;](/sql/t-sql/statements/create-type-transact-sql) `MEMORY_OPTIMIZED`（請參閱`BUCKET_COUNT`、 `INDEX`、和） `HASH`  
  
-   [DECLARE @local_variable &#40;transact-sql&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql) （請參閱） `NULL`  |  `NOT NULL`  
  
 記憶體最佳化資料表支援 `PRIMARY KEY` 和 `NOT NULL` 條件約束。 如需執行不受支援之條件約束的詳細資訊，請參閱[遷移 Check 和 Foreign Key 條件約束](../../database-engine/migrating-check-and-foreign-key-constraints.md)。  
  
 如需不支援功能的詳細資訊，請參閱[記憶體內部 OLTP 不支援 Transact-SQL 建構](transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [支援的資料類型](supported-data-types-for-in-memory-oltp.md)  
  
-   [使用解譯的 Transact-SQL 存取記憶體最佳化的資料表](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [記憶體內部 OLTP 的系統檢視表、預存程序、DMV 和等候類型](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部優化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [原生編譯預存程序的移轉問題](migration-issues-for-natively-compiled-stored-procedures.md)   
 [支援的 SQL Server 功能](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
