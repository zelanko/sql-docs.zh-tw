---
description: 使用資料指標 (ODBC)
title: 使用 (ODBC) 的資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], how to topics
ms.assetid: c502736f-bca0-45c3-ae25-d2ad52d296bf
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4b8d8b297afe44f990b7d0fa685ffa4aff51accf
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867785"
---
# <a name="use-cursors-odbc"></a>使用資料指標 (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
### <a name="to-use-cursors"></a>使用資料指標  
  
1.  呼叫 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 來設定所需的資料指標屬性：  
  
     設定 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_CONCURRENCY 屬性 (這是慣用的選項)。  
  
     或者  
  
     設定 SQL_CURSOR_SCROLLABLE 和 SQL_CURSOR_SENSITIVITY 屬性。  
  
2.  使用 SQL_ATTR_ROW_ARRAY_SIZE 屬性呼叫 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) 來設定資料列集大小。  
  
3.  如果使用 WHERE CURRENT OF 子句完成定點更新，可以選擇呼叫 [SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md) 來設定資料指標名稱。  
  
4.  執行 SQL 陳述式。  
  
5.  如果使用 WHERE CURRENT OF 子句完成定點更新，而且資料指標名稱沒有隨步驟 3 中的 [SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md) 提供，可以選擇呼叫 [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) 來設定資料指標名稱。  
  
6.  呼叫 [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) 來取得資料列集中的資料行 (C) 數目。  
  
     使用資料行取向的繫結。  
  
     \- 或 -  
  
     使用資料列取向的繫結。  
  
7.  視需要，從資料指標提取資料列集。  
  
8.  呼叫 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 來判斷是否有其他結果集可用。  
  
    -   如果該函數傳回 SQL_SUCCESS，表示有其他可用的結果集。  
  
    -   如果該函數傳回 SQL_NO_DATA，表示沒有其他可用的結果集。  
  
    -   如果該函數傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR，請呼叫 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md) 來判斷是否可以使用來自 PRINT 或 RAISERROR 陳述式的輸出。  
  
     如果繫結陳述式參數用於預存程序的輸出參數或傳回值，請使用繫結參數緩衝區中目前可用的資料。  
  
     在使用繫結參數時，每個 [SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md) 或 [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md) 呼叫都會執行 SQL 陳述式 S 次，其中 S 是繫結參數陣列中的元素數。 這代表將要處理 S 個結果集，其中每個結果集都是由 SQL 陳述式的單一執行通常會傳回的結果集、輸出參數和傳回碼等所有項目而組成。  
  
     請注意，當結果集包含計算資料列時，每個計算資料列都可以提供為個別的結果集。 這些計算結果集會散佈在一般的資料列內，將一般的資料列分隔成多個結果集。  
  
9. 您可以選擇使用 SQL_UNBIND 呼叫 [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md)，以釋放任何繫結的資料行緩衝區。  
  
10. 如果有其他可用的結果集，請到步驟 6。  
  
     在步驟 9 中，呼叫部分處理之結果集上的 [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) 會清除結果集的其餘部分。 清除部分處理之結果集的另一個方式為，呼叫 [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md)。  
  
     您可以透過設定 SQL_ATTR_CURSOR_TYPE 和 SQL_ATTR_CONCURRENCY，或是設定 SQL_ATTR_CURSOR_SENSITIVITY 和 SQL_ATTR_CURSOR_SCROLLABLE，控制所使用的資料指標類型。 您不應該混合使用這兩種指定資料指標行為的方法。  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標的 how to 主題 &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
