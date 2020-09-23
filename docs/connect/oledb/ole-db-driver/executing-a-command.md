---
title: 執行命令 (OLE DB 驅動程式) | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 中的取用者如何藉由建立工作階段、取得資料列集，然後使用 Execute 來執行命令。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- commands [OLE DB Driver for SQL Server]
- OLE DB, executing commands
- sessions [OLE DB Driver for SQL Server]
- OLE DB extensions for XML
- OLE DB Driver for SQL Server, command execution
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f24216ec62b77c56d5d2b18563f64e37fd4b7691
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861522"
---
# <a name="executing-a-command"></a>執行命令
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  建立資料來源的連接後，取用者會呼叫 **IDBCreateSession::CreateSession** 方法來建立工作階段。 此工作階段會當做命令、資料列集或交易 Factory 運作。  
  
 若要直接使用個別的資料表或索引，取用者會要求 **IOpenRowset** 介面。 **IOpenRowset::OpenRowset** 方法會從單一基底資料表或索引開啟並傳回包含所有資料列的資料列集。  
  
 若要執行命令 (例如 SELECT \* FROM Authors)，取用者會要求 **IDBCreateCommand** 介面。 取用者可以執行 **IDBCreateCommand::CreateCommand** 方法來建立命令物件，並要求 **ICommandText** 介面。 **ICommandText::SetCommandText** 方法可用於指定要執行的命令。  
  
 **Execute** 命令用於執行命令。 此命令可以是任何 SQL 陳述式或程序名稱。 並非所有命令都會產生結果集 (資料列集) 物件。 SELECT * FROM Authors 之類的命令會產生結果集。  
  
## <a name="see-also"></a>另請參閱  
 [建立 OLE DB Driver for SQL Server 應用程式](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)  
  
  
