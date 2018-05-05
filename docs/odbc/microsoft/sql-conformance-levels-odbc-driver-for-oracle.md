---
title: SQL 一致性層級 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6124577353292209f2bcbd2ca35b6b33add34ca6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性層級 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 支援的最小 SQL 文法和核心 SQL 文法和也支援下列 sql 的 ODBC 延伸模組：  
  
-   日期、 時間和時間戳記資料  
  
-   左和右外部聯結  
  
-   數值的函式：  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|符號||  
    |Exp|pi|sin||  
    |floor|Power|sqrt||  
  
-   日期函數：  
  
    |||||  
    |-|-|-|-|  
    |Curdate|dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|就試試|year|  
    |dayofmonth|Month|季||  
  
-   字串函數：  
  
    |||||  
    |-|-|-|-|  
    |ascii|Left|權限|ucase|  
    |Char|長度|rtrim||  
    |Concat|Ltrim|soundex||  
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
