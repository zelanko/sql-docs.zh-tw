---
description: SQL 一致性層級 (ODBC Driver for Oracle)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483421"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>SQL 一致性層級 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC Driver for Oracle 支援最小的 SQL 文法和 Core SQL 文法，也支援下列 ODBC 擴充至 SQL：  
  
-   日期、時間和時間戳記資料  
  
-   左方和右外部聯結  
  
-   數值函數：  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            樓層  
        :::column-end:::
        :::column:::
            Log  
            Log10  
            Mod  
            Pi  
            電源  
        :::column-end:::
        :::column:::
            round  
            second  
            簽署  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   日期函式：  

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            Dayofmonth  
        :::column-end:::
        :::column:::
            Dayofweek  
            Dayofyear  
            小時  
            Month  
        :::column-end:::
        :::column:::
            monthname  
            minute  
            就試試  
            quarter  
        :::column-end:::
        :::column:::
            second  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   字串函式：  

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Left  
            長度  
            Ltrim  
            取代  
        :::column-end:::
        :::column:::
            向右  
            rtrim  
            soundex  
            substring  
        :::column-end:::
        :::column:::
            ucase  
        :::column-end:::
    :::row-end:::

-   類型轉換函數：  

    轉換  

-   系統函數：  
  
    Ifnull  
    使用者
