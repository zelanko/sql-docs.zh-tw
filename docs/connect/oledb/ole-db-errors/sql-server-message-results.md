---
title: SQL Server 訊息結果 (OLE DB 驅動程式)
description: 了解不會產生 OLE DB Driver for SQL Server 資料列集或計數的 Transact-SQL 陳述式，以及其預期的傳回值。
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc3701313f920eead650435ca40538ad8a4b6ef0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862500"
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式不會產生 OLE DB Driver for SQL Server 資料列集或執行時受到影響之資料列的計數：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 成功執行後，OLE DB Driver for SQL Server 會傳回 S_OK，而且訊息可以提供給 OLE DB Driver for SQL Server 取用者使用。  
  
 OLE DB Driver for SQL Server 會傳回 S_OK，而且在執行許多 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式之後，或在取用者執行 OLE DB Driver for SQL Server 成員函式之後，會提供一或多個參考用訊息。  
  
OLE DB Driver for SQL Server 取用者可以動態指定查詢文字。 取用者應在_每次_執行成員函式後檢查錯誤介面。 無論傳回碼的值為何、是否傳回對 `IRowset` 或 `IMultipleResults` 的介面參考、受影響的資料列計數為何，都一律應執行這些檢查。
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
