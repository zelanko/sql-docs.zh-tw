---
title: 資料表和索引 |Microsoft Docs
description: 建立、 改變和 droping 的資料表和索引使用 OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- OLE DB Driver for SQL Server, tables
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 9c491180eaf101ef3495ed015252b0fad60ef222
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743116"
---
# <a name="tables-and-indexes"></a>資料表和索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 會公開 **IIndexDefinition** 和 **ITableDefinition** 介面，讓取用者建立、改變和卸除 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表和索引。 有效的資料表和索引定義是取決於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本。  
  
 建立或卸除資料表和索引的能力，取決於取用者應用程式使用者的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存取權限。 卸除資料表可藉由宣告式參考完整性條件約束或其他因數的存在，而受進一步的條件約束。  
  
 大部分的應用程式目標設為[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]for SQL Server 介面，而這些 OLE DB 驅動程式不是使用 SQL-DMO。 SQL-DMO 是 OLE Automation 物件的集合，可支援 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 所有的管理功能。 以多個 OLE DB 提供者為目標的應用程式會使用這些受多個 OLE DB 提供者支援的一般 OLE DB 介面。  
  
 在提供者特定屬性集 DBPROPSET_SQLSERVERCOLUMN 中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會定義下列屬性。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|類型：VT_BSTR<br /><br /> R/W：寫入<br /><br /> 預設值：Null<br /><br /> 描述：此屬性只能用於 **ITableDefinition**。 在建立 [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md) 時會使用這個屬性指定的字串<br /><br /> 陳述式。|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立 SQL Server 資料表](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [將資料行新增至 SQL Server 資料表](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [從 SQL Server 資料表中移除資料行](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [卸除 SQL Server 資料表](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [建立 SQL Server 索引](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [卸除 SQL Server 索引](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server 程式設計](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
