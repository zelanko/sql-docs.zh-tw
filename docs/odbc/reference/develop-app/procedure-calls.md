---
title: 程式呼叫 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282228"
---
# <a name="procedure-calls"></a>程序呼叫
*過程*是存儲在數據源上的可執行物件。 通常，它是先行編譯的一或多個 SQL 陳述式。 呼叫過程的逸出序列是  
  
 **[****]****call**呼叫*過程名稱***,**[**[***參數*] ,*[* 參數 ] , 參數 * ...**)**]**}**  
  
 其中*過程名稱*指定過程的名稱,*參數*指定過程參數。  
  
 有關過程調用轉義序列的詳細資訊,請參閱附錄 C 中[的過程呼叫轉義序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md):SQL 語法。  
  
 程序可以有零或多個參數。 它還可以返回一個值,如語法開頭的可選參數標記 **?*** 所示。 如果*參數*是輸入參數或輸入/輸出參數,則可以是文本或參數標記。 但是,可互操作的應用程式應始終使用參數標記,因為某些數據源不接受文本參數值。 如果*參數*是輸出參數,則它必須是參數標記。 在執行過程呼叫語句之前,必須使用**SQLBind 參數**綁定參數標記。  
  
 輸入和輸入/輸出參數可以從程序呼叫省略。 如果使用括弧調用過程,但沒有任何參數(如 [調用*過程名稱*()]),則驅動程式指示數據源對第一個參數使用預設值。 如果過程沒有任何參數,則可能導致該過程失敗。 如果調用過程時沒有括弧(如 [調用*過程名稱*]),則驅動程式不會發送任何參數值。  
  
 在程序呼叫中可以針對輸入和輸入/輸出參數指定常值。 例如,假設過程**InsertOrder**有五個輸入參數。 以下對**InsertOrder**的呼叫省略了第一個參數,為第二個參數提供了文本,並使用參數標記進行第三個、第四個和第五個參數:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 請注意,如果省略了參數,則仍必須顯示從其他參數分隔它的逗號。 如果省略了輸入或輸入/輸出參數，程序就會使用參數的預設值。 指定輸入或輸入/輸出參數的預設值的另一種方法是將綁定到參數的長度/指示器緩衝區的值設置為SQL_DEFAULT_PARAM。  
  
 如果省略輸入/輸出參數,或者為該參數提供了文本,則驅動程式將丟棄輸出值。 同樣地，如果省略了程序傳回值的參數標記，驅動程式就會捨棄傳回值。 最後，如果應用程式指定的程序傳回值參數不會傳回值，驅動程式會將繫結至參數之長度/指標緩衝區的值設定為 SQL_NULL_DATA。  
  
 假設過程PARTS_IN_ORDERS創建一個包含特定零件號的訂單清單的結果集。 以下代碼呼叫零件號 544 的過程:  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 要確定資料來源是否支援過程,應用程式使用SQL_PROCEDURES選項呼叫**SQLGetInfo。**  
  
 有關過程的詳細資訊,請參閱[過程](../../../odbc/reference/develop-app/procedures-odbc.md)。
