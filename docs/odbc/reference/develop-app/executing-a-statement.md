---
title: 執行陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c111620b2f06e7b2eacb159d7cf1c8817bd27c59
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912303"
---
# <a name="executing-a-statement"></a>執行陳述式
有四種方式執行的陳述式，在編譯 （預備） 資料庫引擎和使用者定義時，取決於：  
  
-   **直接執行**應用程式定義的 SQL 陳述式。 已備妥，並以單一步驟的執行階段執行。  
  
-   **備妥的執行**應用程式定義的 SQL 陳述式。 它是備妥，並在執行階段於個別的步驟執行。 可以準備一次，多次執行陳述式。  
  
-   **程序**應用程式可以定義和編譯一個或多個 SQL 陳述式，在開發時間和儲存資料來源做為程序上的這些陳述式。 在執行階段的一或多次執行程序。 應用程式可以列舉可用以使用目錄函數的預存程序。  
  
-   **目錄函數**驅動程式寫入器會建立函式會傳回預先定義的結果集。 通常，此函式提交預先定義的 SQL 陳述式，或呼叫針對這個用途建立的程序。 此函式會執行在執行階段的一或多次。  
  
 特定的陳述式 （如其陳述式控制代碼所識別） 可以執行任何次數。 陳述式可以執行各種不同的 SQL 陳述式，或其使用相同的 SQL 陳述式可以重複執行。 例如，下列程式碼會使用相同的陳述式控制代碼 (*hstmt1*) 擷取並顯示 Sales 資料庫中的資料表。 然後重複使用此控點以擷取使用者所選取的資料表中的資料行。  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 此外，下列程式碼將示範如何使用單一的控制代碼來重複執行相同的陳述式，從資料表刪除資料列。  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 對於許多驅動程式配置陳述式會高度耗費資源的工作，所以重複使用相同的陳述式，以這種方式是通常更有效率釋放現有的陳述式和配置新的。 必須小心關閉資料指標的結果集之前重新陳述式，透過建立陳述式的結果集的應用程式如需詳細資訊，請參閱[關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重複使用陳述式也會強迫應用程式，以避免每次最多可處於作用中的陳述式數目的部分驅動程式的限制。 「 作用中 」 的確切定義特定驅動程式，但它通常是指任何準備或執行的陳述式，而且仍然有可用的結果。 例如，在之後**插入**陳述式已備妥，通常被視為設為作用中; 之後**選取**在執行陳述式和資料指標仍開啟時，通常認定為為作用中。之後**CREATE TABLE**在執行陳述式，它通常不視為設為作用中。  
  
 應用程式會決定多少陳述式可以透過呼叫一次在單一連接上作用中**SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 選項。 應用程式可以使用更多使用中的陳述式超過此限制，藉由開啟多個連接至資料來源;因為連接可能會耗費資源，不過，應該考量的效能影響。  
  
 應用程式可以限制針對 sql_attr_query_timeout 時陳述式屬性情況下執行的陳述式所分配的時間量。 如果在逾時期限到期之前的資料來源會傳回結果集，執行 SQL 陳述式的函式會傳回 SQLSTATE HYT00 （逾時過期）。 根據預設，沒有無逾時。  
  
 此章節包含下列主題。  
  
-   [直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [備妥的執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [程序](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 陳述式的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [使用目錄函式](../../../odbc/reference/develop-app/executing-catalog-functions.md)
