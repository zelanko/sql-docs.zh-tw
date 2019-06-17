---
title: SQL 一致性層級 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0bf63b831dace7678f5d3fdf952a9d6d5f60aa6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313392"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性層級 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 支援的 Minimum SQL 文法和核心 SQL 文法，而且也支援下列 sql 的 ODBC 延伸模組：  
  
-   日期、 時間和時間戳記的資料  
  
-   左和右外部聯結  
  
-   數值函式：  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |ceiling|log10|second|truncate|  
    |Cos|Mod|符號||  
    |Exp|Pi|sin||  
    |floor|Power|sqrt||  
  
-   日期函數：  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|就試試|year|  
    |Dayofmonth|Month|季||  
  
-   字串函數：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|權限|Ucase|  
    |Char|長度|rtrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|取代|substring||  
  
-   類型轉換函式：  
  
    ||  
    |-|  
    |轉換|  
  
-   系統函數：  
  
    ||  
    |-|  
    |Ifnull|  
    |使用者|
