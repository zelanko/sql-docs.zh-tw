---
title: 當使用 SQL Server 的 OLE DB 驅動程式 |Microsoft 文件
description: 當使用 SQL Server 的 OLE DB 驅動程式
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1aaca043dc057f6f7cc07322e6bf75822a8ebe8b
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690101"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>當使用 SQL Server 的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB 驅動程式的 SQL Server 是一種技術可讓您存取資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫。  如需不同的資料存取技術的討論，請參閱[資料存取技術藍圖](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 決定是否要使用 SQL Server 的 OLE DB 驅動程式，為您的應用程式的資料存取技術，當您應該考慮許多因素。  
  
 對於新的應用程式而言，如果您正在使用 Microsoft Visual C# 或 Visual Basic 等 Managed 程式語言，而且需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，則應該使用 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (屬於 .NET Framework 的一部分)。  
  
 如果您正在開發以 COM 為基礎的應用程式，而且需要存取所引進的新功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您應該使用 SQL server 的 OLE DB 驅動程式。 如果您不需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，可以繼續使用 Windows Data Access Components (WDAC)。  
  
 對於現有的 OLE DB 應用程式，主要的問題在於您是否需要存取的新功能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果您有一個不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之新功能的完整應用程式，就可以繼續使用 WDAC。 但是，如果您需要存取這些新功能，例如[xml 資料型別](../../t-sql/xml/xml-transact-sql.md)，您應該使用 SQL server 的 OLE DB 驅動程式。  
  
 SQL Server 和 MDAC 支援這兩個 OLE DB 驅動程式讀取認可的交易隔離資料列版本設定，但只有 OLE DB 驅動程式使用 SQL Server 支援快照集交易隔離。 (在程式設計的詞彙中，含有資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  
  
 OLE DB 驅動程式的 SQL Server 與 MDAC 之間差異的詳細資訊，請參閱[應用程式更新至 OLE DB 驅動程式的 SQL Server 從 MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 的 OLE DB 驅動程式](../oledb/oledb-driver-for-sql-server.md)     
 [OLE DB 的使用說明主題](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
