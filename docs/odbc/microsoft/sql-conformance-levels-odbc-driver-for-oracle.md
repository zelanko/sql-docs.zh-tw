---
title: SQL 一致性層級（ODBC Driver for Oracle） |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e283bbc13f0d0dda055b047b027f7b9816502df5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300678"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性層級 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 支援最低 SQL 文法和 Core SQL 文法，而且也支援下列 SQL ODBC 延伸模組：  
  
-   日期、時間和時間戳記資料  
  
-   左方和右方外部聯結  
  
-   數值函數：  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|簽署||  
    |Exp|Pi|sin||  
    |樓層|電源|sqrt||  
  
-   日期函式：  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|monthname|second|  
    |Curtime|Dayofyear|minute|week|  
    |Dayname|Hour|就試試|year|  
    |Dayofmonth|Month|quarter||  
  
-   字串函式：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|向右|ucase|  
    |Char|長度|rtrim||  
    |Concat|Ltrim|soundex||  
    |Lcase|Replace|substring||  
  
-   類型轉換函式：  
  
    ||  
    |-|  
    |轉換|  
  
-   系統函數：  
  
    ||  
    |-|  
    |Ifnull|  
    |User|
