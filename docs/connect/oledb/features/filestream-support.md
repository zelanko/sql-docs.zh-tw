---
title: FILESTREAM 支援 |Microsoft 文件
description: SQL Server 的 OLE DB 驅動程式中的 FILESTREAM 支援
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eb5c5abb611223d31af9832c512a418b18ac78a9
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="filestream-support"></a>FILESTREAM 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

FILESTREAM 提供透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或直接存取 Windows 檔案系統來儲存及存取大型二進位值的方式。 大型二進位值是大於 2 GB 的值。 如需有關增強型 FILESTREAM 支援的詳細資訊，請參閱[FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)。  
  
開啟資料庫連接時， **@@TEXTSIZE** 會設定為-1 （「 無限制 」），根據預設。  
  
也可以使用 Windows 檔案系統 API 來存取及更新 FILESTREAM 資料行。  
  
如需詳細資訊，請參閱下列主題：  
  
-   [FILESTREAM 支援&#40;OLE DB&#41;](../../oledb/ole-db/filestream-support-ole-db.md)    
  
-   [使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)  
  
## <a name="querying-for-filestream-columns"></a>查詢是否有 FILESTREAM 資料行  
OLE DB 中的結構描述資料列集將不會報告某個資料行是否為 FILESTREAM 資料行。 ITableDefinition 中 OLE DB 無法用來建立 FILESTREAM 資料行。    
  
若要建立 FILESTREAM 資料行或是偵測哪些現有的資料行是 FILESTREAM 資料行，您可以使用**is_filestream**資料行[sys.columns](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)目錄檢視。  
  
以下是一個範例：  
  
```sql  
-- Create a table with a FILESTREAM column.  
CREATE TABLE Bob_01 (GuidCol1 uniqueidentifier ROWGUIDCOL NOT NULL UNIQUE DEFAULT NEWID(), IntCol2 int, varbinaryCol3 varbinary(max) FILESTREAM);  
  
-- Find FILESTREAM columns.  
SELECT name FROM sys.columns WHERE is_filestream=1;  
  
-- Determine whether a column is a FILESTREAM column.  
SELECT is_filestream FROM sys.columns WHERE name = 'varbinaryCol3' AND object_id IN (SELECT object_id FROM sys.tables WHERE name='Bob_01');  
```  
  
## <a name="down-level-compatibility"></a>下層相容性  
如果您的用戶端編譯時是使用 SQL server 的 OLE DB 驅動程式，應用程式連接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)])，然後**varbinary （max)**行為將會與行為相容所導入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的原生用戶端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。 也就是說，傳回之資料的大小最大值受限於 2 GB。 結果值大於 2 GB，就會進行截斷，將會傳回 「 字串資料右邊截斷 」 警告。 
  
當資料類型相容性設定為 80 時，用戶端行為將會與下層用戶端行為一致。  
  
使用 SQLOLEDB 或其他前發行的提供者的用戶端[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]， **varbinary （max)**會對應至映像。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
