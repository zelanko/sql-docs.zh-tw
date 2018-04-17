---
title: 使用 OLE DB 驅動程式的 SQL Server 標頭和程式庫檔案 |Microsoft 文件
description: 使用 SQL Server 標頭和程式庫檔案的 OLE DB 驅動程式
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 932a5c8d272bf975e4931326b96bea495e927a08
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用 OLE DB 驅動程式的 SQL Server 標頭和程式庫檔案
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在安裝程序期間選取 SQL Server SDK 選項，OLE DB 驅動程式時，會安裝 OLE DB 驅動程式的 SQL Server 標頭和程式庫檔案。 開發應用程式時，將開發所需的所有檔案複製並安裝到您的開發環境相當重要。 如需有關安裝及轉散發 SQL server 的 OLE DB 驅動程式的詳細資訊，請參閱[安裝 OLE DB 驅動程式的 SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 OLE DB 驅動程式的 SQL Server 標頭和程式庫檔案會安裝在下列位置：  
  
 *%PROGRAM FILES%*\Microsoft SQL Server\Client SDK\OLEDB\180\SDK  
  
 SQL Server 標頭檔 (msoledbsql.h) OLE DB 驅動程式可用來將 SQL Server 資料存取功能的 OLE DB 驅動程式新增到自訂應用程式。 SQL Server 標頭檔，OLE DB 驅動程式包含定義、 屬性、 屬性、 與充分利用新功能所需的介面中導入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。  
  
 OLE DB 驅動程式的 SQL Server 標頭檔，除了沒有也是匯出程式庫的 msoledbsql.lib 程式庫檔案的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]大量複製程式 (BCP) 功能。  
  
 SQL Server 標頭檔，OLE DB 驅動程式與 sqloledb.h 標頭檔使用的 Microsoft 資料存取元件 (MDAC)，向後相容，但是未包含 SQLOLEDB 的 Clsid (OLE DB 提供者[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]MDAC 隨附) 或符號的XML 功能 （這是驅動程式不支援 OLE DB for SQL Server）。    
  
 OLE DB 應用程式使用 SQL Server 的 OLE DB 驅動程式只需要參考 msoledbsql.h。 如果應用程式會使用 SQL Server 的 MDAC (SQLOLEDB) 和 OLE DB 驅動程式，則可以同時參考 sqloledb.h 和 msoledbsql.h，但必須先使用參考 sqloledb.h。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server 的標頭檔使用的 OLE DB 驅動程式  
 若要使用 SQL Server 標頭檔的 OLE DB 驅動程式，您必須使用**包含**您 C/c + + 程式碼內的陳述式。 下列章節說明如何執行此 OLE DB 應用程式。  
  
> [!NOTE]  
>  SQL Server 標頭和程式庫檔案，OLE DB 驅動程式只能是編譯使用 Visual Studio c + + 2012年或更新版本。  
  
### <a name="ole-db"></a>OLE DB  
 若要使用 OLE DB 驅動程式的 SQL Server OLE DB 應用程式中，使用下列幾行程式碼的標頭檔：  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果應用程式**包含**sqloledb.h，陳述式**包含**msoledbsql.h 陳述式必須緊跟在後。  
  
 在建立 OLE DB 驅動程式透過資料來源的連接適用於 SQL Server，使用"MSOLEDBSQL"當做提供者名稱字串。  

  
## <a name="component-names-and-properties-by-version"></a>依版本排列的元件名稱和屬性  

|屬性|SQL Server 的 OLE DB 驅動程式|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 標頭檔名稱|msoledbsql.h|Sqloledb.h|  
|OLE DB 提供者 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>靜態連結與 BCP 函數  
 當應用程式使用 BCP 函數時，應用程式最好在連接字串中指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  
  
 如需詳細資訊，請參閱 < 執行[執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
