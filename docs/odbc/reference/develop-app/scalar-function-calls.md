---
title: "純量函式呼叫 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3fb62d7c916584da7411f398f66a2acf134bfa24
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="scalar-function-calls"></a>純量函式呼叫
純量函數會傳回每個資料列的值。 比方說，絕對值純量函數會採用數字的資料行做為引數和傳回的資料行中的每個值的絕對值。 是逸出序列呼叫純量函式  
  
 **{fn***純量函數* **}**   
  
 其中*純量函數*是所列出的函數的其中一個[附錄 e： 純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。 如需純量函數逸出序列的詳細資訊，請參閱[純量函數逸出序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)附錄 c: SQL 文法中。  
  
 例如，下列 SQL 陳述式建立相同的結果集的大寫的客戶名稱。 第一個陳述式會使用逸出序列語法。 第二個陳述式使用 OS/2 的 Ingres 原生的語法，且不互通。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 應用程式可以混合使用原生語法的純量函數的呼叫和純量函式呼叫會使用 ODBC 語法。 例如，假設員工資料表中的名稱會儲存為姓氏、 逗號和名字。 下列 SQL 陳述式會建立 Employee 資料表中的員工姓氏的結果集。 該陳述式使用 ODBC 純量函數**SUBSTRING**和 SQL Server 純量函數**CHARINDEX**並且正確地將只能在 SQL Server 上執行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) – 1)} FROM Customers  
```  
  
 應用程式應使用的最大的互通性**轉換**純量函數，並確認純量函式的輸出所需的類型。 **轉換**函式將資料從一個 SQL 資料類型轉換成指定的 SQL 資料類型。 語法**轉換**函式  
  
 **轉換 (** *value_exp* **，** *data_type***)**  
  
 其中*value_exp*資料行名稱，另一個純量函數或常值的結果和*data_type*是符合關鍵字**#define**所使用的名稱SQL 資料類型識別項中所定義[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。 例如，下列 SQL 陳述式會使用**轉換**，確定函式的輸出**CURDATE**函式是日期，而不是時間戳記或字元資料：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 若要判斷資料來源所支援的純量函數，應用程式呼叫**SQLGetInfo** SQL_CONVERT_FUNCTIONS、 與 SQL_NUMERIC_FUNCTIONS、 SQL_STRING_FUNCTIONS、 SQL_SYSTEM_FUNCTIONS，SQL_TIMEDATE_函式的選項。 若要判斷哪些轉換作業都受到**轉換**函式，應用程式呼叫**SQLGetInfo**與任何一開頭 SQL_CONVERT 的選項。

