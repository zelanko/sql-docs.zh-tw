---
title: 純量函式呼叫 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897752"
---
# <a name="scalar-function-calls"></a>純量函式呼叫
純量函數會傳回每個資料列的值。 比方說，絕對值的純量函式會採用數值的資料行，做為引數，並傳回資料行中的每個值的絕對值。 呼叫純量函式逸出序列是  
  
 **{fn**  _scalar-function_ **}**  
  
 何處*純量函數*是其中一個函式中所列[附錄 e:純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 如需純量函式逸出序列的詳細資訊，請參閱[純量函式逸出序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)附錄 c:SQL 文法。  
  
 例如，下列 SQL 陳述式建立相同的結果集的大寫的客戶名稱。 第一個陳述式會使用逸出序列的語法。 第二個陳述式使用原生的語法來 Ingres OS/2，且不具互通性。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 應用程式可以混合使用原生的語法的純量函式呼叫和使用 ODBC 語法的純量函式的呼叫。 例如，假設員工資料表中的名稱會儲存為姓氏、 逗號和名字。 下列 SQL 陳述式建立結果集的員工姓氏的 Employee 資料表中。 陳述式使用 ODBC 純量函式**SUBSTRING**和 SQL Server 純量函式**CHARINDEX**和將 SQL 伺服器上才會正確執行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 應用程式應該使用的最大的互通性**轉換**純量函式，並確認純量函式的輸出所需的類型。 **轉換**函式將資料從一個 SQL 資料類型轉換成指定的 SQL 資料型別。 語法**轉換**函式  
  
 **CONVERT(** _value_exp_ **,** _data_type_ **)**  
  
 其中*value_exp*資料行名稱，另一個純量函式或常值，結果並*data_type*符合關鍵字 **#define**所使用的名稱SQL 資料類型識別項中定義[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。 例如，下列 SQL 陳述式會使用**轉換**並確定函式的輸出**CURDATE**函式是日期類型，而不是時間戳記或字元資料：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 若要判斷資料來源所支援的純量函式，呼叫應用程式**SQLGetInfo** SQL_CONVERT_FUNCTIONS、 與 SQL_NUMERIC_FUNCTIONS、 SQL_STRING_FUNCTIONS、 SQL_SYSTEM_FUNCTIONS，SQL_TIMEDATE_函式的選項。 若要判斷哪些轉換作業都受到**轉換**函式應用程式會呼叫**SQLGetInfo**搭配任何開頭 SQL_CONVERT 選項。
