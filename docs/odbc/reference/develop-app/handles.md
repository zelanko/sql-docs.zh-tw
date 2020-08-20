---
description: 處理
title: 控制碼 |Microsoft Docs
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
ms.openlocfilehash: 6e9d2445dbbd676e8d48be519c1649d550fd89c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465760"
---
# <a name="handles"></a>處理
控制碼是可識別特定專案的不透明、32位值;在 ODBC 中，此專案可以是環境、連接、語句或描述項。 當應用程式呼叫 **SQLAllocHandle**時，驅動程式管理員或驅動程式會建立指定之類型的新專案，並將其控制碼傳回給應用程式。 應用程式稍後在呼叫 ODBC 函數時，會使用控制碼來識別該專案。 驅動程式管理員和驅動程式會使用此控制碼來找出專案的相關資訊。  
  
 例如，下列程式碼會使用兩個語句控制碼 (*hstmtOrder* 和 *hstmtLine*) 來識別要在其中建立銷售訂單和銷售訂單行號之結果集的語句。 稍後會使用這些控制碼來識別要從中提取資料的結果集。  
  
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
  
 控制碼只對建立它們的 ODBC 元件有意義;也就是說，只有驅動程式管理員可以解讀驅動程式管理員控制碼，而只有驅動程式可以解讀自己的控制碼。  
  
 例如，假設上述範例中的驅動程式配置了結構來儲存語句的相關資訊，並將指標傳回此結構作為語句控制碼。 當應用程式呼叫 **SQLPrepare**時，它會傳遞 SQL 語句以及用於銷售訂單行號之語句的控制碼。 驅動程式會將 SQL 語句傳送到資料來源，以準備它並傳回存取計畫識別碼。 驅動程式會使用控制碼來尋找要儲存此識別碼的結構。  
  
 稍後，當應用程式呼叫 **SQLExecute** 來產生特定銷售訂單的行號結果集時，它會傳遞相同的控制碼。 驅動程式會使用此控制碼，從結構中取出存取計畫識別碼。 它會將識別碼傳送給資料來源，以告訴它要執行的計畫。  
  
 ODBC 有兩種層級的控制碼：驅動程式管理員控制碼和驅動程式控制碼。 應用程式會在呼叫 ODBC 函數時使用驅動程式管理員控制碼，因為它會在驅動程式管理員中呼叫這些函數。 驅動程式管理員會使用此控制碼來尋找對應的驅動程式控制碼，並在驅動程式中呼叫函式時使用驅動程式控制碼。 如需如何使用驅動程式和驅動程式管理員處理的範例，請參閱 [連接程式中的驅動程式管理員角色](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)。  
  
 有兩個層級的控制碼是 ODBC 架構的構件;在大部分的情況下，它與應用程式或驅動程式無關。 雖然通常沒有理由這麼做，但應用程式可能會藉由呼叫 **SQLGetInfo**來判斷驅動程式控制碼。  
  
 此章節包含下列主題。  
  
-   [環境控制代碼](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [連線控制代碼](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [陳述式控制代碼](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [描述項控制代碼](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [狀態轉換](../../../odbc/reference/develop-app/state-transitions.md)
