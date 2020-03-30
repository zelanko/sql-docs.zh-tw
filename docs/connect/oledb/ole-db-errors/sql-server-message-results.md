---
title: SQL Server 訊息結果 | Microsoft Docs
description: SQL Server 訊息結果
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994916"
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式不會產生 OLE DB Driver for SQL Server 資料列集或執行時受到影響之資料列的計數：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 成功執行後，OLE DB Driver for SQL Server 會傳回 S_OK，而且訊息可以提供給 OLE DB Driver for SQL Server 取用者使用。  
  
 OLE DB Driver for SQL Server 會傳回 S_OK，而且在執行許多 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式之後，或在取用者執行 OLE DB Driver for SQL Server 成員函式之後，會提供一或多個參考用訊息。  
  
 每個成員函數執行之後，不管傳回碼的值為何、傳回的 **IRowset** 或 **IMultipleResults** 介面參考是否存在，或者受影響的資料列計數為何，允許動態指定查詢文字的 OLE DB Driver for SQL Server 取用者都應該會檢查錯誤介面。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
