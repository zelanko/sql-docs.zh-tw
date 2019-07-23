---
title: 使用 OLE DB Driver for SQL Server 標頭與程式庫檔案 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 標頭及程式庫檔案
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989229"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用 OLE DB Driver for SQL Server 標頭及程式庫檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在安裝過程中選取 [適用于 SQL Server SDK 的 OLE DB 驅動程式] 選項時, 會安裝 SQL Server 標頭和程式庫檔案的 OLE DB 驅動程式。 開發應用程式時，將開發所需的所有檔案複製並安裝到您的開發環境相當重要。 如需針對 SQL Server 安裝和轉散發 OLE DB 驅動程式的詳細資訊, 請參閱[安裝適用于 SQL Server 的 OLE DB 驅動程式](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 SQL Server 標頭檔和程式庫檔案的 OLE DB 驅動程式會安裝在下列位置:  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 SQL Server 標頭檔的 OLE DB 驅動程式 (內含 msoledbsql.h) 可以用來將 SQL Server 資料存取功能的 OLE DB 驅動程式新增至您的自訂應用程式。 OLE DB Driver for SQL Server 標頭檔包含使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所導入之新功能所需的所有定義、屬性 (Attribute)、屬性 (Property) 與介面。  
  
 除了 SQL Server 標頭檔的 OLE DB 驅動程式之外, 還有內含 msoledbsql.h 的程式庫檔案, 也就是[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)功能的匯出程式庫。  
  
 OLE DB Driver for SQL Server 標頭檔與搭配 Microsoft Data Access Components (MDAC) 所使用的 sqloledb.h 標頭檔具回溯相容性，但是不包含適用於 SQLOLEDB 的 CLSID (MDAC 隨附的 OLE DB Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 或適用於 XML 功能的符號 (不受 OLE DB Driver for SQL Server 所支援)。    
  
 OLE DB 使用 OLE DB Driver for SQL Server 的應用程式只需要參考內含 msoledbsql.h。 如果應用程式同時使用 MDAC (SQLOLEDB) 和 OLE DB Driver for SQL Server，則可以同時參考 sqloledb.h 和 msoledbsql.h，但是必須先參考 sqloledb.h。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>使用 SQL Server 標頭檔的 OLE DB 驅動程式  
 若要使用 SQL Server 標頭檔的 OLE DB 驅動程式, 您必須在  C/C++程式設計程式碼中使用 include 語句。 下列各節說明如何在 OLE DB 應用程式中執行此動作。  
  
> [!NOTE]  
>  SQL Server 標頭檔和程式庫檔案的 OLE DB 驅動程式只能使用 Visual Studio C++ 2012 或更新版本來編譯。  
  
### <a name="ole-db"></a>OLE DB  
 若要在 OLE DB 應用程式中使用 SQL Server 標頭檔的 OLE DB 驅動程式, 請使用下列程式程式碼:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果應用程式具有 sqloledb 的**include**語句, 內含 msoledbsql.h 的**include**語句就必須在它之後。  
  
 透過 SQL Server 的 OLE DB 驅動程式來建立資料來源的連接時, 請使用 "內含 MSOLEDBSQL.H" 做為提供者名稱字串。  

  
## <a name="component-names-and-properties-by-version"></a>依版本排列的元件名稱和屬性  

|屬性|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 標頭檔名稱|msoledbsql.h|Sqloledb.h|  
|OLE DB 提供者 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>靜態連結與 BCP 函數  
 當應用程式使用 BCP 函數時，應用程式最好在連接字串中指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  
  
 如需詳細資訊, 請參閱執行[大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
