---
title: OLE DB Driver for SQL Server 的系統需求
description: 了解在 OLE DB Driver for SQL Server 中使用 SQL Server 的資料存取功能 (例如 MARS) 所需的軟體必要條件。
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c86f62f98e81ce3c4fdd86e1e79e8f73e1422851
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127972"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的系統需求

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

若要使用 MARS 這類 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料存取功能，您必須已經安裝下列軟體：  

* 在用戶端上安裝 OLE DB Driver for SQL Server。  
* 在伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。

> [!NOTE]  
> 在安裝此軟體之前，請確定已使用管理員權限登入。  

## <a name="operating-system-requirements"></a>作業系統需求  

如需支援 OLE DB Driver for SQL Server 的作業系統清單，請參閱[OLE DB Driver for SQL Server 的支援原則](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)。  

## <a name="azure-active-directory-authentication-requirements"></a>Azure Active Directory 驗證需求  

使用 Azure Active Directory 驗證方法搭配 OLE DB driver for SQL Server *_ 18.3 之前的版本時，請確認已安裝 [SQL Server 的 Active Directory 驗證程式庫](https://go.microsoft.com/fwlink/?LinkID=513072)。 (18.3 版包含屬於其安裝程式套件的相依性。)其他驗證方法或 OLE DB 作業並不需要 ADAL。 如需詳細資訊，請參閱[使用 Azure Active Directory](features/using-azure-active-directory.md)。

## <a name="sql-server-requirements"></a>SQL Server 需求  

若要使用 OLE DB Driver for SQL Server 來存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料，您必須已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。  

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援來自所有 MDAC 版本、Windows Data Access Components 及所有 OLE DB Driver for SQL Server 版本的連線。 當舊版的用戶端版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接時，用戶端不知道的伺服器資料類型會對應至與用戶端版本相容的類型。 如需詳細資訊，請參閱[用戶端版本的資料類型相容性](#data-type-compatibility-for-client-versions)。  

## <a name="cross-language-requirements"></a>跨語言需求  

所有支援之作業系統的當地語系化版本都支援 OLE DB Driver for SQL Server 的英文版本。 在與 OLE DB Driver for SQL Server 的當地語系化版本相同語言的當地語系化作業系統上，支援 OLE DB Driver for SQL Server 的當地語系化版本。 只要有安裝相符的語言設定，受支援作業系統的英文版就會支援 OLE DB Driver for SQL Server 的當地語系化版本。  

在升級方面：  

可以將英文版的 OLE DB Driver for SQL Server 升級到任何當地語系化版本的 OLE DB Driver for SQL Server。  
* 可以將當地語系化版本的 OLE DB Driver for SQL Server 升級到相同語言之當地語系化版本的 OLE DB Driver for SQL Server。  
* 可以將當地語系化版本的 OLE DB Driver for SQL Server 升級到英文版本的 OLE DB Driver for SQL Server。  
* 不可以將當地語系化版本的 OLE DB Driver for SQL Server 升級到不同當地語系化語言之當地語系化版本的 OLE DB Driver for SQL Server。  

## <a name="data-type-compatibility-for-client-versions"></a>用戶端版本的資料類型相容性  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 OLE DB Driver for SQL Server 會將新的資料類型對應到與下層用戶端相容的舊版資料類型，如下表所示。  

OLE DB 和 ADO 應用程式可以使用 **DataTypeCompatibility** 連接字串關鍵字搭配 OLE DB Driver for SQL Server，以便操作舊版的資料類型。 當 **DataTypeCompatibility=80** 時，OLE DB 用戶端會使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 表格式資料流 (TDS) 版本而非 TDS 版本進行連線。 這表示對 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和較新的資料類型來說，下層的轉換將由伺服器執行，而不是 OLE DB Driver for SQL Server。 也表示連接可以使用的功能將限於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 在 API 呼叫時，即可偵測出使用新資料類型或功能的嘗試，且錯誤會傳回給進行呼叫的應用程式，而不會嘗試將無效的要求傳遞給伺服器。  

IDBInfo::GetKeywords 將一律會傳回與連線上的伺服器版本相對應的關鍵字清單，且不受 **DataTypeCompatibility** 的影響。  

|資料類型|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components、MDAC 和<br /><br /> 具有 DataTypeCompatibility=80 的 OLE DB Driver for SQL Server OLE DB 應用程式|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|映像|  
|varchar(max)|varchar|varchar|varchar|Text|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|Xml|Xml|Xml|Xml|Ntext|  
|CLR UDT (> 8 Kb)|varbinary|udt|udt|映像|  
|date|varchar|date|date|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>另請參閱  

[OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)  
[安裝 OLE DB Driver for SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
