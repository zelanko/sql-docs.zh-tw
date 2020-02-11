---
title: 執行語句 |Microsoft Docs
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
ms.openlocfilehash: d95226e9d895bf78e15176744f651b7e830a1a10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901348"
---
# <a name="executing-a-statement"></a>執行陳述式
有四種方式可以執行語句，視資料庫引擎編譯（準備）和定義它們的時間而定：  
  
-   **直接執行**應用程式會定義 SQL 語句。 它在執行時間是以單一步驟準備和執行。  
  
-   **備**妥的執行應用程式會定義 SQL 語句。 它會在執行時間以個別步驟進行準備和執行。 語句可以準備一次，並執行多次。  
  
-   **程式**應用程式可以在開發階段定義和編譯一或多個 SQL 語句，並將這些語句以程式形式儲存在資料來源上。 程式會在執行時間執行一次或多次。 應用程式可以使用目錄函數來列舉可用的預存程式。  
  
-   **目錄**函式驅動程式寫入器會建立一個函式，以傳回預先定義的結果集。 通常，此函式會提交預先定義的 SQL 語句，或呼叫針對此用途所建立的程式。 函數會在執行時間執行一次或多次。  
  
 特定的語句（由其語句控制碼識別）可以執行任何次數。 語句可以使用各種不同的 SQL 語句來執行，也可以使用相同的 SQL 語句重複執行。 例如，下列程式碼會使用相同的語句控制碼（*hstmt1*）來取出和顯示 Sales 資料庫中的資料表。 然後，它會重複使用此控制碼來抓取使用者所選取之資料表中的資料行。  
  
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
  
 下列程式碼會示範如何使用單一控制碼來重複執行相同的語句，以從資料表中刪除資料列。  
  
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
  
 對於許多驅動程式而言，配置語句是一項昂貴的工作，因此以這種方式重複使用相同的語句，通常比釋放現有的語句和配置新的語句更有效率。 在語句上建立結果集的應用程式必須在暫停語句之前，小心關閉結果集上的資料指標。如需詳細資訊，請參閱[關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重複使用語句也會強制應用程式避免在一次可以使用的語句數目的某些驅動程式中受到限制。 「作用中」的確切定義是驅動程式特有的，但通常是指已備妥或執行的任何語句，而且仍有可用的結果。 例如，在備妥**INSERT**語句之後，通常會將它視為作用中;在執行**SELECT**語句且資料指標仍然開啟之後，通常會被視為作用中;在執行**CREATE TABLE**語句之後，通常不會將它視為作用中。  
  
 應用程式會使用 SQL_MAX_CONCURRENT_ACTIVITIES 選項來呼叫**SQLGetInfo** ，以決定一次可以在單一連接上啟用多少個語句。 應用程式可以使用比此限制更多的作用中語句，方法是開啟資料來源的多個連接。但是連接可能會很耗費資源，因此應考慮對效能的影響。  
  
 應用程式可以使用 SQL_ATTR_QUERY_TIMEOUT 語句屬性，限制針對語句所配置的時間量。 如果在資料來源傳回結果集之前，超時期間過期，執行 SQL 語句的函式會傳回 SQLSTATE HYT00 （超時時間已過期）。 預設是沒有逾時。  
  
 此章節包含下列主題。  
  
-   [直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [備妥的執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [程序](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 陳述式的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [執行目錄函式](../../../odbc/reference/develop-app/executing-catalog-functions.md)
