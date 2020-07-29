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
ms.openlocfilehash: ecb2b323a9acb84c2c7a53b28653e81ef65ea23b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006991"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>使用 OLE DB Driver for SQL Server 標頭及程式庫檔案
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  在安裝程序期間選取 OLE DB Driver for SQL Server SDK 選項時，會安裝 OLE DB Driver for SQL Server 標頭檔與程式庫檔案。 開發應用程式時，將開發所需的所有檔案複製並安裝到您的開發環境相當重要。 如需有關安裝和轉散發 OLE DB Driver for SQL Server 的詳細資訊，請參閱[安裝 OLE DB Driver for SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md)。  
  
 OLE DB Driver for SQL Server 標頭檔和程式庫檔案會安裝到下列位置：  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 OLE DB Driver for SQL Server 標頭檔 (msoledbsql.h) 可以用來將 OLE DB Driver for SQL Server 資料存取功能新增至您的自訂應用程式。 OLE DB Driver for SQL Server 標頭檔包含使用 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中所導入之新功能所需的所有定義、屬性 (Attribute)、屬性 (Property) 與介面。  
  
 除了 OLE DB Driver for SQL Server 標頭檔之外，還有一個 msoledbsql.lib 程式庫檔案，也就是 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 功能的匯出程式庫。  
  
 OLE DB Driver for SQL Server 標頭檔與搭配 Microsoft Data Access Components (MDAC) 所使用的 sqloledb.h 標頭檔具回溯相容性，但是不包含適用於 SQLOLEDB 的 CLSID (MDAC 隨附的 OLE DB Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) 或適用於 XML 功能的符號 (不受 OLE DB Driver for SQL Server 所支援)。    
  
 使用 OLE DB Driver for SQL Server 的 OLE DB 應用程式只需要參考 msoledbsql.h。 如果應用程式同時使用 MDAC (SQLOLEDB) 和 OLE DB Driver for SQL Server，則可以同時參考 sqloledb.h 和 msoledbsql.h，但是必須先參考 sqloledb.h。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>使用 OLE DB Driver for SQL Server 標頭檔  
 若要使用 OLE DB Driver for SQL Server 標頭檔，您必須在 C/C++ 程式碼中使用 **include** 陳述式。 下列各節描述如何在 OLE DB 應用程式中執行該動作。  
  
> [!NOTE]  
>  OLE DB Driver for SQL Server 標頭檔和程式庫檔案僅能使用 Visual Studio C++ 2012 或更新版本編譯。  
  
### <a name="ole-db"></a>OLE DB  
 透過下列幾行程式碼，在 OLE DB 應用程式中使用 OLE DB Driver for SQL Server 標頭檔：  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  如果應用程式有適用於 sqloledb.h 的 **include** 陳述式，適用於 msoledbsql.h 的 **include** 陳述式必須緊跟在後。  
  
 透過 OLE DB Driver for SQL Server 建立資料來源的連接時，請使用 "SQLNCLI11" 作為提供者名稱字串。  

  
## <a name="component-names-and-properties-by-version"></a>依版本排列的元件名稱和屬性  

|屬性|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB 標頭檔名稱|msoledbsql.h|Sqloledb.h|  
|OLE DB 提供者 DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>靜態連結與 BCP 函數  
 當應用程式使用 BCP 函數時，應用程式最好在連接字串中指定用來編譯應用程式之標頭檔與程式庫隨附相同版本的驅動程式。  
  
 如需詳細資訊，請參閱[執行大量複製作業](../../oledb/features/performing-bulk-copy-operations.md)。  
  
## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
