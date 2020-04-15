---
title: 執行語句 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305739"
---
# <a name="executing-a-statement"></a>執行陳述式
執行敘述有四種方法,具體取決於資料庫引擎編譯(準備)報表以及定義語句的人員:  
  
-   **直接執行**應用程式定義 SQL 語句。 它在運行時以單個步驟準備和執行。  
  
-   **已準備好的執行**應用程式定義 SQL 語句。 它在運行時以單獨的步驟準備和執行。 語句可以準備一次,並多次執行。  
  
-   **程式**應用程式可以在開發時定義和編譯一個或多個 SQL 語句,並將這些語句存儲到數據源中作為過程。 該過程在運行時執行一次或多次。 應用程式可以使用目錄函數枚舉可用的存儲過程。  
  
-   **目錄功能**驅動程式編寫器創建返回預定義結果集的函數。 通常,此函數提交預定義的 SQL 語句或調用為此目的創建的過程。 該函數在運行時執行一次或多次。  
  
 特定語句(由其語句句柄標識)可以執行任意次數。 語句可以使用各種不同的 SQL 語句執行,也可以使用相同的 SQL 語句重複執行。 例如,以下代碼使用相同的語句句柄 (*hstmt1*) 來檢索和顯示 Sales 資料庫中的表。 然後,它重用此句柄以檢索用戶選擇的表中的列。  
  
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
  
 以下代碼顯示了如何使用單個句柄重複執行同一語句以從表中刪除行。  
  
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
  
 對於許多驅動程序來說,分配語句是一項昂貴的任務,因此以這種方式重用同一語句通常比釋放現有語句和分配新語句更有效。 在語句上創建結果集的應用程式在重新執行語句之前必須小心關閉結果集上的游標;有關詳細資訊,請參閱[關閉游標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 重用語句還強制應用程式避免某些驅動程式中一次處於活動狀態的語句數的限制。 "活動"的確切定義特定於驅動程式,但它通常是指已準備或執行但仍具有可用結果的任何語句。 例如,在編寫**INSERT**語句后,通常認為它處於活動狀態;因此,它通常被視為處於活動狀態。執行**SELECT**語句且游標仍處於打開狀態後,通常將其視為處於活動狀態;因此,該語句通常被視為處於活動狀態。在執行**CREATE TABLE**語句後,通常不將其視為活動。  
  
 應用程式透過使用SQL_MAX_CONCURRENT_ACTIVITIES選項呼叫**SQLGetInfo,** 確定一次在單個連接上可以處於活動狀態的語句數。 應用程式可以通過打開到數據源的多個連接來使用比此限制更活躍的語句;但是,由於連接可能非常昂貴,因此應考慮對性能的影響。  
  
 應用程式可以限制為語句分配的時間量,以便使用SQL_ATTR_QUERY_TIMEOUT語句屬性執行。 如果超時期限在數據源返回結果集之前過期,則執行 SQL 語句的函數將返回 SQLSTATE HYT00(超時已過期)。 預設是沒有逾時。  
  
 此章節包含下列主題。  
  
-   [直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [備妥的執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [程序](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [SQL 陳述式的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [執行目錄函式](../../../odbc/reference/develop-app/executing-catalog-functions.md)
