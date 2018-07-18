---
title: SQL Server 的 OLE DB 驅動程式的元件 |Microsoft 文件
description: 適用於 SQL Server 的 OLE DB 驅動程式的元件
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 78b72796de5aa4ac2fb9bc0793f98365b7d8281e
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/14/2018
ms.locfileid: "35611683"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>適用於 SQL Server 的 OLE DB 驅動程式的元件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 驅動程式的 SQL Server 包含下列元件：  

|元件|描述|  
|---------------|-----------------|  
|msoledbsql.dll|動態連結程式庫 (DLL) 檔案，其中包含所有 SQL Server 功能，OLE DB 驅動程式。|  
|msoledbsqlr.rll|SQL Server 文件庫，OLE DB 驅動程式隨附的資源檔。|   
|msoledbsql.h|若要使用 SQL Server 的 OLE DB 驅動程式，需要 SQL Server 包含的所有新定義的標頭檔，OLE DB 驅動程式。 此標頭檔會取代 sqloledb.h 標頭檔。<br /><br /> 注意： 您可以參考 msoledbsql.h 和 sqloledb.h 相同程式中的，只要先定義 sqloledb.h。|  
|msoledbsql.lib|需要直接呼叫的程式庫檔案[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)函式，是 SQL Server OLE DB 驅動程式的一部分。<br /><br /> 注意： 如果您在程式碼參考 msoledbsql.lib 檔案，您必須確定 msoledbsql.dll 檔案是在您的系統路徑，和之使用者的系統路徑中使用應用程式。|  

## <a name="see-also"></a>另請參閱  
 [利用 OLE DB Driver for SQL Server 建置](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
