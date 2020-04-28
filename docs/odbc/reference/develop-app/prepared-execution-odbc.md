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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 147ca85b21296575ff55afbe66ab286cc4824fae
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282308"
---
# <a name="prepared-execution-odbc"></a>備妥的執行 ODBC
備妥的執行是執行語句多次的有效方式。 語句會先編譯或*備*妥為存取計畫。 然後，稍後會執行一次或多次的存取計畫。 如需存取計畫的詳細資訊，請參閱[處理 SQL 語句](../../../odbc/reference/processing-a-sql-statement.md)。  
  
 垂直和自訂應用程式通常會使用備妥的執行，以重複執行相同、參數化的 SQL 語句。 例如，下列程式碼會準備語句，以更新不同部分的價格。 然後每次使用不同的參數值多次執行語句。  
  
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
  
 已備妥的執行速度比直接執行語句執行一次以上，主要是因為語句只編譯一次。直接執行的語句會在每次執行時進行編譯。 備妥的執行也可以減少網路流量，因為如果資料來源支援存取計畫識別碼，則每次執行語句時，驅動程式都可以將存取計畫識別碼傳送至資料來源，而不是整個 SQL 語句。  
  
 應用程式可以在準備好和執行語句之後，取得結果集的中繼資料。 不過，針對某些驅動程式傳回備妥的中繼資料，未執行語句的成本很高，因此可互通的應用程式應加以避免。 如需詳細資訊，請參閱[結果集中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 備妥的執行不應該用於單次執行的陳述式。 對於這類語句，它會比直接執行稍微慢一點，因為它需要額外的 ODBC 函式呼叫。  
  
> [!IMPORTANT]  
>  藉由明確呼叫**SQLEndTran**或在自動認可模式中作業來認可或回復交易，會導致某些資料來源刪除連接上所有語句的存取計畫。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 選項。  
  
 若要準備和執行語句，應用程式：  
  
1.  呼叫**SQLPrepare** ，並將包含 SQL 語句的字串傳遞給它。  
  
2.  設定任何參數的值。 在準備語句之前或之後，實際上可以設定參數。 如需詳細資訊，請參閱本節稍後的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
3.  會呼叫**SQLExecute** ，並執行任何必要的額外處理，例如提取資料。  
  
4.  視需要重複步驟2和3。  
  
5.  呼叫**SQLPrepare**時，驅動程式：  
  
    -   修改 SQL 語句，以使用資料來源的 SQL 文法，而不剖析語句。 這包括取代 ODBC 中的[Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中所討論的逸出序列。 應用程式可以藉由呼叫**SQLNativeSql**來捕獲 SQL 語句的修改形式。 如果已設定 SQL_ATTR_NOSCAN 語句屬性，則不會取代逸出序列。  
  
    -   將語句傳送到資料來源以進行準備。  
  
    -   儲存傳回的存取計畫識別碼以供稍後執行（如果準備成功），或傳回任何錯誤（如果準備失敗）。 錯誤包括語法錯誤，例如 SQLSTATE 42000 （語法錯誤或存取違規）和語意錯誤，例如 SQLSTATE 42S02 （找不到基表或 view）。  
  
        > [!NOTE]  
        >  有些驅動程式在此時不會傳回錯誤，而是在執行語句或呼叫目錄函式時傳回它們。 因此， **SQLPrepare**可能會在發生失敗時顯示為成功。  
  
6.  呼叫**SQLExecute**時，驅動程式：  
  
    -   抓取目前的參數值，並視需要加以轉換。 如需詳細資訊，請參閱本節稍後的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   將存取計畫識別碼和已轉換的參數值傳送至資料來源。  
  
    -   傳回任何錯誤。 這些通常是執行階段錯誤，例如 SQLSTATE 24000 （不正確資料指標狀態）。 不過，有些驅動程式會在此時傳回語法和語意錯誤。  
  
 如果資料來源不支援語句準備，驅動程式就必須將它模擬到可能的程度。 例如，當呼叫**SQLPrepare**時，驅動程式可能不會執行任何動作，然後在呼叫**SQLExecute**時直接執行語句。  
  
 如果資料來源在沒有執行的情況下支援語法檢查，驅動程式可能會提交語句，以便在呼叫**SQLPrepare**時進行檢查，並在呼叫**SQLExecute**時提交要執行的語句。  
  
 如果驅動程式無法模擬語句準備，它會在呼叫**SQLPrepare**時儲存語句，並在呼叫**SQLExecute**時提交它以供執行。  
  
 因為模擬語句的準備並不完美，所以**SQLExecute**可能會傳回**SQLPrepare**正常傳回的任何錯誤。
