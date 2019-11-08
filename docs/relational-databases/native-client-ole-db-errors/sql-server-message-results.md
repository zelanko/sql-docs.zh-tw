---
title: SQL Server 訊息結果 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3383dcd08ed5910d949608e521b3cd23f37aace8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790158"
---
# <a name="sql-server-message-results"></a>SQL Server 訊息結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句不會在執行時產生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者資料列集或受影響的資料列計數：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 成功執行時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 S_OK，而且訊息可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者使用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回 S_OK，而且在執行許多 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句或取用者執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者成員函式之後，會有一或多個參考訊息可供使用。  
  
 允許動態指定查詢文字的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者取用者應該在每個成員函式執行後檢查錯誤介面，而不論傳回碼的值為何、IRowset 是否存在。或**IMultipleResults**介面參考，或受影響的資料列計數。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
