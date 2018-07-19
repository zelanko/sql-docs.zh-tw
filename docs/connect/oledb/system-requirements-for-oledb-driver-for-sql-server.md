---
title: 適用於 SQL Server 的 OLE DB 驅動程式的系統需求 |Microsoft 文件
description: 適用於 SQL Server OLE DB 驅動程式的需求
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
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 485693e8f350370a293696a09f11ba036397b15e
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689461"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>適用於 SQL Server 的 OLE DB 驅動程式的系統需求
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  若要使用 MARS 這類 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料存取功能，您必須已經安裝下列軟體：  

-   OLE DB 驅動程式的用戶端上的 SQL Server。  

-   在伺服器上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。   

> [!NOTE]  
>  在安裝此軟體之前，請確定已使用管理員權限登入。  

## <a name="operating-system-requirements"></a>作業系統需求  
 如需 SQL Server 的支援 OLE DB 驅動程式的作業系統，請參閱[OLE DB driver for SQL Server 的支援原則](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md)。  

## <a name="sql-server-requirements"></a>SQL Server 需求  
 若要使用 SQL Server 的 OLE DB 驅動程式，將存取資料的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫，您必須擁有的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援用於 SQL Server 所有版本的 MDAC、 Windows Data Access Components 及所有版本的 OLE DB 驅動程式的連接。 當舊版的用戶端版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接時，用戶端不知道的伺服器資料類型會對應至與用戶端版本相容的類型。 如需詳細資訊，請參閱本主題稍後的「用戶端版本的資料類型相容性」。  

## <a name="cross-language-requirements"></a>跨語言需求  
 支援的作業系統的所有當地語系化版本都支援英文版的 OLE DB 驅動程式的 SQL Server。 當地語系化 OLE DB 驅動程式的 SQL Server 版本相同語言的當地語系化作業系統上支援的 OLE DB 驅動程式的 SQL Server 的當地語系化的版本。 OLE DB 驅動程式的 SQL Server 的當地語系化的版本也支援在支援的作業系統英文版上，只要安裝相符的語言設定。  

 在升級方面：  

-   OLE DB 驅動程式的 SQL Server 的英文版可以升級至任何當地語系化版本的 OLE DB 驅動程式，適用於 SQL Server。  

-   相同語言的 SQL Server 的 OLE DB 驅動程式的 SQL Server 的當地語系化的版本可以升級到 OLE DB 驅動程式的當地語系化版本。  

-   OLE DB 驅動程式的 SQL Server 的當地語系化的版本可以升級至英文版的 OLE DB 驅動程式，適用於 SQL Server。  

-   OLE DB 驅動程式的 SQL Server 的當地語系化的版本無法升級至當地語系化 OLE DB 驅動程式的不同當地語系化語言的 SQL Server 版本。  

## <a name="data-type-compatibility-for-client-versions"></a>用戶端版本的資料類型相容性  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 驅動程式的 SQL Server 對應新的資料類型到較舊的資料類型，而且與下層用戶端，如下表所示。  

 OLE DB 和 ADO 的應用程式可以使用**DataTypeCompatibility**連接字串關鍵字搭配 OLE DB 驅動程式的 SQL Server，以便操作舊版的資料類型。 當**DataTypeCompatibility = 80**，OLE DB 用戶端會使用連接[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]表格式資料流 (TDS) 版本，而非 TDS 版本。 這表示對於[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]和更新版本的資料類型，下層的轉換將會執行伺服器，而不是 OLE DB 驅動程式的 SQL Server。 也表示連接可以使用的功能將限於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 功能集。 在 API 呼叫時，即可偵測出使用新資料類型或功能的嘗試，且錯誤會傳回給進行呼叫的應用程式，而不會嘗試將無效的要求傳遞給伺服器。   


 IDBInfo::GetKeywords 一律會傳回的關鍵字清單，對應到連接上的伺服器版本，而且不會受到**DataTypeCompatibility**。  

|資料類型|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|SQL Server 的 OLE DB 驅動程式|Windows Data Access Components、MDAC 和<br /><br /> OLE DB 驅動程式的 SQL Server OLE DB 應用程式與 DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|varchar(max)|varchar|varchar|varchar|文字|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|CLR UDT (> 8Kb)|varbinary|udt|udt|image|  
|日期|varchar|日期|日期|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>另請參閱  
 [SQL Server 的 OLE DB 驅動程式](../oledb/oledb-driver-for-sql-server.md)   
 [安裝 OLE DB Driver for SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
