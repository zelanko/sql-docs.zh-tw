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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0a1e9155eeb3e2147bed3dd31e78176bdc38d2
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363318"
---
# <a name="explicit-data-type-conversion-function"></a>明確資料類型轉換函式
明確的資料類型轉換是根據 SQL 資料類型定義來指定。  
  
 明確資料類型轉換函數的 ODBC 語法不會限制轉換。 某個資料類型對另一個資料類型之特定轉換的有效性，將由每個驅動程式特定的實作為決定。 驅動程式會將 ODBC 語法轉譯成原生語法，而不會拒絕這些轉換（雖然在 ODBC 語法中是合法的）不受資料來源支援。 ODBC 函數**SQLGetInfo**具有轉換選項（例如 SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH 等等），提供了一種方法來查詢資料來源所支援的轉換。  
  
 **CONVERT**函數的格式為：  
  
 **CONVERT （** _value_exp_， _data_type_**）**  
  
 函式會傳回*value_exp*轉換成指定*data_type*的指定值，其中*data_type*是下列其中一個關鍵字：  

:::row:::
    :::column:::
        SQL_BIGINT  
        SQL_BINARY  
        SQL_BIT  
        SQL_CHAR  
        SQL_DATE  
        SQL_DECIMAL  
        SQL_DOUBLE  
        SQL_FLOAT  
        SQL_GUID  
        SQL_INTEGER  
        SQL_INTERVAL_DAY  
        SQL_INTERVAL_DAY_TO_HOUR  
    :::column-end:::
    :::column:::
        SQL_INTERVAL_DAY_TO_MINUTE  
        SQL_INTERVAL_DAY_TO_SECOND  
        SQL_INTERVAL_HOUR  
        SQL_INTERVAL_HOUR_TO_MINUTE  
        SQL_INTERVAL_HOUR_TO_SECOND  
        SQL_INTERVAL_MINUTE  
        SQL_INTERVAL_MINUTE_TO_SECOND  
        SQL_INTERVAL_MONTH  
        SQL_INTERVAL_SECOND  
        SQL_INTERVAL_YEAR  
        SQL_INTERVAL_YEAR_TO_MONTH  
        SQL_LONGVARBINARY  
    :::column-end:::
    :::column:::
        SQL_LONGVARCHAR  
        SQL_NUMERIC  
        SQL_REAL  
        SQL_SMALLINT  
        SQL_TIME  
        SQL_TIMESTAMP  
        SQL_TINYINT  
        SQL_VARBINARY  
        SQL_VARCHAR  
        SQL_WCHAR  
        SQL_WLONGVARCHAR  
        SQL_WVARCHAR  
    :::column-end:::
:::row-end:::

 明確資料類型轉換函數的 ODBC 語法不支援轉換格式的規格。 如果基礎資料來源支援明確格式的規格，則驅動程式必須指定預設值或執行格式規格。  
  
 *Value_exp*的引數可以是資料行名稱、另一個純量函數的結果，或數值或字串常值。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 將 CURDATE 純量函數的輸出轉換為字元字串。  
  
 因為 ODBC 不會針對純量函數（因為函式通常是資料來源特定）來強制傳回值的資料類型，所以應用程式應該盡可能使用 CONVERT 純量函數來強制轉換資料類型。  
  
 下列兩個範例說明**CONVERT**函數的用法。 這些範例假設有一個名為 EMPLOYEES 的資料表，具有 SQL_SMALLINT 類型的具有 EMPNO 資料行，以及 SQL_CHAR 類型的 EMPNAME 資料行。  
  
 如果應用程式指定下列 SQL 語句：  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 驅動程式會將 SQL 語句轉譯為：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE to_char(EMPNO) LIKE '1%'  
    ```  
  
-   SQL Server 的驅動程式會將 SQL 語句轉譯為：  
  
    ```  
    SELECT EMPNO FROM EMPLOYEES WHERE convert(char,EMPNO) LIKE '1%'  
    ```  
  
 如果應用程式指定下列 SQL 語句：  
  
```  
SELECT {fn ABS(EMPNO)}, {fn CONVERT(EMPNAME,SQL_SMALLINT)}  
   FROM EMPLOYEES WHERE EMPNO <> 0  
```  
  
-   ORACLE 驅動程式會將 SQL 語句轉譯為：  
  
    ```  
    SELECT abs(EMPNO), to_number(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```  
  
-   SQL Server 的驅動程式會將 SQL 語句轉譯為：  
  
    ```  
    SELECT abs(EMPNO), convert(smallint, EMPNAME) FROM EMPLOYEES  
       WHERE EMPNO <> 0  
    ```  
  
-   Ingres 的驅動程式會將 SQL 語句轉譯為：  
  
    ```  
    SELECT abs(EMPNO), int2(EMPNAME) FROM EMPLOYEES WHERE EMPNO <> 0  
    ```
