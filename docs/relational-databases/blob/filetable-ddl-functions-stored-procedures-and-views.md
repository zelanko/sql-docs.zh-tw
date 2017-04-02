---
title: "FileTable DDL、函數、預存程序及檢視 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-blob"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FileTables [SQL Server], 資料庫物件"
ms.assetid: 7e2e0f7f-94a8-4178-8bc7-d2e14ac8528c
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# FileTable DDL、函數、預存程序及檢視
  列出已加入或變更以支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中 FileTable 功能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫物件。  
  
 下表中的 [狀態] 資料行會指出項目為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]中的新項目，或是存在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，但已在 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中變更，可支援語意搜尋。  
  
 如需支援 FILESTREAM 的陳述式和資料庫物件清單，請參閱＜ [FILESTREAM DDL, Functions, Stored Procedures, and Views](../../relational-databases/blob/filestream-ddl-functions-stored-procedures-and-views.md)＞。  
  
##  <a name="ddl"></a> Transact-SQL 資料定義語言 (DDL) 陳述式  
  
|物件|狀態|其他資訊|  
|------------|------------|----------------------|  
|[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)<br /><br /> [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)|已變更|[啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|已變更|[建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)|已變更|[啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)|已變更|[建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)|  
|[RESTORE &#40;Transact-SQL&#41;](../Topic/RESTORE%20\(Transact-SQL\).md)<br /><br /> [RESTORE 引數 &#40;Transact-SQL&#41;](../Topic/RESTORE%20Arguments%20\(Transact-SQL\).md)|已變更||  
  
##  <a name="func"></a> 函數  
  
|物件|狀態|其他資訊|  
|------------|------------|----------------------|  
|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|**已加入**|[使用 FileTables 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|**已加入**|[使用 FileTables 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|**已加入**|[使用 FileTables 中的目錄與路徑](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)|  
  
##  <a name="sproc"></a> 預存程序  
  
|物件|狀態|其他資訊|  
|------------|------------|----------------------|  
|[sp_kill_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../Topic/sp_kill_filestream_non_transacted_handles%20\(Transact-SQL\).md)|**已加入**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="cv"></a> 目錄檢視  
  
|物件|狀態|其他資訊|  
|------------|------------|----------------------|  
|[sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)|**已加入**|[啟用 FileTable 的必要條件](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)|  
|[sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)|**已加入**|[建立、改變及卸除 FileTable](../../relational-databases/blob/create-alter-and-drop-filetables.md)<br /><br /> [管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)|**已加入**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
|[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)|已變更|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
##  <a name="dmv"></a> 動態管理檢視  
  
|物件|狀態|其他資訊|  
|------------|------------|----------------------|  
|[sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)|**已加入**|[管理 FileTable](../../relational-databases/blob/manage-filetables.md)|  
  
## 另請參閱  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  