---
title: OLE DB Driver for SQL Server 的系統需求 | Microsoft Docs
description: OLE DB Driver for SQL Server 的需求
ms.custom: ''
ms.date: 02/12/2019
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: cec8b2aca53f64e7a3883dbccddce1a330c8a6e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993785"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的系統需求
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  若要使用 MARS 這類 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料存取功能，您必須已經安裝下列軟體：  

-   用戶端上 SQL Server 的 OLE DB 驅動程式。  

-   在伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。   

> [!NOTE]  
>  在安裝此軟體之前，請確定已使用管理員權限登入。  

## <a name="operating-system-requirements"></a>作業系統需求  
 如需支援 SQL Server 之 OLE DB 驅動程式的作業系統清單, 請參閱[SQL Server OLE DB 驅動程式的支援原則](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)。  

 ## <a name="azure-active-directory-authentication-requirements"></a>Azure Active Directory 驗證需求  
 搭配 OLE DB 驅動程式使用 Azure Active Directory 驗證方法時, 請確定已安裝[SQL Server 的 Active Directory 驗證程式庫](https://go.microsoft.com/fwlink/?LinkID=513072)。 其他驗證方法或 OLE DB 作業不需要 ADAL。
如需詳細資訊，請參閱[使用 Azure Active Directory](features/using-azure-active-directory.md)。

## <a name="sql-server-requirements"></a>SQL Server 需求  
 若要使用 SQL Server 的 OLE DB 驅動程式來存取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫中的資料, 您必須[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝實例。  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援來自所有 MDAC 版本、Windows Data Access Components 及所有 OLE DB Driver for SQL Server 版本的連線。 當舊版的用戶端版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接時，用戶端不知道的伺服器資料類型會對應至與用戶端版本相容的類型。 如需詳細資訊，請參閱[用戶端版本的資料類型相容性](#data-type-compatibility-for-client-versions)。  

## <a name="cross-language-requirements"></a>跨語言需求  
 支援的作業系統的所有當地語系化版本都支援 SQL Server 的 OLE DB 驅動程式的英文版。 當地語系化的作業系統支援 SQL Server 的 OLE DB 驅動程式的當地語系化版本, 這是與 SQL Server 版本的當地語系化 OLE DB 驅動程式相同的語言。 只要有安裝相符的語言設定，受支援作業系統的英文版就會支援 OLE DB Driver for SQL Server 的當地語系化版本。  

 在升級方面：  

-   SQL Server 的 OLE DB 驅動程式的英文版本可以升級至任何當地語系化版本的 OLE DB 驅動程式以進行 SQL Server。  

-   SQL Server 的 OLE DB 驅動程式當地語系化版本可以升級至相同語言 SQL Server 的 OLE DB 驅動程式當地語系化版本。  

-   SQL Server 的 OLE DB 驅動程式當地語系化版本可以升級為 SQL Server OLE DB 驅動程式的英文版。  

-   SQL Server 的 OLE DB 驅動程式的當地語系化版本無法升級為不同當地語系化語言 SQL Server 版本的當地語系化 OLE DB 驅動程式。  

## <a name="data-type-compatibility-for-client-versions"></a>用戶端版本的資料類型相容性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 OLE DB Driver for SQL Server 會將新的資料類型對應到與下層用戶端相容的舊版資料類型，如下表所示。  

 OLE DB 和 ADO 應用程式可以使用**DataTypeCompatibility**連接字串關鍵字搭配 OLE DB 驅動程式, 以便 SQL Server 與舊版資料類型一起運作。 當 **DataTypeCompatibility=80** 時，OLE DB 用戶端會使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 表格式資料流 (TDS) 版本而非 TDS 版本進行連線。 這表示對 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和較新的資料類型來說，下層的轉換將由伺服器執行，而不是 OLE DB Driver for SQL Server。 也表示連接可以使用的功能將限於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 在 API 呼叫時，即可偵測出使用新資料類型或功能的嘗試，且錯誤會傳回給進行呼叫的應用程式，而不會嘗試將無效的要求傳遞給伺服器。   


 IDBInfo:: GetKeywords 一律會傳回對應至連接上之伺服器版本的關鍵字清單, 而且不會受到**DataTypeCompatibility**的影響。  

|資料類型|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|OLE DB Driver for SQL Server|Windows Data Access Components、MDAC 和<br /><br /> 使用 DataTypeCompatibility = 80 SQL Server OLE DB 應用程式的 OLE DB 驅動程式|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|文字|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8 Kb)|varbinary|udt|udt|image|  
|日期|varchar|日期|日期|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [安裝 OLE DB Driver for SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
