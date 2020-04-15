---
title: 使用 SQL 伺服器預設結果集 |微軟文件
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08926660face8061abdf8352d0c4a84ad7e67f8a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305377"
---
# <a name="using-sql-server-default-result-sets"></a>使用 QL Server 預設結果集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  預設的 ODBC 資料指標屬性為：  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 每當這些屬性設定為其預設值時,[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本機用戶端 ODBC 驅動程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]將使用 默認結果集。 預設結果集可用於任何受到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支援的 SQL 陳述式，而且是將整個結果集傳送到用戶端的最有效率的方法。  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]引入了對多個活動結果集 (MARS) 的支援;應用程式現在可以每個連接具有多個活動預設結果集。 預設不會啟用 MARS。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前，預設結果集不能在相同連接上支援多個作用中陳述式。 在連接上執行 SQL 陳述式以後，伺服器要等到結果集中的所有資料列都已經處理過後，才能在該連接上接受來自用戶端的命令 (取消其餘結果集的要求除外)。 要取消部分處理的結果集的其餘部分,請調用[SQLCloseCursor 或](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) [SQLFreeStmt,fOption](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)參數*fOption*設置為SQL_CLOSE。 要完成部分處理的結果集並測試是否存在另一個結果集,請呼叫[SQLMoreResult](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。 如果 ODBC 應用程式在完全處理預設結果集之前嘗試對連接句柄執行命令,則呼叫將產生SQL_ERROR,並且對**SQLGetDiagRec**的呼叫將傳回:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>另請參閱  
 [如何實作資料指標](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
