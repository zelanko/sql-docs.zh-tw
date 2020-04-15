---
title: 明確資料型態轉換功能 。微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2de8a8cb6177e9210e8d48c0ce097d13c9a276fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306989"
---
# <a name="explicit-data-type-conversion-function"></a>明確資料類型轉換函式
顯式資料類型轉換根據 SQL 資料類型定義指定。  
  
 顯式資料類型轉換函數的 ODBC 語法不限制轉換。 一種數據類型到另一種數據類型的特定轉換的有效性將由每個特定於驅動程式的實現確定。 驅動程式將由於它將 ODBC 語法轉換為本機語法,因此將拒絕數據源不支援的轉換(儘管在 ODBC 語法中是合法的)。 ODBC 函數**SQLGetInfo**具有轉換選項(如SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH等),提供了一種查詢數據源支援的轉換的方法。  
  
 **CONVERT**函數的格式為:  
  
 **轉換**_value_exp__(value_exp,data_type)_ ** **  
  
 該函數傳回*value_exp*轉換為指定*data_type*指定的值,其中*data_type*是以下關鍵字之一:  
  
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
  
 顯式資料類型轉換函數的 ODBC 語法不支援轉換格式的規範。 如果基礎資料來源支援顯式格式的規範,則驅動程式必須指定預設值或實現格式規範。  
  
 *參數value_exp*可以是列名、另一個標量函數的結果或數位或字串文本。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 將 CURDATE 標量函數的輸出轉換為字串。  
  
 由於 ODBC 不強制使用標量函數傳回值的資料類型(因為這些函數通常是特定於資料源的),因此應用程式應盡可能使用 CONVERT 標量函數來強制轉換數據類型。  
  
 以下兩個範例說明了**CONVERT**函數的使用。 這些示例假定存在名為「員工」的表,該表的類型為SQL_SMALLINT的 EMPNO 列,類型SQL_CHAR EMPNAME 列。  
  
 如果應用程式指定以下 SQL 語句:  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 的驅動程式將 SQL 語句轉換為:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 的驅動程式將 SQL 語句轉換為:  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 如果應用程式指定以下 SQL 語句:  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 的驅動程式將 SQL 語句轉換為:  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 的驅動程式將 SQL 語句轉換為:  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 的驅動程式將 SQL 語句轉換為:  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
