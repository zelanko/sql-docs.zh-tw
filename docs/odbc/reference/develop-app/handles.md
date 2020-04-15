---
title: 手柄 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300208"
---
# <a name="handles"></a>處理
句柄是不透明的 32 位值,用於標識特定項;在 ODBC 中,此專案可以是環境、連接、語句或描述符。 當應用程式呼叫**SQLAllocHandle**時,驅動程式管理器或驅動程式將創建指定類型的新項,並將其句柄返回到應用程式。 應用程式稍後使用句柄在調用 ODBC 函數時識別該項。 驅動程式管理員和驅動程式使用句柄查找有關該專案的資訊。  
  
 例如,以下代碼使用兩個語句句柄 *(hstmtOrder 和* *hstmtLine)* 來標識要創建銷售訂單和銷售訂單行號的結果集的語句。 它稍後使用這些句柄來標識要從哪個結果集獲取數據。  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 句柄僅對創建句柄的 ODBC 元件有意義;也就是說,只有驅動程式管理器可以解釋驅動程式管理器句柄,只有驅動程式可以解釋其自己的句柄。  
  
 例如,假設前面的示例中的驅動程式分配一個結構來存儲有關語句的資訊,並將指向此結構的指標作為語句句柄返回。 當應用程式調用**SQLPrepare**時,它將傳遞一個 SQL 語句和用於銷售訂單行號的語句的句柄。 驅動程式將 SQL 語句發送到數據源,數據源會準備它並返回訪問計畫識別碼。 驅動程式使用句柄查找要存儲此標識符的結構。  
  
 稍後,當應用程式調用**SQLExecute**生成特定銷售訂單的結果行號集時,它將傳遞相同的句柄。 驅動程式使用句柄從結構中檢索訪問計劃標識符。 它將標識符發送到數據源,告訴它要執行哪個計畫。  
  
 ODBC 有兩個級別的句柄:驅動程式管理器句柄和驅動程式句柄。 應用程式在調用 ODBC 函數時使用驅動程式管理器句柄,因為它在驅動程式管理器中調用這些函數。 驅動程式管理員使用此句柄查找相應的驅動程式句柄,並在在驅動程式中調用函數時使用驅動程式句柄。 有關如何使用驅動程式和驅動程式管理器句柄的範例,請參閱[驅動程式管理員在連接過程中的角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有兩個級別的句柄是 ODBC 體系結構的工件;在大多數情況下,它與應用程式或驅動程序無關。 儘管通常沒有理由這樣做,但應用程式可以通過調用**SQLGetInfo**來確定驅動程式句柄。  
  
 此章節包含下列主題。  
  
-   [環境控制代碼](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [連線控制代碼](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述項控制代碼](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [狀態轉換](../../../odbc/reference/develop-app/state-transitions.md)
