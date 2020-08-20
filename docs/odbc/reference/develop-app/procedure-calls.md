---
description: 程序呼叫
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed5da9bbe94bf1f508e1b94c17e81c7b0169f6e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465730"
---
# <a name="procedure-calls"></a>程序呼叫
程式 *是儲存* 在資料來源上的可執行物件。 通常，它是先行編譯的一或多個 SQL 陳述式。 呼叫程式的換用順序為  
  
 **{**[**？ =**]**呼叫***程式-名稱*[** (**[*參數*] [**，**[*參數*]] .。。**) **]**}**  
  
 where *程式名稱* 指定程式的名稱， *參數* 指定程式參數。  
  
 如需有關程序呼叫 escape 順序的詳細資訊，請參閱附錄 C： SQL 文法中的 [程序呼叫 Escape sequence](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) 。  
  
 程序可以有零或多個參數。 它也可以傳回值（如語法開頭的選擇性參數標記 **？ =** 所表示）。 如果 *參數* 是輸入或輸入/輸出參數，它可以是常值或參數標記。 不過，互通的應用程式應該一律使用參數標記，因為某些資料來源不接受常值參數值。 如果 *參數* 是輸出參數，則它必須是參數標記。 在執行程序呼叫語句之前，必須先使用 **SQLBindParameter** 來系結參數標記。  
  
 輸入和輸入/輸出參數可以從程序呼叫省略。 如果以括弧呼叫程式，但沒有任何參數，例如 {call *procedure-name* ( # A1}，驅動程式會指示資料來源使用第一個參數的預設值。 如果程式沒有任何參數，這可能會導致程式失敗。 如果呼叫的程式沒有括弧，例如 {call *procedure-name*}，驅動程式就不會傳送任何參數值。  
  
 在程序呼叫中可以針對輸入和輸入/輸出參數指定常值。 例如，假設程式 **InsertOrder** 有五個輸入參數。 下列 **InsertOrder** 呼叫會省略第一個參數，提供第二個參數的常值，並使用第三個、第四個和第五個參數的參數標記：  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 請注意，如果省略某個參數，則必須仍會顯示從其他參數分隔的逗號。 如果省略了輸入或輸入/輸出參數，程序就會使用參數的預設值。 另一種指定輸入或輸入/輸出參數預設值的方式，就是將系結至參數的長度/指標緩衝區值設定為 SQL_DEFAULT_PARAM。  
  
 如果省略輸入/輸出參數，或為參數提供常值，驅動程式會捨棄輸出值。 同樣地，如果省略了程序傳回值的參數標記，驅動程式就會捨棄傳回值。 最後，如果應用程式指定的程序傳回值參數不會傳回值，驅動程式會將繫結至參數之長度/指標緩衝區的值設定為 SQL_NULL_DATA。  
  
 假設 PARTS_IN_ORDERS 的程式會建立一個結果集，其中包含包含特定元件編號的訂單清單。 下列程式碼會針對元件編號544呼叫這個程式：  
  
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
  
 為了判斷資料來源是否支援程式，應用程式會使用 SQL_PROCEDURES 選項來呼叫 **SQLGetInfo** 。  
  
 如需有關程式的詳細資訊，請參閱 [程式](../../../odbc/reference/develop-app/procedures-odbc.md)。
