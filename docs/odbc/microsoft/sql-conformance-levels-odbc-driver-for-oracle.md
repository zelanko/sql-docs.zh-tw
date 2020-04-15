---
title: SQL 一致性級別(Oracle 的 ODBC 驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300678"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性層級 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 的 ODBC 驅動程式支援最小 SQL 語法和核心 SQL 語法,還支援以下對 SQL 的 ODBC 延伸:  
  
-   日期、時間與時間戳資料  
  
-   左和右外部聯結  
  
-   數位函數:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|簽署||  
    |Exp|Pi|sin||  
    |樓層|Power|sqrt||  
  
-   日期函式：  
  
    |||||  
    |-|-|-|-|  
    |庫達|週日|月名|second|  
    |詛咒|Dayofyear|minute|week|  
    |日名|Hour|就試試|year|  
    |每月的一天|Month|quarter||  
  
-   字串函式：  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|向右|烏瓦凱斯|  
    |Char|長度|裡特裡姆||  
    |Concat|Ltrim|音效||  
    |Lcase|Replace|substring||  
  
-   類型轉換功能:  
  
    ||  
    |-|  
    |轉換|  
  
-   系統功能:  
  
    ||  
    |-|  
    |Ifnull|  
    |User|
