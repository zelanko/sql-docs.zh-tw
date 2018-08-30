---
title: Microsoft OLE DB Driver for SQL Server | Microsoft Docs
description: Microsoft OLE DB Driver for SQL Server
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
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 3e1764fdd2a96fcf1d0da218ef86b2e4cb62fd8c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025909"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Microsoft OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 是獨立的資料存取應用程式開發介面 (API)，用於 OLE DB 中導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 OLE DB Driver for SQL Server 提供 SQL OLE DB 驅動程式，在單一動態連結程式庫 (DLL)。 此介面也提供遠超過 Windows Data Access Components (Windows DAC，之前稱為 Microsoft Data Access Components，或稱 MDAC) 的新功能。 OLE DB Driver for SQL Server 可用於建立新的應用程式，或者加強需要利用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所推出之新功能 (例如，Multiple Active Result Set (MARS)、使用者定義資料型別 (UDT)、查詢通知、快照隔離和 XML 資料類型支援) 的現有應用程式。  
  
> [!NOTE]  
>  如需 OLE DB Driver for SQL Server 和 Windows DAC，加上之問題的資訊來更新適用於 SQL Server 的 OLE DB 驅動程式的 Windows DAC 應用程式之前，請考慮之間的差異，請參閱[應用程式更新至 OLE DB Driver for SQL從 MDAC server](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
 OLE DB Driver for SQL Server 可以配合 Windows DAC 所提供的 OLE DB Core Services 使用，但這並非必要條件；是否使用 Core Services 是依個別應用程式的需求而定 (例如，是否需要連接共用)。  
  
 ActiveX Data Object (ADO) 應用程式可能會使用 OLE DB Driver for SQL Server，但建議您搭配使用 ADO **DataTypeCompatibility**連接字串關鍵字 (或其對應**資料來源**屬性)。 當使用 OLE DB Driver for SQL Server，ADO 應用程式，可利用推出這些新功能[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]透過連接字串關鍵字或 OLE DB 屬性可透過 OLE DB Driver for SQL Server 或[!INCLUDE[tsql](../../includes/tsql-md.md)]。 如需有關使用搭配 ADO 使用這些功能，請參閱[使用的 ADO 與 OLE DB Driver for SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
 OLE DB Driver for SQL Server 的設計目的是提供簡化的方法，讓您使用 OLE DB 取得 SQL Server 的原生資料存取權。 它提供方法來改革及發展新的資料存取功能，而不需要變更目前的 Windows DAC 元件現在是 Microsoft Windows 平台的一部分。  
  
 雖然 OLE DB Driver for SQL Server 會使用 Windows DAC 中的元件，但它並非明確相依於特定的 Windows DAC 版本。 您可以使用適用於 SQL Server 的 OLE DB 驅動程式，使用與任何 OLE DB Driver for SQL Server 支援的作業系統一起安裝的 Windows DAC 版本。  

 ## <a name="different-generations-of-ole-db-drivers"></a>不同的層代的 OLE DB 驅動程式

有三個不同的層代的 SQL Server 的 Microsoft OLE DB 提供者。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍然隨附[Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx)。 它不會再維護，不建議用於新的開發中使用此驅動程式。

### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)
從開始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，則[SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供者介面 (SQLNCLI)，並隨附的 OLE DB 提供者[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]透過[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。

很[宣布淘汰在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)也不建議用於新的開發中使用此驅動程式。 如需有關可用的下載與 SNAC 生命週期的詳細資訊，請參閱[所述的 SNAC 生命週期](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE db[取消](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)和在 2018 年發行。

新的 OLE DB 提供者會呼叫 Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)。 新的提供者將會更新為最新的伺服器功能，從現在開始使用。

> [!NOTE]
> 若要使用新 Microsoft OLE DB Driver for SQL Server，在現有的應用程式中，您應該規劃您的連接字串從 SQLOLEDB 或 SQLNCLI，轉換 MSOLEDBSQL。
  
## <a name="in-this-section"></a>本節內容  
[使用 OLE DB Driver for SQL Server 的時機](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 討論 OLE DB Driver for SQL Server 在 Microsoft 資料存取技術中扮演什麼角色、它與 Windows DAC 和 ADO.NET 的比較，並提供指標以決定要使用什麼資料存取技術。  
  
 [OLE DB Driver for SQL Server 功能](../oledb/features/oledb-driver-for-sql-server-features.md )  
 說明 OLE DB Driver for SQL Server 支援的功能。  
  
 [利用 OLE DB Driver for SQL Server 建置](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 提供 OLE DB Driver for SQL Server 開發的概觀，包括與 Windows DAC 的差異、所使用的元件，以及如何搭配 ADO 使用。  
  
 本章節也會討論 OLE DB Driver for SQL Server 安裝和部署，包括如何轉散發 OLE DB Driver for SQL Server 文件庫。  
  
 [OLE DB Driver for SQL Server 的系統需求](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 討論使用 OLE DB Driver for SQL Server 所需的系統資源。  
  
 [OLE DB Driver for SQL Server 程式設計](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 提供使用 OLE DB Driver for SQL Server 的相關資訊。  
  
 [尋找詳細的 OLE DB Driver for SQL Server 資訊](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 提供有關 OLE DB 驅動程式的其他資源，適用於 SQL Server，包括外部資源的連結，及取得進一步協助。  
  
  
## <a name="see-also"></a>另請參閱  
 [從 SQL Server 2005 Native Client 更新應用程式](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 的使用說明主題](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
