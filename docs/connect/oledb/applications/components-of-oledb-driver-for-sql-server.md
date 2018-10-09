---
title: Microsoft OLE DB Driver for SQL Server | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 164b87135257f812898c254fd7fd4f5c762c72ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735246"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 的元件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 包含下列元件：  

|元件|Description|  
|---------------|-----------------|  
|msoledbsql.dll|動態連結程式庫 (DLL) 檔案，其中包含所有的 OLE DB driver for SQL Server 功能。|  
|msoledbsqlr.rll|OLE DB driver for SQL Server 文件庫隨附的資源檔。|   
|msoledbsql.h|使用 OLE DB Driver for SQL Server 才能 OLE DB Driver for SQL Server 標頭檔，其中包含所有新的定義。 此標頭檔取代 sqloledb.h 標頭檔。<br /><br /> 注意： 您可以參考 msoledbsql.h 和 sqloledb.h 相同程式中的，只要先定義 sqloledb.h。|  
|msoledbsql.lib|需要直接呼叫的程式庫檔案[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)是 OLE DB Driver for SQL Server 的一部分的函式。<br /><br /> 如果您在程式碼中參考 sqlncli11.lib 檔，必須確認 sqlncli11.dll 檔位於您的系統路徑，以及使用應用程式之使用者的系統路徑。|  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
