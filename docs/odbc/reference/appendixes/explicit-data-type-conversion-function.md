---
description: 明確資料類型轉換函式
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
ms.openlocfilehash: da897469d26cd0403dc023cfcd3f3e03bfceeba4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466185"
---
# <a name="explicit-data-type-conversion-function"></a>明確資料類型轉換函式
明確的資料類型轉換是根據 SQL 資料類型定義來指定。  
  
 明確資料類型轉換函數的 ODBC 語法不會限制轉換。 將某種資料類型轉換成另一種資料類型的有效性將由每個驅動程式特定的實作為決定。 驅動程式會將 ODBC 語法轉譯成原生語法，以拒絕這些轉換，雖然資料來源不支援 ODBC 語法中合法的轉換。 ODBC 函數 **SQLGetInfo**具有轉換選項 (例如 SQL_CONVERT_BIGINT、SQL_CONVERT_BINARY、SQL_CONVERT_INTERVAL_YEAR_MONTH 等) ，可提供一種方式來查詢資料來源所支援的轉換。  
  
 **CONVERT**函數的格式為：  
  
 **轉換 (** _value_exp_、 _data_type_ **) **  
  
 函數會傳回 *value_exp* 轉換成指定的 *data_type*所指定的值，其中 *data_type* 是下列其中一個關鍵字：  

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
  
 引數 *value_exp* 可以是資料行名稱、另一個純量函數的結果，或是數值或字串常值。 例如：  
  
```  
{ fn CONVERT( { fn CURDATE() }, SQL_CHAR ) }  
```  
  
 將 CURDATE 純量函數的輸出轉換成字元字串。  
  
 由於 ODBC 不會針對純量函式的傳回值強制資料型別 (因為函數通常是資料來源特定的) ，因此應用程式應該盡可能使用 CONVERT 純量函數來強制執行資料類型轉換。  
  
 下列兩個範例說明 **CONVERT** 函數的用法。 這些範例假設有一個名為 EMPLOYEES 的資料表，具有 SQL_SMALLINT 類型的具有 EMPNO 資料行，以及 SQL_CHAR 類型的 EMPNAME 資料行。  
  
 如果應用程式指定下列 SQL 語句：  
  
```  
SELECT EMPNO FROM EMPLOYEES WHERE {fn CONVERT(EMPNO,SQL_CHAR)} LIKE '1%'  
```  
  
-   ORACLE 的驅動程式會將 SQL 語句轉譯為：  
  
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
  
-   ORACLE 的驅動程式會將 SQL 語句轉譯為：  
  
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
