---
title: 使用 OLE DB Driver for SQL Server 標頭及程式庫檔案 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 標頭及程式庫檔案
ms.custom: ''
ms.date: 06/12/2018
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
manager: craigg
ms.openlocfilehash: 9cd6a50bec611b7068b3f79f3867f9e2a6242a70
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816036"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用 OLE DB Driver for SQL Server 標頭及程式庫檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在安裝過程中選取 OLE DB Driver for SQL Server SDK 選項時，會安裝 OLE DB Driver for SQL Server 標頭和程式庫檔案。 開發應用程式時，將開發所需的所有檔案複製並安裝到您的開發環境相當重要。 如需有關安裝及轉散發 OLE DB Driver for SQL Server 的詳細資訊，請參閱 <<c0> [ 安裝 OLE DB Driver for SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 OLE DB Driver for SQL Server 標頭和程式庫檔案會安裝在下列位置：  
  
 *%PROGRAM FILES %* \Microsoft SQL Server\Client SDK\OLEDB\181\SDK  
  
 OLE DB Driver for SQL Server 標頭檔 (msoledbsql.h) 可用來將 SQL Server 資料存取功能的 OLE DB 驅動程式新增至自訂應用程式。 OLE DB Driver for SQL Server 標頭檔包含使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所導入之新功能所需的所有定義、屬性 (Attribute)、屬性 (Property) 與介面。  
  
 除了 OLE DB Driver for SQL Server 標頭檔，另外還有 msoledbsql.lib 的程式庫檔案的匯出程式庫即為[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)功能。  
  
 OLE DB Driver for SQL Server 標頭檔與搭配 Microsoft Data Access Components (MDAC) 所使用的 sqloledb.h 標頭檔具回溯相容性，但是不包含適用於 SQLOLEDB 的 CLSID (MDAC 隨附的 OLE DB Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 或適用於 XML 功能的符號 (不受 OLE DB Driver for SQL Server 所支援)。    
  
 使用 OLE DB Driver for SQL Server OLE DB 應用程式只需要參考 msoledbsql.h。 如果應用程式同時使用 MDAC (SQLOLEDB) 和 OLE DB Driver for SQL Server，則可以同時參考 sqloledb.h 和 msoledbsql.h，但是必須先參考 sqloledb.h。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>使用 OLE DB Driver for SQL Server 標頭檔案  
 若要使用 OLE DB Driver for SQL Server 標頭檔案，您必須使用**包括**您 C/c + + 程式碼內的陳述式。 下列各節說明如何執行此 OLE DB 應用程式。  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server 標頭和程式庫檔案只能是編譯使用 Visual Studio c + + 2012年或更新版本。  
  
### <a name="ole-db"></a>OLE DB  
 若要使用 OLE DB Driver for SQL Server OLE DB 應用程式，使用下列幾行程式碼中的標頭檔案：  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果應用程式**包括**sqloledb.h，陳述式**包含**msoledbsql.h 陳述式必須緊跟在後。  
  
 當建立 SQL Server 透過 OLE DB 驅動程式的資料來源的連接，請使用"MSOLEDBSQL"當做提供者名稱字串。  

  
## <a name="component-names-and-properties-by-version"></a>依版本排列的元件名稱和屬性  

|屬性|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 標頭檔名稱|msoledbsql.h|Sqloledb.h|  
|OLE DB 提供者 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>靜態連結與 BCP 函數  
 當應用程式使用 BCP 函數時，應用程式最好在連接字串中指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  
  
 如需詳細資訊，請參閱 < 執行[執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
