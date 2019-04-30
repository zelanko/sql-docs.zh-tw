---
title: 程序呼叫 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 775b48eb5a7f2089d65c6e9548a986b2f7b9bec7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63284581"
---
# <a name="procedure-calls"></a>程序呼叫
A*程序*是儲存在資料來源上的可執行物件。 通常，它是先行編譯的一或多個 SQL 陳述式。 是逸出序列呼叫程序  
  
 **{**[**？ =**]**呼叫** *程序名稱*[**(**[*參數*] [**，**[*參數*]]...**)**] **}**  
  
 何處*程序名稱*指定名稱的程序並*參數*指定程序參數。  
  
 如需詳細程序呼叫逸出序列的詳細資訊，請參閱[程序呼叫逸出序列](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md)附錄 c:SQL 文法。  
  
 程序可以有零或多個參數。 它也可以傳回的值，選擇性的參數標記所示 **？ =** 語法的開頭。 如果*參數*是輸入或輸入/輸出參數，它可以是常值或參數標記。 不過，互通的應用程式應該一律會使用參數標記，因為某些資料來源不接受常值的參數值。 如果*參數*是一個 output 參數，它必須是參數標記。 必須與繫結參數標記**SQLBindParameter**陳述式執行之前的程序呼叫。  
  
 輸入和輸入/輸出參數可以從程序呼叫省略。 如果程序會呼叫包含括號，但不含任何參數，例如 {呼叫*程序名稱*（)}，驅動程式會指示要使用第一個參數的預設值的資料來源。 如果此程序並沒有任何參數，這可能會造成程序失敗。 如果程序呼叫沒有括號，例如 {呼叫*程序名稱*}，驅動程式不會傳送任何參數值。  
  
 在程序呼叫中可以針對輸入和輸入/輸出參數指定常值。 例如，假設此程序**InsertOrder**有五個輸入參數。 下列呼叫來**InsertOrder**省略第一個參數、 第二個引數，請提供常值和參數標記用於第三、 第四個和第五個參數：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 請注意，是否省略參數，逗號分隔的其他參數必須仍會出現。 如果省略了輸入或輸入/輸出參數，程序就會使用參數的預設值。 若要指定之長度/指標緩衝區的值設定為輸入或輸入/輸出參數的預設值的另一種方式繫結至 SQL_DEFAULT_PARAM 的參數。  
  
 如果省略了輸入/輸出參數或常值提供給參數，此驅動程式會捨棄輸出值。 同樣地，如果省略了程序傳回值的參數標記，驅動程式就會捨棄傳回值。 最後，如果應用程式指定的程序傳回值參數不會傳回值，驅動程式會將繫結至參數之長度/指標緩衝區的值設定為 SQL_NULL_DATA。  
  
 假設在程序 PARTS_IN_ORDERS 建立結果集，其中包含一份包含幾個特定部分的訂單。 下列程式碼會呼叫此程序的組件編號 544:  
  
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
  
 若要判斷資料來源是否支援程序，應用程式會呼叫**SQLGetInfo** SQL_PROCEDURES 選項。  
  
 如需有關程序的詳細資訊，請參閱[程序](../../../odbc/reference/develop-app/procedures-odbc.md)。
