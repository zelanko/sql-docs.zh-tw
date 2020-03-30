---
title: FILESTREAM、函數、預存程序、檢視 | Microsoft Docs
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 9ecb49ee-f64e-4d30-a803-e4064a21950a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3bc559bce60b4b179cd6e5a69846e1caa9b4668b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "75257958"
---
# <a name="filestream-functions-stored-procedures-and-views"></a>FILESTREAM、函數、預存程序和檢視
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  列出支援 FILESTREAM 的 Transact-SQL 陳述式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件。  
  
 如需支援 FileTable 功能的資料庫物件清單，請參閱＜ [FileTable DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)＞。  
  
##  <a name="transact-sql-data-definition-language-ddl-statements"></a><a name="ddl"></a> Transact-SQL 資料定義語言 (DDL) 陳述式  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)
  
##  <a name="system-functions"></a><a name="func"></a> 系統函數  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/get-filestream-transaction-context-transact-sql.md)  
  
-   [PathName &#40;Transact-SQL&#41;](../../relational-databases/system-functions/pathname-transact-sql.md)  
  
##  <a name="system-stored-procedures"></a><a name="proc"></a> 系統預存程序  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
-   [sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md)  
  
##  <a name="system-views---catalog-views"></a><a name="cat"></a> 系統檢視表 - 目錄檢視  
  
-   [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
  
##  <a name="system-views---dynamic-management-views"></a><a name="dmv"></a> 系統檢視表 - 動態管理檢視  
  
-   [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
  
-   [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
  
##  <a name="programming-apis"></a><a name="api"></a> 程式設計 API  
  
-   [使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
-   [Managed API - SqlFileStream 類別](https://go.microsoft.com/fwlink/?LinkId=220875)  
  
  
