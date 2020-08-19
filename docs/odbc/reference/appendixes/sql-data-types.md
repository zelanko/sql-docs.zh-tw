---
description: SQL 資料類型
title: SQL 資料類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8209463c3c316a5bd2e45a2d7b08eb65b3cb113d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483151"
---
# <a name="sql-data-types"></a>SQL 資料類型
每個 DBMS 都會定義自己的 SQL 類型。 每個 ODBC 驅動程式都只會公開相關聯 DBMS 定義的 SQL 資料類型。 有關驅動程式如何將 DBMS SQL 型別對應到 ODBC 定義的 SQL 類型識別碼的資訊，以及驅動程式如何將 DBMS SQL 型別對應至本身的驅動程式特定 SQL 類型識別碼，會透過呼叫 **SQLGetTypeInfo**來傳回。 當透過呼叫 **SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLProcedureColumns**和 **SQLSpecialColumns**來描述資料行和參數的資料類型時，驅動程式也會傳回 SQL 資料類型。  
  
> [!NOTE]  
>  SQL 資料類型包含在執行描述項的 SQL_DESC_ CONCISE_TYPE、SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位中。 SQL 資料類型的特性包含在執行描述項的 SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH 和 SQL_DESC_OCTET_LENGTH 欄位中。 如需詳細資訊，請參閱本附錄稍後的 [資料類型識別碼和描述](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) 項。  
  
 指定的驅動程式和資料來源不一定支援本附錄中定義的所有 SQL 資料類型。 驅動程式對於 SQL 資料類型的支援取決於驅動程式符合的 SQL-92 層級。 為了判斷驅動程式所支援的 SQL-92 文法層級，應用程式會使用 SQL_SQL_CONFORMANCE 資訊類型來呼叫 **SQLGetInfo** 。 此外，指定的驅動程式和資料來源可能會支援其他的驅動程式特定的 SQL 資料類型。 為了判斷驅動程式支援的資料類型，應用程式會呼叫 **SQLGetTypeInfo**。 如需有關驅動程式特定的 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。 如需特定資料來源中資料類型的詳細資訊，請參閱該資料來源的檔。  
  
> [!IMPORTANT]  
>  本附錄中的表格只是指導方針，而且會顯示 SQL 資料類型的一般使用名稱、範圍和限制。 給定的資料來源可能只支援部分列出的資料類型，而支援的資料類型特性可能與所列出的資料類型不同。  
  
 下表列出所有 SQL 資料類型的有效 SQL 類型識別碼。 資料表也會列出 SQL-92 (中對應資料類型的名稱和描述（如果有的話) ）。  
  
|SQL 類型識別碼 [1]|一般 SQL 資料<br /><br /> 類型 [2]|一般類型描述|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*) |固定字串長度為 *n*的字元字串。|  
|SQL_VARCHAR|VARCHAR (*n*) |最大字串長度為 *n*的可變長度字元字串。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可變長度字元資料。 最大長度取決於資料來源。形|  
|SQL_WCHAR|WCHAR (*n*) |固定字串長度為*n*的 Unicode 字元字串|  
|SQL_WVARCHAR|VARWCHAR (*n*) |Unicode 可變長度字元字串，最大字串長度為 *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 可變長度字元資料。 最大長度與資料來源相依|  
|SQL_DECIMAL|DECIMAL (*p*，*s*) |具有有效位數（至少 *p* 和小數位數）的帶正負號、精確數值 *。*  (最大有效位數為驅動程式定義。 )  (1 <= *p* <= 15;*s*  <= *p*) 。億|  
|SQL_NUMERIC|數值 (*p*，*s*) |具有有效位數*p*和小數位數*s*的已簽署、精確、數值 (1 <= *p* <= 15;*s*  <= *p*) 。億|  
|SQL_SMALLINT|SMALLINT|有效位數5且小數位數為0的精確數值 (帶正負號：-32768 <= *n* <= 32767，未簽署： 0 <= *n* <= 65535) [3]。|  
|SQL_INTEGER|INTEGER|有效位數10且小數位數為0的精確數值 (簽署：-2 [31] <= *n* <= 2 [31]-1，未簽署： 0 <= *n* <= 2 [32]-1) [3]。|  
|SQL_REAL|REAL|具有二進位有效位數 24 (零或絕對值 10 [-38] 到 10 [38] ) 的帶正負號、近似值、數位值。|  
|SQL_FLOAT|FLOAT (*p*) |帶正負號、近似的數值，其中至少有 *p*的二進位精確度。  (最大有效位數為驅動程式定義。 ) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|具有二進位精確度53的帶正負號、近似數值 (零或絕對值 10 [-308] 到 10 [308] ) 。|  
|SQL_BIT|BIT|單一位二進位資料。八角|  
|SQL_TINYINT|TINYINT|有效位數3且小數位數為0的精確數值 (帶正負號：-128 <= *n* <= 127，未簽署： 0 <= *n* <= 255) [3]。|  
|SQL_BIGINT|bigint|精確度19的精確數值 (如果簽署的) 或 20 (如果未簽署的) 和小數位數 0 (已簽署：-2 [63] <= *n* <= 2 [63]-1，未簽署： 0 <= *n* <= 2 [64]-1) [3]，[9]。|  
|SQL_BINARY|二元 (*n*) |固定長度 *n*的二進位資料。形|  
|SQL_VARBINARY|VARBINARY (*n*) |最大長度為 *n*的可變長度二進位資料。 最大值是由使用者設定。形|  
|SQL_LONGVARBINARY|LONG VARBINARY|變數長度二進位資料。 最大長度取決於資料來源。形|  
|SQL_TYPE_DATE [6]|日期|Year、month 和 day 欄位，符合西曆的規則。  (請參閱本附錄稍後 [的西曆條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)。 ) |  
|SQL_TYPE_TIME [6]|TIME (*p*) |Hour、minute 和 second 欄位，有效值為00到23的小時、00到59的有效值，以及00到61的有效秒數。 Precision *p* 表示秒數有效位數。|  
|SQL_TYPE_TIMESTAMP [6]|時間戳記 (*p*) |Year、month、day、hour、minute 和 second 欄位，與日期和時間資料類型所定義的有效值相同。|  
|SQL_TYPE_UTCDATETIME|>DATETIMEOFFSET.UTCDATETIME|Year、month、day、hour、minute、second、utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位具有1/10 微秒的精確度。|  
|SQL_TYPE_UTCTIME|UTCTIME|Hour、minute、second、utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位具有1/10 微秒的精確度。|  
|SQL_INTERVAL_MONTH [7]|間隔月份 (*p*) |兩個日期之間的月數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_YEAR [7]|間隔年份 (*p*) |兩個日期之間的年數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|每月的間隔年份 (*p*) |兩個日期之間的年和月數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_DAY [7]|間隔日 (*p*) |兩個日期之間的天數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_HOUR [7]|間隔小時 (*p*) |兩個日期/時間之間的時數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_MINUTE [7]|間隔分鐘 (*p*) |兩個日期/時間之間的分鐘數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_SECOND [7]|間隔秒 (*p*，*q*) |兩個日期/時間之間的秒數; *p* 是間隔的有效位數，而 *q* 是間隔的秒數有效位數。|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|間隔日 (*p*) 為小時|兩個日期/時間之間的天數/小時數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|間隔日 (*p*) 為分鐘|兩個日期/時間之間的天數/小時/分鐘數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|間隔日 (*p*) 至第二個 (*q*) |兩個日期/時間之間的天數/小時/分鐘/秒數; *p* 是間隔的有效位數，而 *q* 是間隔的秒數有效位數。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|間隔小時 (*p*) 為分鐘|兩個日期/時間之間的小時數/分鐘數; *p* 是間隔前置精確度。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|間隔小時 (*p*) 至第二 (*q*) |兩個日期/時間之間的小時/分鐘/秒數; *p* 是間隔的有效位數，而 *q* 是間隔的秒數有效位數。|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|間隔分鐘 (*p*) 至第二 (*q*) |兩個日期/時間之間的分鐘數/秒數; *p* 是間隔的有效位數，而 *q* 是間隔的秒數有效位數。|  
|SQL_GUID|GUID|固定長度的 GUID。|  
  
 [1] 這是呼叫 **SQLGetTypeInfo**時，在 DATA_TYPE 資料行中傳回的值。  
  
 [2] 這是在名稱中傳回的值，並透過呼叫 **SQLGetTypeInfo**來建立 PARAMS 資料行。 NAME 資料行會傳回指定（例如 CHAR），而 CREATE PARAMS 資料行則會傳回以逗號分隔的建立參數清單，例如有效位數、小數位數和長度。  
  
 [3] 應用程式使用 **SQLGetTypeInfo** 或 **SQLColAttribute** 來判斷特定資料類型或結果集內的特定資料行是否未簽署。  
  
 [4] SQL_DECIMAL 和 SQL_NUMERIC 資料類型的精確度不同。 十進位 (*p*，*s*) 的有效位數是實值的有效位數，不小於*p*，而數值 (*p**的有效位數) 完全*等於*p*。  
  
 [5] 根據執行的不同，SQL_FLOAT 的精確度可以是24或53：如果是24，則 SQL_FLOAT 資料類型與 SQL_REAL 相同;如果是53，SQL_FLOAT 資料類型與 SQL_DOUBLE 相同。  
  
 [6] *在 ODBC 3.x 中，* SQL 日期、時間和時間戳記資料類型分別為 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP;在 ODBC *2.x 中，* 資料類型為 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP。  
  
 [7] 如需 SQL 資料類型間隔的詳細資訊，請參閱本附錄稍後的「 [間隔資料類型](../../../odbc/reference/appendixes/interval-data-types.md) 」一節。  
  
 [8] SQL_BIT 的資料類型與 SQL-92 中的位類型具有不同的特性。  
  
 [9] 此資料類型在 SQL-92 中沒有對應的資料類型。  
  
 本節提供下列範例。  
  
-   [範例 SQLGetTypeInfo 結果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
