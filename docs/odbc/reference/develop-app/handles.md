---
title: 處理 |Microsoft 文件
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
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 830c4b653af74097c59c9aff9e073267792a84b7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handles"></a>處理
控制代碼是不透明，32 位元值，識別特定的項目。在 ODBC 中，這個項目可以是環境、 連接、 陳述式或描述元。 當應用程式呼叫**SQLAllocHandle**、 驅動程式管理員或驅動程式會建立指定類型的新項目和其控制代碼傳回至應用程式。 更新版本的應用程式會使用控制代碼，以便識別該項目時呼叫 ODBC 函數。 驅動程式與驅動程式管理員使用控點來尋找相關項目資訊。  
  
 例如，下列程式碼會使用兩個陳述式控制代碼 (*hstmtOrder*和*hstmtLine*) 來識別用來建立結果集的銷售訂單和銷售訂單行號的陳述式。 稍後，它會使用這些控制代碼來識別哪一個結果集提取資料。  
  
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
  
 控點是有意義，才能建立它們; ODBC 元件也就是驅動程式管理員可以解譯驅動程式管理員控制代碼，並將驅動程式可以解譯它自己的控制代碼。  
  
 例如，假設上述範例中的驅動程式配置來儲存陳述式的相關資訊的結構，並傳回陳述式控制代碼與此結構的指標。 當應用程式呼叫**SQLPrepare**，它會通過的 SQL 陳述式，而且陳述式控制代碼用於銷售訂單行號。 驅動程式會將 SQL 陳述式傳送至資料來源，以準備好，並傳回存取計畫識別碼。 驅動程式會使用控制代碼來尋找要儲存這個識別項的結構。  
  
 稍後，當應用程式呼叫**SQLExecute**來產生特定的銷售訂單的行號的結果集，它會傳遞相同的控制代碼。 驅動程式會使用控制代碼從結構中擷取的存取權的計劃識別碼。 它會將識別碼傳送到資料來源，告訴它要執行的計劃。  
  
 ODBC 有兩個層級的控制代碼： 驅動程式管理員控制代碼和驅動程式的控制代碼。 呼叫 ODBC 函數，因為它會呼叫這些函式在驅動程式管理員時，應用程式使用驅動程式管理員控制代碼。 驅動程式管理員用來尋找對應的驅動程式控制代碼的這個控制代碼，並使用驅動程式的控制代碼，驅動程式中呼叫函數時。 如需如何使用驅動程式和驅動程式管理員控制代碼的範例，請參閱[連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有兩個層級的控制代碼是 ODBC 架構; 的成品在大部分情況下，不相關應用程式或驅動程式。 雖然通常是沒有理由，若要這樣做，以判斷驅動程式的控制代碼藉由呼叫應用程式可能會**SQLGetInfo**。  
  
 此章節包含下列主題。  
  
-   [環境控制代碼](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述項控制代碼](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [狀態轉換](../../../odbc/reference/develop-app/state-transitions.md)
