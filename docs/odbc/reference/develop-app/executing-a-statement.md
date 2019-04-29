---
title: 執行陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5660cfe2f264e0971d30cd2eaf1aadf68581321e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032816"
---
# <a name="executing-a-statement"></a>執行陳述式
有四種方法執行陳述式，在編譯 （預備） 資料庫引擎和使用者定義它們時，取決於：  
  
-   **直接執行**應用程式定義的 SQL 陳述式。 它是備妥，並以單一步驟的執行階段執行。  
  
-   **備妥的執行**應用程式定義的 SQL 陳述式。 它是備妥，並在個別步驟中的執行階段執行。 可以準備一次，多次執行陳述式。  
  
-   **程序**應用程式可以定義和編譯一個或多個 SQL 陳述式，在開發時間，並將這些陳述式儲存資料來源做為程序。 在執行階段的一或多次執行程序。 應用程式可以列舉可用以使用目錄函數的預存程序。  
  
-   **目錄函式**驅動程式寫入器會建立函式會傳回預先定義的結果集。 通常，此函式提交預先定義的 SQL 陳述式，或呼叫針對這個用途建立的程序。 在執行階段的一或多次時，會執行函式。  
  
 特定陳述式 （如其陳述式控制代碼所識別） 可以執行任何次數。 可以使用各種不同的 SQL 陳述式，執行陳述式，或它可以重複使用執行相同的 SQL 陳述式。 例如，下列程式碼會使用相同的陳述式控制代碼 (*hstmt1*) 來擷取並顯示 Sales 資料庫中的資料表。 然後重複使用此控點以擷取使用者所選取的資料表中的資料行。  
  
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
  
 此外，下列程式碼會示範如何使用單一的控制代碼來重複執行相同的陳述式，從資料表刪除資料列。  
  
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
  
 對於許多驅動程式配置陳述式會耗費資源的工作中，所以重複使用相同的陳述式，以這種方式是通常更有效率，比釋放現有的陳述式和配置新的。 建立結果集的陳述式的應用程式必須非常小心設定之前重新陳述式的結果時關閉資料指標如需詳細資訊，請參閱 <<c0> [ 關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重複使用陳述式時，也會強制應用程式，以避免在有些驅動程式，可同時處於作用中的陳述式的數目限制。 「 作用中 」 的確切定義驅動程式特有的但它通常是指已備妥或執行任何陳述式，而且仍然有可用的結果。 例如，在後**插入**已備妥陳述式，通常被視為作用; 之後**選取**在執行陳述式和資料指標仍開啟時，它通常會被視為作用中;之後**CREATE TABLE**在執行陳述式，則通常不視為為作用中。  
  
 應用程式可讓您判斷多少的陳述式可以藉由呼叫一次在單一連接上作用**SQLGetInfo** SQL_MAX_CONCURRENT_ACTIVITIES 選項。 應用程式可以開啟多個連接到資料來源; 使用超過此限制的更多作用中陳述式因為連接可能很昂貴，不過，應該考慮的效能影響。  
  
 應用程式可以限制針對 SQL_ATTR_QUERY_TIMEOUT 陳述式屬性情況下執行的陳述式所分配的時間量。 如果在逾時期限到期之前的資料來源傳回結果集，執行 SQL 陳述式的函式會傳回 SQLSTATE HYT00 （逾時過期）。 根據預設，沒有任何逾時。  
  
 此章節包含下列主題。  
  
-   [直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [備妥的執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [程序](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 陳述式的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [使用目錄函式](../../../odbc/reference/develop-app/executing-catalog-functions.md)
