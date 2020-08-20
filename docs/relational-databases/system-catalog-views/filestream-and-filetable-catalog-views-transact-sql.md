---
description: Filestream 和 FileTable 目錄檢視 (Transact-SQL)
title: Filestream 和 FileTable 目錄檢視 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c50e3042b82540e17ec6be721d84ba9cfe469c87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482236"
---
# <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 和 FileTable 目錄檢視 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  本節描述與 FileTable 功能相關的目錄檢視。  
  
## <a name="filestream-and-filetable-catalog-views-transact-sql"></a>Filestream 和 filetable 目錄檢視 (Transact-sql) 
 [sys.database_filestream_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-filestream-options-transact-sql.md)  
 顯示 FileTable 中已啟用的非交易式 FILESTREAM 資料存取層級的相關資訊。 針對 SQL Server 執行個體中的每個資料庫，各包含一個資料列。  
  
 [sys.filetable_system_defined_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql.md)  
 顯示與 FileTable 相關的系統定義物件清單。 針對每個系統定義物件，各包含一個資料列。  
  
 [sys.filetables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filetables-transact-sql.md)  
 針對每個 FileTable，各傳回一個資料列。 從 **sys. 資料表**繼承。  

## <a name="see-also"></a>另請參閱
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream 及 FileTable 動態管理檢視 (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream 和 FileTable 系統預存程序 (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
  
