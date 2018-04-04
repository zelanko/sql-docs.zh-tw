---
title: OLE DB 驅動程式的 SQL Server 程式設計 |Microsoft 文件
description: OLE DB 驅動程式的 SQL Server 程式設計
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1a3d642eb3cef1f9f01accd8b50f571f5e4903ac
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server-programming"></a>SQL Server 程式設計的 OLE DB 驅動程式
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驅動程式的 SQL Server 是獨立的資料存取應用程式開發介面 (API)，用於 OLE DB 中導入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 OLE DB 驅動程式的 SQL Server 提供一個動態連結程式庫 (DLL) 中的 SQL OLE DB 驅動程式。 此介面也提供遠超過 Windows Data Access Components (Windows DAC，之前稱為 Microsoft Data Access Components，或稱 MDAC) 的新功能。 OLE DB 驅動程式的 SQL Server 可以用來建立新的應用程式，或者加強需要利用所引進的功能的現有應用程式[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，例如多個 active result set (MARS)、 使用者定義資料型別 (UDT)、 查詢通知、 快照集隔離和 XML 資料類型支援。  
  
> [!NOTE]  
>  如需 OLE DB 驅動程式的 SQL Server 和 Windows DAC，再加上有關問題的資訊來更新適用於 SQL Server 的 OLE DB 驅動程式的 Windows DAC 應用程式之前，請考慮差異的清單，請參閱[應用程式更新至 OLE DB 驅動程式 （SQL)從 MDAC 伺服器](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
 SQL Server OLE DB 驅動程式可以搭配 OLE DB 核心服務提供與 Windows DAC，但是這並非必要條件。若要使用的核心服務，或不選擇取決於個別的應用程式 （例如，如果需要連接共用） 的需求。  
  
 ActiveX Data Object (ADO) 應用程式可能會用於 SQL Server 的 OLE DB 驅動程式，但建議使用 ADO 搭配**DataTypeCompatibility**連接字串關鍵字 (或其對應**資料來源**屬性)。 ADO 應用程式時使用 SQL Server 的 OLE DB 驅動程式，可以利用這些中引進的新功能[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]可透過 SQL Server OLE DB 驅動程式透過連接字串關鍵字或 OLE DB 屬性或[!INCLUDE[tsql](../../includes/tsql-md.md)]。 如需有關使用搭配 ADO 使用這些功能，請參閱[使用 ADO 與 OLE DB 驅動程式的 SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
 OLE DB 驅動程式的 SQL Server 被設計來提供簡化的 SQL Server 使用 OLE DB 原生資料存取方式。 它提供方法來改革及發展新的資料存取功能，而不需要變更目前的 Windows DAC 元件現在是 Microsoft Windows 平台的一部分。  
  
 OLE DB 驅動程式的 SQL Server 使用 Windows DAC 中的元件，但並非明確相依於特定的 Windows DAC 版本。 您可以使用適用於 SQL Server 的 OLE DB 驅動程式會隨 SQL Server 的 OLE DB 驅動程式支援的任何作業系統的 Windows DAC 版本。  
  
## <a name="in-this-section"></a>本節內容  
 [SQL Server 的 OLE DB 驅動程式](../oledb/oledb-driver-for-sql-server.md)  
 列出重要新 OLE DB 驅動程式的 SQL Server 功能。  
  
 [當使用 SQL Server 的 OLE DB 驅動程式](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 討論如何 OLE DB 驅動程式的 SQL 伺服器配合 Microsoft 資料存取技術，它會比較 Windows DAC 和 ADO.NET，並提供指標以決定資料存取技術的使用。  
  
 [SQL Server 功能的 OLE DB 驅動程式](../oledb/features/oledb-driver-for-sql-server-features.md )  
 描述 SQL Server 的 OLE DB 驅動程式支援的功能。  
  
 [使用 OLE DB 驅動程式的 SQL Server 的建立應用程式](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 提供 SQL Server 開發，包含與 Windows DAC 的元件，它會使用，以及如何 ADO 可以搭配 OLE DB 驅動程式的概觀。  
  
 本章節也討論 OLE DB 驅動程式，SQL Server 安裝與部署，包括如何轉散發 SQL Server 文件庫，OLE DB 驅動程式。  
  
 [適用於 SQL Server 的 OLE DB 驅動程式的系統需求](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 討論使用 SQL Server 的 OLE DB 驅動程式所需的系統資源。  
  
 [SQL Server 的 OLE DB 驅動程式&#40;OLE DB&#41;](../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
 提供使用 SQL Server 的 OLE DB 驅動程式的相關資訊。  
  
 [如需 SQL Server 資訊尋找更多的 OLE DB 驅動程式](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 SQL Server，包括外部資源的連結，取得進一步協助提供 OLE DB 驅動程式的其他資源。  
  
  
## <a name="see-also"></a>另請參閱  
 [從 SQL Server 2005 Native Client 將應用程式更新](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 的使用說明主題](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
