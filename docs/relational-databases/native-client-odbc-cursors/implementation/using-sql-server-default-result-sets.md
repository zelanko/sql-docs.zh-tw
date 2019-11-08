---
title: 使用 SQL Server 預設結果集 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dfd3ef8ec56f458bb57b1898a1bf7212534b7af1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784483"
---
# <a name="using-sql-server-default-result-sets"></a>使用 QL Server 預設結果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  預設的 ODBC 資料指標屬性為：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 每當這些屬性設定為預設值時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式就會使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 預設結果集。 預設結果集可用於任何受到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援的 SQL 陳述式，而且是將整個結果集傳送到用戶端的最有效率的方法。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 引進了 multiple active result sets （MARS）的支援;應用程式現在每個連接都可以有一個以上的使用中預設結果集。 預設不會啟用 MARS。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前，預設結果集不能在相同連接上支援多個作用中陳述式。 在連接上執行 SQL 陳述式以後，伺服器要等到結果集中的所有資料列都已經處理過後，才能在該連接上接受來自用戶端的命令 (取消其餘結果集的要求除外)。 若要取消部分處理之結果集的其餘部分，請呼叫[SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)或[SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) ，並將*fOption*參數設定為 SQL_CLOSE。 若要完成部分處理的結果集，並測試另一個結果集是否存在，請呼叫[SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。 如果 ODBC 應用程式在預設結果集已完全處理之前，在連接控制碼上嘗試命令，則呼叫會產生 SQL_ERROR 而且**SQLGetDiagRec**的呼叫會傳回：  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>另請參閱  
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
