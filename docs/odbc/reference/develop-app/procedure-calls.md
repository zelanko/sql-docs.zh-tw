---
title: 程序呼叫 |Microsoft 文件
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
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6327ef340fe5fbd712ad9237bb6749d20bbd69af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="procedure-calls"></a>程序呼叫
A*程序*是儲存在資料來源上的可執行物件。 通常，它是先行編譯的一或多個 SQL 陳述式。 是逸出序列呼叫程序  
  
 **{**[**？ =**]**呼叫***程序名稱*[**(**[*參數*] [**，**[*參數*]]...**)**]**}**  
  
 其中*程序名稱*指定程序的名稱和*參數*指定程序參數。  
  
 如需程序呼叫逸出序列的詳細資訊，請參閱[程序呼叫的逸出序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)附錄 c: SQL 文法中。  
  
 程序可以有零或多個參數。 它也可以傳回值，選擇性的參數標記所示**？ =** 語法的開頭。 如果*參數*是輸入參數或輸入/輸出參數，它可以是常值或參數標記。 不過，因為某些資料來源不接受常值的參數值可互通的應用程式應該一律使用參數標記。 如果*參數*是一個 output 參數，它必須是參數標記。 必須與參數標記繫結**SQLBindParameter**陳述式執行之前的程序呼叫。  
  
 輸入和輸入/輸出參數可以從程序呼叫省略。 如果程序會呼叫包含括號，但不含任何參數，例如 {呼叫*程序名稱*（)}，驅動程式會指示要使用第一個參數的預設值的資料來源。 如果程序並沒有任何參數，這可能會導致程序失敗。 如果程序呼叫沒有括號，例如 {呼叫*程序名稱*}，驅動程式不會傳送任何參數值。  
  
 在程序呼叫中可以針對輸入和輸入/輸出參數指定常值。 例如，假設此程序**InsertOrder**有五個輸入參數。 下列呼叫**InsertOrder**省略第一個參數、 常值提供第二個參數，並使用參數標記的第三、 第四個和第五個參數：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 請注意，是否省略參數，逗號分隔它與其他參數必須仍然會出現。 如果省略了輸入或輸入/輸出參數，程序就會使用參數的預設值。 另一種方式將指定之長度/指標緩衝區的值設定輸入或輸入/輸出參數的預設值繫結至為 SQL_DEFAULT_PARAM 參數。  
  
 如果省略了輸入/輸出參數或常值提供給參數，此驅動程式會捨棄的輸出值。 同樣地，如果省略了程序傳回值的參數標記，驅動程式就會捨棄傳回值。 最後，如果應用程式指定的程序傳回值參數不會傳回值，驅動程式會將繫結至參數之長度/指標緩衝區的值設定為 SQL_NULL_DATA。  
  
 假設 PARTS_IN_ORDERS 的程序建立結果集，其中包含一份包含特定零件編號的訂單。 下列程式碼會呼叫此程序的零件編號 544:  
  
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
  
 若要判斷資料來源是否支援程序，應用程式呼叫**SQLGetInfo** SQL_PROCEDURES 選項。  
  
 如需程序的詳細資訊，請參閱[程序](../../../odbc/reference/develop-app/procedures-odbc.md)。
