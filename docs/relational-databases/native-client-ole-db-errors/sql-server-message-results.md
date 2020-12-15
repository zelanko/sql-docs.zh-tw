---
description: SQL Server Native Client 訊息結果
title: 'SQL Server 訊息結果 (Native Client OLE DB 提供者) '
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fe5f2711334f371831bc76d60b5b74ef6b9a417
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467629"
---
# <a name="sql-server-native-client-message-results"></a>SQL Server Native Client 訊息結果
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句不會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行時產生原生用戶端 OLE DB 提供者資料列集或受影響資料列的計數：  
  
-   PRINT  
  
-   具有 10 或更低嚴重性的 RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 這些陳述式會傳回一或多個參考用訊息，或使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 傳回參考用訊息來取代資料列集或計數結果。 在成功執行時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client OLE DB 提供者會傳回 S_OK，而且訊息可供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 提供者取用者使用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者會傳回 S_OK，而且在執行許多 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句或取用者 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 提供者成員函式的取用者時，會有一或多個參考用訊息可供使用。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]無論傳回碼的值為何、傳回的 **IRowset** 或 **IMultipleResults** 介面參考是否存在，或受影響的資料列計數為何，允許動態指定查詢文字的原生 OLE DB 用戶端，都應該在每個成員函式執行之後檢查錯誤介面。  
  
## <a name="see-also"></a>另請參閱  
 [錯誤](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
