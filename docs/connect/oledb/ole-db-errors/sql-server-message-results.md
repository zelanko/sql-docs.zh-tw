---
title: SQL Server 訊息結果 |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 9098994ac5349fa9747c952e66eb902231956a5c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802850"
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
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 在成功執行時，OLE DB Driver for SQL Server 傳回 S_OK，而且訊息可以提供給 OLE DB Driver for SQL Server 取用者。  
  
 OLE DB Driver for SQL Server 會傳回 S_OK，且一或多個參考用訊息可取得在執行許多[!INCLUDE[tsql](../../../includes/tsql-md.md)]陳述式或取用者執行的 OLE DB Driver for SQL Server 成員函式。  
  
 每個成員函數執行之後，不管傳回碼的值為何、傳回的 **IRowset** 或 **IMultipleResults** 介面參考是否存在，或者受影響的資料列計數為何，允許動態指定查詢文字的 OLE DB Driver for SQL Server 取用者都應該會檢查錯誤介面。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../oledb/ole-db-errors/errors.md)  
  
  
