---
title: FILESTREAM 支援 | Microsoft Docs
description: OLE DB Driver for SQL Server 中的 FILESTREAM 支援
ms.custom: ''
ms.date: 09/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- FILESTREAM [SQL Server], OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server [FILESTREAM support]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: da67f050eba24ecf040124533c9d98c3f3f6bfec
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74056736"
---
# <a name="filestream-support"></a>FILESTREAM 支援
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，OLE DB Driver for SQL Server 支援已增強的 FILESTREAM 功能。 如需範例，請參閱 [Filestream 及 OLE DB](../../oledb/ole-db-how-to/filestream/filestream-and-ole-db.md)。  

FILESTREAM 提供透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或直接存取 Windows 檔案系統來儲存及存取大型二進位值的方式。 大型二進位值是大於 2 GB 的值。 如需有關增強型 FILESTREAM 支援的詳細資訊，請參閱 [FILESTREAM &#40;SQL Server&#41;](../../../relational-databases/blob/filestream-sql-server.md)。  
  
當開啟資料庫連接時， **\@\@TEXTSIZE** 根據預設會設定為 -1 (「無限制」)。  
  
也可以使用 Windows 檔案系統 API 來存取及更新 FILESTREAM 資料行。  
  
如需詳細資訊，請參閱[使用 OpenSqlFilestream 存取 FILESTREAM 資料](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)。  
  
## <a name="querying-for-filestream-columns"></a>查詢是否有 FILESTREAM 資料行  
OLE DB 中的結構描述資料列集將不會報告某個資料行是否為 FILESTREAM 資料行。 OLE DB 中的 ITableDefinition 不能用來建立 FILESTREAM 資料行。    
  
若要建立 FILESTREAM 資料行或是偵測哪些現有資料行為 FILESTREAM 資料行，您可以使用 **sys.columns** 目錄檢視的 [is_filestream](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md) 資料行。  
  
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
如果您的用戶端是使用 OLE DB Driver for SQL Server 編譯的，而且應用程式連接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)])，則 **varbinary(max)** 行為將與 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引進的行為相容。 也就是說，傳回之資料的大小最大值受限於 2 GB。 如果結果值大於 2 GB，將會發生截斷，而且將會傳回「字串資料右邊截斷」警告。 
  
當資料類型相容性設定為 80 時，用戶端行為將會與下層用戶端行為一致。  
  
如果是使用 SQLOLEDB 的用戶端或是在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前發行的其他提供者，**varbinary(max)** 將會對應到 image。  
  
## <a name="comments"></a>註解
- 若要傳送與接收大於 2 GB 的 **varbinary(max)** 值，應用程式會在參數和結果繫結中使用 **DBTYPE_IUNKNOWN**。 若是參數，提供者必須針對 ISequentialStream 和傳回 ISequentialStream 的結果，呼叫 IUnknown::QueryInterface。  

-  若是 OLE DB，將會放寬與 ISequentialStream 值相關的檢查。 當 *wType* 在 **DBBINDING** 結構中為 **DBTYPE_IUNKNOWN** 時，可以從 **dwPart** 中省略 *DBPART_LENGTH*，或將資料長度 (在資料緩衝區中的位移 *obLength*) 設定為 ~ 0，以停用長度檢查。 在此情況下，提供者將不會檢查值的長度，而且將會透過資料流要求並傳回所有可用的資料。 這項變更將會套用到所有大型物件 (LOB) 類型與 XML，但是只會在連接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] (或更新版本) 伺服器時才會套用。 這將會提供開發人員更大的彈性，同時維持現有應用程式與下層伺服器的一致性與回溯相容性。  此變更會影響傳輸資料的所有介面，主要是 IRowset::GetData、ICommand::Execute 和 IRowsetFastLoad::InsertRow。
 

## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 功能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
