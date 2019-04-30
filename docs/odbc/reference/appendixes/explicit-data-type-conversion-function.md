---
title: 明確資料類型轉換函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- explicit data type conversion functions [ODBC]
- data type conversion functions [ODBC]
- functions [ODBC], explicit data type conversion functions
ms.assetid: d5789450-b668-4753-96c8-6789e955e7ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77cb69877324b36120b3a277688bb1ad737f5c4d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188983"
---
# <a name="explicit-data-type-conversion-function"></a>明確資料類型轉換函式
明確資料類型轉換是根據 SQL 資料類型定義所指定。  
  
 明確資料類型轉換函式的 ODBC 語法不會限制轉換。 特定一個資料類型轉換成另一種資料類型的有效性取決於每個驅動程式專屬的實作。 驅動程式，因為它會將 ODBC 語法轉譯成原生的語法，拒絕這些轉換，雖然法律在 ODBC 語法中，不支援的資料來源。 ODBC 函數**SQLGetInfo**，轉換選項 （例如 SQL_CONVERT_BIGINT SQL_CONVERT_BINARY、 SQL_CONVERT_INTERVAL_YEAR_MONTH，等等），可用來詢問有關資料來源所支援的轉換.  
  
 格式**轉換**函式是：  
  
 **CONVERT(** _value_exp_, _data_type_**)**  
  
 函式會傳回所指定的值*value_exp*轉換為指定*data_type*，其中*data_type*是其中一個下列關鍵字：  
  
|||  
|-|-|  
|SQL_BIGINT|SQL_INTERVAL_HOUR_TO_MINUTE|  
|SQL_BINARY|SQL_INTERVAL_HOUR_TO_SECOND|  
|SQL_BIT|SQL_INTERVAL_MINUTE_TO_SECOND|  
|SQL_CHAR|SQL_LONGVARBINARY|  
|SQL_DECIMAL|SQL_LONGVARCHAR|  
|SQL_DOUBLE|SQL_NUMERIC|  
|SQL_FLOAT|SQL_REAL|  
|SQL_GUID|SQL_SMALLINT|  
|SQL_INTEGER|SQL_DATE|  
|SQL_INTERVAL_MONTH|SQL_TIME|  
|SQL_INTERVAL_YEAR|SQL_TIMESTAMP|  
|SQL_INTERVAL_YEAR_TO_MONTH|SQL_TINYINT|  
|SQL_INTERVAL_DAY|SQL_VARBINARY|  
|SQL_INTERVAL_HOUR|SQL_VARCHAR|  
|SQL_INTERVAL_MINUTE|SQL_WCHAR|  
|SQL_INTERVAL_SECOND|SQL_WLONGVARCHAR|  
|SQL_INTERVAL_DAY_TO_HOUR|SQL_WVARCHAR|  
|SQL_INTERVAL_DAY_TO_MINUTE||  
|SQL_INTERVAL_DAY_TO_SECOND||  
  
 明確資料類型轉換函式的 ODBC 語法不支援的轉換格式的規格。 如果基礎資料來源所支援的明確的格式規格，則驅動程式就必須指定預設值，或實作格式規格。  
  
 引數*value_exp*可以是資料行名稱、 結果的另一個純量函式或數值或字串常值。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 將 CURDATE 純量函式的輸出轉換成字元字串。  
  
 因為 ODBC 不會託管的傳回值的資料類型 （因為函式通常會將資料來源特有） 的純量函數、 應用程式應該使用轉換的純量函數時，無法強制執行資料類型轉換。  
  
 下列兩個範例說明使用**轉換**函式。 這些範例假設名為 EMPLOYEES 的使用類型 SQL_SMALLINT EMPNO 資料行和類型 SQL_CHAR EMPNAME 資料行的資料表存在。  
  
 如果應用程式指定下列的 SQL 陳述式：  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 的驅動程式會將轉譯的 SQL 陳述式：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 的驅動程式會將轉譯的 SQL 陳述式：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 如果應用程式指定下列的 SQL 陳述式：  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 的驅動程式會將轉譯的 SQL 陳述式：  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 的驅動程式會將轉譯的 SQL 陳述式：  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 的驅動程式會將轉譯的 SQL 陳述式：  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
