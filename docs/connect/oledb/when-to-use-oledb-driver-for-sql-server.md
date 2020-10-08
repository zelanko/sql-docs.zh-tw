---
title: 使用 OLE DB Driver 的時機
description: 了解何時應使用 OLE DB Driver for SQL Server，以及使其與其他驅動程式有所區別的概要資料存取概念。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cca9bd078060ee9a03df996a62353d051c9625b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726899"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>使用 OLE DB Driver for SQL Server 的時機
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 是可用來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中資料的其中一種技術。  如需不同資料存取技術的討論內容，請參閱 [Data Access Technologies Road Map](../connect-history.md) (資料存取技術藍圖)  
  
 決定是否要使用 OLE DB Driver for SQL Server 當做應用程式的資料存取技術時，您應該考慮許多因素。  
  
 對於新的應用程式而言，如果您正在使用 Microsoft Visual C# 或 Visual Basic 等 Managed 程式語言，而且需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的新功能，則應該使用 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (屬於 .NET Framework 的一部分)。  
  
 如果您正在開發以 COM 為基礎的應用程式，而且需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所導入的新功能，則應該使用 OLE DB Driver for SQL Server。 如果您不需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能，可以繼續使用 Windows Data Access Components (WDAC)。  
  
 對於現有的 OLE DB 應用程式而言，主要的問題在於您是否需要存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新功能。 如果您有一個不需要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之新功能的完整應用程式，就可以繼續使用 WDAC。 但是，如果您需要存取這些新功能 (例如 [xml 資料類型](../../t-sql/xml/xml-transact-sql.md))，就應該使用 OLE DB Driver for SQL Server。  
  
 OLE DB Driver for SQL Server 和 MDAC 都支援使用資料列版本設定進行讀取認可的交易隔離，但是只有 OLE DB Driver for SQL Server 支援快照集交易隔離。 (在程式設計的詞彙中，含有資料列版本設定的讀取認可交易隔離與讀取認可的交易相同)。  
  
 如需 OLE DB Driver for SQL Server 和 MDAC 之間差異的相關資訊，請參閱[將應用程式從 MDAC 更新為 OLE DB Driver for SQL Server](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server](oledb-driver-for-sql-server.md)  
 [OLE DB 的使用說明主題](ole-db-how-to/ole-db-how-to-topics.md)  
  
