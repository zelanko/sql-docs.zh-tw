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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304259"
---
# <a name="scalar-function-calls"></a>純量函式呼叫
純量函數會傳回每個資料列的值。 例如，絕對值純量函數會接受數值資料行做為引數，並傳回資料行中每個值的絕對值。 呼叫純量函數的轉義順序為  
  
 **{fn**純量_函數_ **}**    
  
 其中，純量函數是[附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函*式*中所列的其中一個函數。 如需純量函式 escape 序列的詳細資訊，請參閱附錄 C： SQL 文法中的純量[函數 Escape 序列](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md)。  
  
 例如，下列 SQL 語句會建立相同的大寫客戶名稱結果集。 第一個語句使用 escape 序列語法。 第二個語句會針對 OS/2 使用 Ingres 的原生語法，而且無法互通。  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 應用程式可以混用純量函式的呼叫，以使用原生語法和呼叫使用 ODBC 語法的純量函數。 例如，假設 Employee 資料表中的名稱是以姓氏、逗號和名字的名稱儲存。 下列 SQL 語句會在 Employee 資料表中建立員工姓氏的結果集。 語句使用 ODBC 純量函式**SUBSTRING**和 SQL Server 純量函數**CHARINDEX** ，而且只會在 SQL Server 上執行。  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 為了達到最大的互通性，應用程式應該使用**CONVERT**純量函數，以確保純量函數的輸出是必要的類型。 **CONVERT**函數會將資料從一個 sql 資料類型轉換成指定的 sql 資料類型。 **CONVERT**函數的語法為  
  
 **CONVERT （** _value_exp_ **，** _data_type_**）**  
  
 其中*value_exp*是資料行名稱、另一個純量函數的結果或常值，而*data_type*則是符合 SQL 資料類型識別碼所使用之 **#define**名稱的關鍵字，如[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)中所定義。 例如，下列 SQL 語句會使用**CONVERT**函式，確保**CURDATE**函數的輸出是日期，而不是時間戳記或字元資料：  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 為了判斷資料來源支援哪些純量函數，應用程式會使用 SQL_CONVERT_FUNCTIONS、SQL_NUMERIC_FUNCTIONS、SQL_STRING_FUNCTIONS、SQL_SYSTEM_FUNCTIONS 和 SQL_TIMEDATE_FUNCTIONS 選項來呼叫**SQLGetInfo** 。 為了判斷**CONVERT**函式支援哪些轉換作業，應用程式會使用以 SQL_CONVERT 開頭的任何選項來呼叫**SQLGetInfo** 。
