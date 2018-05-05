---
title: 備妥的執行 ODBC |Microsoft 文件
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
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e03123e34834033b4c53fb1eb5818f6c78def82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="prepared-execution-odbc"></a>備妥的執行 ODBC
備妥的執行是有效的方式執行的陳述式一次以上。 第一次編譯的陳述式，或*備妥，*成存取計畫。 就執行一或多次於稍後存取計劃。 如需存取計劃的詳細資訊，請參閱[處理 SQL 陳述式](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 垂直和自訂應用程式通常會使用備妥的執行來重複執行相同且參數化 SQL 陳述式。 例如，下列程式碼會準備陳述式來更新不同部分的價格。 接著，它會執行陳述式多次使用不同的參數值每次。  
  
```  
SQLREAL       Price;  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0, PriceInd = 0;  
  
// Prepare a statement to update salaries in the Employees table.  
SQLPrepare(hstmt, "UPDATE Parts SET Price = ? WHERE PartID = ?", SQL_NTS);  
  
// Bind Price to the parameter for the Price column and PartID to  
// the parameter for the PartID column.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &Price, 0, &PriceInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &PartID, 0, &PartIDInd);  
  
// Repeatedly execute the statement.  
while (GetPrice(&PartID, &Price)) {  
   SQLExecute(hstmt);  
}  
```  
  
 備妥的執行速度比直接執行陳述式執行一次以上，主要是因為陳述式會編譯一次。直接執行陳述式是在執行每次進行編譯。 備妥的執行也可以提供網路流量減少因為驅動程式可以傳送存取計劃識別碼至資料來源每次陳述式執行時，而非整個 SQL 陳述式，如果資料來源支援存取計畫識別碼。  
  
 應用程式可以擷取的結果集準備陳述式之後，會在執行之前的中繼資料。 不過，傳回的中繼資料已備妥，未執行的陳述式是高度耗費資源的部分驅動程式，應該盡可能避免互通的應用程式。 如需詳細資訊，請參閱[結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 備妥的執行不應該用於單次執行的陳述式。 這些陳述式，它是比直接執行稍微慢一點因為它需要額外的 ODBC 函數呼叫。  
  
> [!IMPORTANT]  
>  認可或回復交易，藉由明確地呼叫**SQLEndTran**或藉由使用自動認可模式中，會導致某些資料來源，若要刪除的連接上所有陳述式的存取計畫。 如需詳細資訊，請參閱 「 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。  
  
 若要準備並執行陳述式時，應用程式：  
  
1.  呼叫**SQLPrepare**並將其傳遞字串，包含 SQL 陳述式。  
  
2.  設定任何參數的值。 準備陳述式前後，實際上可以設定參數。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
3.  呼叫**SQLExecute** ，並且不是必要的例如將資料擷取的任何其他處理。  
  
4.  視需要重複步驟 2 和 3。  
  
5.  當**SQLPrepare**呼叫時，驅動程式：  
  
    -   修改 SQL 陳述式，而不剖析陳述式中使用資料來源的 SQL 文法。 這包括取代所述的逸出序列[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 應用程式可以藉由呼叫擷取 SQL 陳述式的已修改的表單**SQLNativeSql**。 若已設定 SQL_ATTR_NOSCAN 陳述式屬性，不會取代逸出序列。  
  
    -   將陳述式傳送到資料來源的準備。  
  
    -   傳回的存取計劃會將識別碼儲存供稍後執行 （如果準備成功） 或傳回任何錯誤 （如果準備失敗）。 錯誤包含語法錯誤，例如 SQLSTATE 42000 （語法錯誤或存取違規） 和語意錯誤，例如 SQLSTATE 42S02 （基底資料表或檢視表，找不到）。  
  
        > [!NOTE]  
        >  有些驅動程式不要在此時傳回錯誤，但改為執行陳述式或呼叫目錄函數時，傳回它們。 因此， **SQLPrepare**成功實際上它失敗時可能會出現。  
  
6.  當**SQLExecute**呼叫時，驅動程式：  
  
    -   擷取目前的參數值，並視需要進行轉換。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   將資料來源的存取計畫識別碼和已轉換的參數值。  
  
    -   傳回的任何錯誤。 這些是通常會將執行階段錯誤例如 SQLSTATE 24000 （無效的資料指標狀態）。 不過，有些驅動程式傳回語法和語意錯誤此時。  
  
 如果資料來源不支援陳述式準備，驅動程式必須模擬它的範圍。 例如，驅動程式可能會執行任何動作時**SQLPrepare**呼叫，然後執行 直接執行陳述式時**SQLExecute**呼叫。  
  
 如果資料來源支援語法檢查並未執行，此驅動程式可能會提交的陳述式檢查時**SQLPrepare**稱為並提交進行執行陳述式時**SQLExecute**是呼叫。  
  
 如果驅動程式無法模擬準備陳述式，則會儲存在陳述式時**SQLPrepare**呼叫，並將它提交執行時**SQLExecute**呼叫。  
  
 因為模擬的陳述式準備並不完美， **SQLExecute**可以傳回任何錯誤，通常由**SQLPrepare**。
