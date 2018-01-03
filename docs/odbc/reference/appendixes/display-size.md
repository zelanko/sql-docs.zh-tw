---
title: "顯示大小 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 222150f200720a9213bc8f04cf7900771c2e0619
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="display-size"></a>顯示大小
資料行的顯示大小是以字元格式顯示資料所需字元的數目上限。 下表定義每個 ODBC SQL 資料類型的顯示大小。  
  
|SQL 類型識別碼|顯示大小|  
|-------------------------|------------------|  
|所有的字元類型 [a]|定義 （適用於固定類型） 或 （適用於變數類型） 的最大字元格式顯示資料所需的字元數。|  
|SQL_DECIMAL SQL_NUMERIC|資料行加上 2 的有效位數 (登入的*精確度*數字和小數點)。 例如，定義為 NUMERIC(10,3) 的資料行的顯示大小為 12。|  
|SQL_BIT|1 （1 個數字）。|  
|SQL_TINYINT|如果簽章 （正負號和 3 個數字） 4 或 3，如果不帶正負號 （3 位數）。|  
|SQL_SMALLINT|如果簽章 （正負號和 5 個數字） 6 或 5，如果不帶正負號 （5 個數字）。|  
|SQL_INTEGER|如果簽章 （正負號和 10 個數字） 11 或 10，如果不帶正負號 （10 個數字）。|  
|SQL_BIGINT|20 （正負號和 19 位數，如果簽章或 20 位數，如果不帶正負號）。|  
|SQL_REAL|14 (符號、 7 的數字、 小數點、 字母*E*、 符號以及 2 位數)。|  
|SQL_FLOAT SQL_DOUBLE|24 (符號、 15 位數，小數點、 字母*E*、 符號以及 3 位數)。|  
|所有二進位型別 [a]|定義或 （適用於變數類型） 的最大逾 2 的資料行的長度。 （每個二進位位元組的 2 位數的十六進位數字所表示）。|  
|SQL_TYPE_DATE|10 (日期格式的日期*yyyy-mm-dd*)。|  
|SQL_TYPE_TIME|8 (時間格式*hh: mm:*)<br /><br /> - 或 -<br /><br /> 9 + *s* (時間格式*hh: mm:*[.fff...]，其中*s*小數秒數有效位數)。|  
|SQL_TYPE_TIMESTAMP|19 (如時間戳記在*yyyy-mm-dd hh: mm:*格式)<br /><br /> - 或 -<br /><br /> 20 + *s* (如時間戳記在*yyyy-mm-dd hh: mm:*[.fff …] 格式，其中*s*小數秒數有效位數)。|  
|所有的間隔資料型別|請參閱[間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md)。|  
|SQL_GUID|36 (中的字元數*aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*格式|  
  
 [a] 如果驅動程式無法判斷資料行或參數的長度變數的類型，它會傳回 SQL_NO_TOTAL。
