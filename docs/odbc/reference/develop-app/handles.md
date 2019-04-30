---
title: 處理 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a205a23c4c7e7e45269fd00fc0923d4168ec7091
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061437"
---
# <a name="handles"></a>處理
控點是不透明，32 位元的值，識別特定的項目;在 ODBC 中，此項目可以是環境、 連接、 陳述式或描述元。 當應用程式呼叫**SQLAllocHandle**、 驅動程式管理員] 或 [驅動程式會建立指定型別的新項目和其控制代碼傳回應用程式。 稍後在應用程式會使用控制代碼呼叫 ODBC 函數時，找出該項目。 驅動程式與驅動程式管理員使用控點來尋找相關項目資訊。  
  
 例如，下列程式碼會使用兩個陳述式控制代碼 (*hstmtOrder*並*hstmtLine*) 來識別要在其中建立結果集的銷售訂單與銷售訂單行號的陳述式。 稍後，它會使用這些控制代碼來識別哪一個結果集擷取的資料。  
  
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
  
 控點是有意義，才能建立; ODBC 元件也就是說，驅動程式管理員可以解譯驅動程式管理員控制代碼，而且驅動程式可以解譯它自己的控制代碼。  
  
 例如，假設上述範例中的驅動程式配置來儲存陳述式的相關資訊的結構，並傳回陳述式控制代碼與此結構的指標。 當應用程式呼叫**SQLPrepare**，它會通過的 SQL 陳述式，而且陳述式控制代碼用於銷售訂單的行號。 驅動程式會將 SQL 陳述式傳送到資料來源，準備好，並傳回存取計劃識別碼。 驅動程式會使用控制代碼來尋找要儲存此識別項的結構。  
  
 稍後，當應用程式會呼叫**SQLExecute**來產生特定的銷售訂單的行號的結果集，它會傳遞相同的控制代碼。 驅動程式會使用控制代碼從結構中擷取的存取 」 計劃識別碼。 它會將識別碼傳送至資料來源，告訴它這還打算執行。  
  
 ODBC 有兩個層級的控制代碼：驅動程式管理員控制代碼和驅動程式的控制代碼。 呼叫 ODBC 函數，因為它在驅動程式管理員會呼叫這些函式時，應用程式會使用驅動程式管理員控制代碼。 驅動程式管理員會使用此控制代碼來尋找對應的驅動程式控制代碼，並使用驅動程式的控制代碼，驅動程式中呼叫函數時。 如需驅動程式和驅動程式管理員控制代碼的使用方式的範例，請參閱 <<c0> [ 在連線程序中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有兩個層級的控制代碼是 ODBC 架構; 的成品在大部分情況下，不相關應用程式或驅動程式。 雖然通常是沒有理由這麼做，就可以判斷驅動程式的控制代碼藉由呼叫應用程式**SQLGetInfo**。  
  
 此章節包含下列主題。  
  
-   [環境控制代碼](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [連接控制代碼](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述項控制代碼](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [狀態轉換](../../../odbc/reference/develop-app/state-transitions.md)
