---
title: Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Microsoft OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: adc18554ebb4494112f424f3e6a3dd02c13b121c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993789"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

OLE DB Driver for SQL Server 是用於 OLE DB 的獨立資料存取應用程式開發介面 (API) (已在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中導入)。 OLE DB Driver for SQL Server 會在一個動態連結程式庫 (DLL) 中提供 SQL OLE DB 驅動程式。 此介面也提供遠超過 Windows Data Access Components (Windows DAC，之前稱為 Microsoft Data Access Components，或稱 MDAC) 的新功能。 OLE DB Driver for SQL Server 可用於建立新的應用程式，或者加強需要利用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中所導入功能 (例如，Multiple Active Result Set (MARS)、使用者定義資料型別 (UDT)、查詢通知、快照集隔離和 XML 資料型別支援) 的現有應用程式。  
  
> [!NOTE]  
> 如需 OLE DB Driver for SQL Server 和 Windows DAC 之間的差異清單，以及在將 Windows DAC 應用程式更新為 OLE DB Driver for SQL Server 前要考慮之問題的相關資訊，請參閱[將應用程式從 MDAC 更新為 OLE DB Driver for SQL Server](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  

> [!IMPORTANT]
> 先前的 [Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 和 [SQL Server Native Client OLE DB](../../relational-databases/native-client/sql-server-native-client.md) 提供者 (SQLNCLI) 仍會被取代，因而不建議將它們用於新的程式開發工作。
  
 OLE DB Driver for SQL Server 可以配合 Windows DAC 所提供的 OLE DB Core Services 使用，但這並非必要條件；是否使用 Core Services 是依個別應用程式的需求而定 (例如，是否需要連接共用)。  
  
 ActiveX Data Object (ADO) 應用程式可能會使用 OLE DB Driver for SQL Server，但建議將 ADO 搭配 **DataTypeCompatibility** 連接字串關鍵字 (或其對應的 **DataSource** 屬性) 使用。 使用 OLE DB Driver for SQL Server 時，ADO 應用程式可能會利用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中所導入的新功能，這些新功能可透過連接字串關鍵字或 OLE DB 屬性或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，透過 OLE DB Driver for SQL Serve 使用。 如需搭配 ADO 使用這些功能的詳細資訊，請參閱[搭配使用 ADO 與 OLE DB Driver for SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
 OLE DB Driver for SQL Server 的設計目的是提供簡化的方法，讓您使用 OLE DB 取得 SQL Server 的原生資料存取權。 它提供一種方式來改革及發展新的資料存取功能，而不需變更目前的 Windows DAC 元件 (這些元件現在為 Microsoft Windows 平台的一部分)。  
  
 雖然 OLE DB Driver for SQL Server 會使用 Windows DAC 中的元件，但它並非明確相依於特定的 Windows DAC 版本。 您可以使用 OLE DB Driver for SQL Server 搭配 OLE DB Driver for SQL Server 所支援之任何作業系統安裝的 Windows DAC 版本。  

 ## <a name="different-generations-of-ole-db-drivers"></a>不同世代的 OLE DB 驅動程式

有三個不同世代的 Microsoft OLE DB Provider for SQL Server。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍隨附於 [Windows Data Access Component](https://msdn.microsoft.com/library/ms692897.aspx) \(英文\)。 它已不再受到維護，因此，不建議使用此驅動程式來進行新開發。

### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)
從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，[SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) 包含 OLE DB 提供者介面 (SQLNCLI)，其為透過 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 隨附於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 OLE DB 提供者。

[已在 2011 年宣布取代](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) \(英文\) 它，因此，不建議使用此驅動程式來進行新開發。 如需 SNAC 生命週期與可用下載的詳細資訊，請參閱 [SNAC 生命週期的說明](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/) \(英文\)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE DB 已[取消取代](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) \(英文\) 並於 2018 年發行。

新的 OLE DB 提供者稱為 Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)。 從現在開始，新的提供者將使用最新的伺服器功能來更新。

> [!NOTE]
> 若要在現有的應用程式中使用新的 Microsoft OLE DB Driver for SQL Server，您應該規劃將連接字串從 SQLOLEDB 或 SQLNCLI 轉換為 MSOLEDBSQL。
  
## <a name="in-this-section"></a>本節內容  
[使用 OLE DB Driver for SQL Server 的時機](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 討論 OLE DB Driver for SQL Server 在 Microsoft 資料存取技術中扮演什麼角色、它與 Windows DAC 和 ADO.NET 的比較，並提供指標以決定要使用什麼資料存取技術。  
  
 [OLE DB Driver for SQL Server 功能](../oledb/features/oledb-driver-for-sql-server-features.md )  
 說明 OLE DB Driver for SQL Server 所支援的功能。  
  
 [使用 OLE DB Driver for SQL Server 建置應用程式](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 提供 OLE DB Driver for SQL Server 開發的概觀，包括與 Windows DAC 的差異、所使用的元件，以及如何搭配 ADO 使用。  
  
 本節也會討論 OLE DB Driver for SQL Server 安裝和部署，包括如何轉散發 OLE DB Driver for SQL Server 程式庫。  
  
 [OLE DB Driver for SQL Server 的系統需求](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 討論使用 OLE DB Driver for SQL Server 所需的系統資源。  
  
 [OLE DB Driver for SQL Server 程式設計](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 提供使用 OLE DB Driver for SQL Server 的相關資訊。  
  
 [尋找更多 OLE DB Driver for SQL Server 資訊](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 提供 OLE DB Driver for SQL Server 的其他相關資源，包括外部資源及取得進一步協助的連結。  
  
  
## <a name="see-also"></a>另請參閱  
 [從 SQL Server 2005 Native Client 更新應用程式](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 使用說明主題](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
