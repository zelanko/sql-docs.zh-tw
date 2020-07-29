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
ms.openlocfilehash: c88ef12d636dd5b10e1b7b3cd9418df3e058325b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007051"
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
