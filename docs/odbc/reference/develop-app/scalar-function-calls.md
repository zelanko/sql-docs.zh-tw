---
title: Scalar 函數呼叫 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304259"
---
# <a name="scalar-function-calls"></a>純量函式呼叫
Scalar 函數返回每行的值。 例如,絕對值標量函數將數位列作為參數,並返回列中每個值的絕對值。 呼叫標量函數的逸出序列是  
  
 **[fn**_標量函數_**]**    
  
 *其中標量函數*是附錄 E 中列出的函數之一[:Scalar 函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 有關標量函數轉義序列的詳細資訊,請參閱附錄 C 中的[Scalar 函數轉義序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md):SQL 語法。  
  
 例如,以下 SQL 語句創建大寫客戶名稱的相同結果集。 第一個語句使用轉義序列語法。 第二個語句使用 OS/2 的 Ingres 的本機語法,並且不可互通。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 應用程式可以混合對使用本機語法的標量函數的調用,以及對使用 ODBC 語法的標量函數的調用。 例如,假設"員工"表中的名稱存儲為姓氏、逗號和名字。 以下 SQL 語句在「員工」表中創建一組員工姓氏的結果。 該語句使用 ODBC 標量函數**SUBSTRING**和 SQL Server 標量函數**CHARINDEX,** 並且僅在 SQL Server 上正確執行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 為了達到最大的互操作性,應用程式應使用**CONVERT**標量函數來確保標量函數的輸出是所需的類型。 **CONVERT**函數將數據從一種 SQL 資料類型轉換為指定的 SQL 資料類型。 **CONVERT**函數的語法是  
  
 **轉換(value_exp** _value_exp_ **,** _data_type_**)**  
  
 其中*value_exp*是列名、另一個標量函數的結果或文本值,並且*data_type*是一個關鍵字,與[附錄 D:數據類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)定義中的 SQL 數據類型標識符使用的 **#define**名稱匹配。 例如,以下 SQL 語句使用**CONVERT**函數來確保**CURDATE**函數的輸出是日期,而不是時間戳或字元資料:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 要確定資料來源支援哪些標量函數,應用程式使用SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS和SQL_TIMEDATE_FUNCTIONS選項調用**SQLGetInfo。** 要確定哪些轉換操作受**CONVERT**函數支援,應用程式將**SQLGetInfo**呼叫,並帶有以SQL_CONVERT開頭的任何選項。
