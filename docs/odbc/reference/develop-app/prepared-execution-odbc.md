---
title: 備妥的執行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prepared execution [ODBC]
- SQL statements [ODBC], prepared execution
- SQL statements [ODBC], executing
ms.assetid: f08c8a98-31ee-48b2-9dbf-6f31c2166dbb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c7bd6bc8281dd6bdc3bcfbd437380b2d5269ee43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199108"
---
# <a name="prepared-execution-odbc"></a>備妥的執行 ODBC
備妥的執行是有效的方式來執行陳述式一次以上。 第一次編譯的陳述式，或是*備妥，* 到存取計畫。 然後執行一或多次稍後存取計劃。 如需有關存取計劃的詳細資訊，請參閱[處理 SQL 陳述式](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 備妥的執行常用的垂直和自訂應用程式重複執行相同且參數化 SQL 陳述式。 例如，下列程式碼會準備陳述式來更新的不同部分的價格。 然後，它會執行的陳述式使用不同的參數值多次每一次。  
  
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
  
 備妥的執行速度比直接執行陳述式執行一次以上，主要是因為一次; 編譯的陳述式直接執行陳述式會編譯每次執行。 備妥的執行也可以提供網路流量減少因為驅動程式可以存取計劃識別碼與資料來源，每次傳送陳述式執行時，而不是完整的 SQL 陳述式，如果資料來源支援存取方案識別碼。  
  
 應用程式可以擷取的結果集準備陳述式之後，會在執行之前的中繼資料。 不過，備妥的情況下傳回的中繼資料，未執行的陳述式會耗用一些驅動程式而且應該盡可能避免互通的應用程式。 如需詳細資訊，請參閱 <<c0> [ 結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 備妥的執行不應該用於單次執行的陳述式。 對於這類陳述式，它是比直接執行稍微慢一點因為它需要額外的 ODBC 函式呼叫。  
  
> [!IMPORTANT]  
>  認可或回復交易，藉由明確呼叫**SQLEndTran**或藉由使用在自動認可模式下，會導致某些資料來源，若要刪除的連接上所有陳述式的存取方案。 如需詳細資訊，請參閱 「 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。  
  
 若要準備及執行陳述式時，應用程式：  
  
1.  呼叫**SQLPrepare**並將它傳遞為字串，包含 SQL 陳述式。  
  
2.  設定任何參數的值。 預備此陳述式的前後，實際上可以設定參數。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
3.  呼叫**SQLExecute** ，然後在執行任何額外的處理所需的資源，例如擷取資料。  
  
4.  視需要重複步驟 2 和 3。  
  
5.  當**SQLPrepare**呼叫時，驅動程式：  
  
    -   修改 SQL 陳述式，而不剖析陳述式中使用資料來源的 SQL 文法。 這包括取代中所討論的逸出序列[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 應用程式可以藉由呼叫擷取的 SQL 陳述式修改後的表單**SQLNativeSql**。 如果 SQL_ATTR_NOSCAN 陳述式屬性設定，不會取代逸出序列。  
  
    -   陳述式傳送到資料來源進行準備。  
  
    -   傳回的存取計劃會將識別碼儲存供稍後執行 （如果準備成功） 或 （如果準備失敗） 傳回的任何錯誤。 錯誤包含語法錯誤，例如 SQLSTATE 42000 （語法錯誤或存取違規） 和語意錯誤，例如 SQLSTATE 42S02 （基底資料表或檢視找不到）。  
  
        > [!NOTE]  
        >  有些驅動程式不要在此時傳回錯誤，但改為傳回它們，或呼叫目錄函式時執行的陳述式。 因此， **SQLPrepare**似乎事實上它失敗時成功。  
  
6.  當**SQLExecute**呼叫時，驅動程式：  
  
    -   擷取目前的參數值，並將它們轉換為必要。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   將存取計劃識別碼和已轉換的參數值傳送至資料來源。  
  
    -   會傳回任何錯誤。 這些是一般的執行階段錯誤例如 SQLSTATE 24000 （無效的資料指標狀態）。 不過，有些驅動程式會傳回語法和語意錯誤此時。  
  
 如果資料來源不支援陳述式準備，驅動程式必須模擬它的範圍。 例如，驅動程式可能會執行任何動作時**SQLPrepare**呼叫，然後再執行直接執行陳述式時**SQLExecute**呼叫。  
  
 如果資料來源支援的語法而不會執行檢查，驅動程式可能會提交的陳述式檢查何時**SQLPrepare**呼叫，並提交執行的陳述式時**SQLExecute**是呼叫。  
  
 如果驅動程式無法模擬陳述式準備，它會儲存在陳述式時**SQLPrepare**呼叫，並將它提交執行時**SQLExecute**呼叫。  
  
 模擬的陳述式準備並不完美，因為**SQLExecute**可能會傳回任何錯誤，通常由**SQLPrepare**。
