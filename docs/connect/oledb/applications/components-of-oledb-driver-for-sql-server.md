---
title: OLE DB Driver for SQL Server 的元件 | Microsoft Docs
description: OLE DB Driver for SQL Server 的元件
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5a5124519bd95ec02e93a007d9881ec80814cfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989325"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的元件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驅動程式包含下列元件:  

|元件|Description|  
|---------------|-----------------|  
|msoledbsql.dll|包含 SQL Server 功能之所有 OLE DB 驅動程式的動態連結程式庫 (DLL) 檔案。|  
|msoledbsqlr.rll|SQL Server 程式庫的 OLE DB 驅動程式隨附的資源檔。|   
|msoledbsql.h|SQL Server 標頭檔的 OLE DB 驅動程式, 其中包含使用 OLE DB 驅動程式進行 SQL Server 所需的所有新定義。 此標頭檔會取代 sqloledb 標頭檔。<br /><br /> 注意: 您可以在同一個程式中參考內含 msoledbsql.h 和 sqloledb, 只要先定義了 sqloledb. h 即可。|  
|msoledbsql.lib|直接呼叫屬於 SQL Server OLE DB 驅動程式一部分的[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)函數所需的程式庫檔案。<br /><br /> 注意：如果您在程式碼中參考 msoledbsql.lib 檔，必須確認 msoledbsql.dll 檔位於您的系統路徑，以及使用應用程式的使用者系統路徑。|  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
