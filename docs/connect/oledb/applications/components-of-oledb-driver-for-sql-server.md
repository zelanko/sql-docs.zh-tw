---
title: OLE DB Driver for SQL Server 的元件 | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 元件，包括包含驅動程式功能的程式庫、其他程式庫與標頭檔。
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa548f34701565a5fcfd836232544bc0ee1345f4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862058"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的元件
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 包含下列元件：  

|元件|描述|  
|---------------|-----------------|  
|msoledbsql.dll|動態連結程式庫 (DLL) 檔案，其中包含所有 OLE DB Driver for SQL Server 功能。|  
|msoledbsqlr.rll|隨附 OLE DB Driver for SQL Server 程式庫的資源檔。|   
|msoledbsql.h|OLE DB Driver for SQL Server 標頭檔，其中包含使用 OLE DB Driver for SQL Server 所需的所有新定義。 此標頭檔會取代 sqloledb.h 標頭檔。<br /><br /> 注意:只要先定義 sqloledb，您就可以在相同的程式中參考 msoledbsql.h 和 sqloledb.h。|  
|msoledbsql.lib|直接呼叫屬於 OLE DB Driver for SQL Server 一部分的 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 函式所需的程式庫檔案。<br /><br /> 注意:如果您在程式碼中參考 msoledbsql.lib 檔，必須確認 msoledbsql.dll 檔位於您的系統路徑，以及使用應用程式的使用者系統路徑。|  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
