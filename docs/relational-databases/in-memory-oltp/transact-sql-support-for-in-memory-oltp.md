---
title: "記憶體內部 OLTP 的 Transact-SQL 支援 | Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cc975fbbdb4118158e4beacef63f45a63c479d38
ms.lasthandoff: 04/11/2017

---
# <a name="transact-sql-support-for-in-memory-oltp"></a>記憶體中 OLTP 的 Transact-SQL 支援
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式包含語法選項，可支援記憶體內部 OLTP：  
  
-   [ALTER DATABASE 檔案及檔案群組選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) (已加入 **MEMORY_OPTIMIZED_DATA**)  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md) (已加入 **MEMORY_OPTIMIZED_DATA**)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)  
  
-   [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
    在原生編譯的預存程序中，您可以將變數宣告為 **NOT NULL**。 您無法在一般的預存程序中進行。  
  
 從 SQL Server 2016 開始，**AUTO_UPDATE_STATISTICS** 可以是記憶體最佳化資料表的 **ON**。 如需詳細資訊，請參閱 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)。  
  
 原生編譯的預存程序不支援 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md) ON。  
  
 如需不支援功能的詳細資訊，請參閱[記憶體內部 OLTP 不支援 Transact-SQL 建構](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)。  
  
 如需原生編譯預存程序內和上方支援之建構的相關資訊，請參閱 [原生編譯 T-SQL 模組支援的功能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md) 和 [原生編譯 T-SQL 模組支援的 DDL](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [原生編譯預存程序的移轉問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [記憶體內部 OLTP 不支援的 SQL Server 功能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)   
 [原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)  
  
  
