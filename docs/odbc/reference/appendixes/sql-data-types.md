---
title: SQL 資料類型 |微軟文件
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
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305002"
---
# <a name="sql-data-types"></a>SQL 資料類型
每個 DBMS 定義其自己的 SQL 類型。 每個 ODBC 驅動程式僅公開關聯的 DBMS 定義的 SQL 資料類型。 有關驅動程式如何將 DBMS SQL 類型映射到 ODBC 定義的 SQL 類型識別符以及驅動程式如何將 DBMS SQL 類型映射到其自己的特定於驅動程式的 SQL 類型識別符的資訊將透過呼叫**SQLGetTypeInfo**傳回。 當透過調用 SQLColattribute、SQLColumns、SQLDescribeCol、SQLDescribeParam、SQL**SQLColAttribute****程式列**和**SQLColumns****SQL 特殊列**來描述列和**SQLDescribeParam**參數的數據類型時,驅動程式也會**SQLDescribeCol**返回 SQL 資料類型。  
  
> [!NOTE]  
>  SQL 資料類型包含在實現描述符SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位中。 SQL 資料類型的特徵包含在實現描述符的SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH和SQL_DESC_OCTET_LENGTH欄位中。 關於詳細資訊,請參閱本附錄後面的[資料類型識別碼和描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)號 。  
  
 給定的驅動程式和資料來源不一定支援本附錄中定義的所有 SQL 資料類型。 驅動程式對 SQL 資料類型的支援取決於驅動程式符合的 SQL-92 級別。 要確定驅動程式支援的 SQL-92 語法等級,應用程式使用SQL_SQL_CONFORMANCE資訊類型呼叫**SQLGetInfo。** 此外,給定的驅動程式和數據源可能支援其他特定於驅動程式的 SQL 資料類型。 要確定驅動程式支援哪些資料類型,應用程式將呼叫**SQLGetTypeInfo**。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。 有關特定數據源中的數據類型的資訊,請參閱該數據源的文檔。  
  
> [!IMPORTANT]  
>  本附錄中的表只是指南,顯示 SQL 數據類型的常用名稱、範圍和限制。 給定的數據源可能僅支援某些列出的數據類型,並且支援的數據類型的特徵可能與列出的數據類型不同。  
  
 下表列出了所有 SQL 資料類型的有效 SQL 類型識別碼。 該表還列出了 SQL-92 中相應數據類型的名稱和說明(如果存在)。  
  
|SQL 類型識別碼 {1}|典型的 SQL 資料<br /><br /> 型態[2]】|典型類型描述|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|固定字串長度 n*的*字串。|  
|SQL_VARCHAR|瓦爾查爾(*n*)|具有最大字串長度*n 的*可變長度字串。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可變長度字元資料。 最大長度與數據源相關。[9]|  
|SQL_WCHAR|WCHAR(*n*)|固定字串長度*n*的單碼字串|  
|SQL_WVARCHAR|瓦爾瓦查爾(*n*)|具有最大字串長度*n*的 Unicode 可變長度字串|  
|SQL_WLONGVARCHAR|朗瓦查爾|Unicode 可變長度字元資料。 最大長度取決於資料來源|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|簽名、精確、數值,精度至少為*p*和刻度*s。* (最大精度為驅動程式定義。(1 <= *p* <= 15;*s* <= *p*。[4]|  
|SQL_NUMERIC|數字 *(p*,*s*)|帶精確*p*和刻度*s*的符號、精確、數值(1 <= *p* <= 15;*s* <= *p*。[4]|  
|SQL_SMALLINT|SMALLINT|精度為 5 和刻度 0 的精確數值(簽名: -32,768 <= *n* <= 32,767,未簽名:0 <= *n* <= 65,535)[3]。|  
|SQL_INTEGER|INTEGER|精度為 10 和刻度 0 的精確數值(簽名: -2[31] <= *n* <= 2[31] - 1,未簽名:0 <= *n* <= 2[32] - 1)[3]。|  
|SQL_REAL|real|具有二進位精度 24(零或絕對值 10[-38] 到 10[38])的符號、近似數值。|  
|SQL_FLOAT|浮動(*p*)|簽名的、近似的數值,二進位精確度至少為*p*。 (最大精度為驅動程式定義。[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|簽名、近似、數值,二進位精度 53(零或絕對值 10[-308] 到 10[308])。|  
|SQL_BIT|BIT|單位二進位數據。[8]|  
|SQL_TINYINT|TINYINT|精度為 3 和刻度 0 的精確數值(簽名: -128 <= *n* <= 127,無符號:0 <= *n* <= 255)[3]。|  
|SQL_BIGINT|bigint|精度為 19(如果已簽名)或 20(如果未簽名)和刻度 0(簽名:-2[63] <= *n* <= 2[63] - 1,未簽名:0 <= *n* <= 2[64] - 1)[3],[9]。|  
|SQL_BINARY|BINARY(*n*)|固定長度 n*的*二進位數據。[9]|  
|SQL_VARBINARY|瓦爾里數(*n*)|最大長度*n*的可變長度二進位數據。 最大值由用戶設置。[9]|  
|SQL_LONGVARBINARY|長瓦二進位|變數長度二進位資料。 最大長度與數據源相關。[9]|  
|SQL_TYPE_DATE[6]|日期|年、月和日欄位,符合公曆的規則。 (請參閱[公曆的約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md),本附錄後面的內容。|  
|SQL_TYPE_TIME[6]|時間(*p*)|小時、分鐘和第二個字段(有效值為小時為 00 到 23)、分鐘為 00 到 59 的有效值以及秒數為 00 到 61 的有效值。 精度*p*表示秒精度。|  
|SQL_TYPE_TIMESTAMP[6]|時間標記(*p*)|年份、月份、日、小時、分鐘和第二個字段,為 DATE 和 TIME 數據類型定義有效值。|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|年、月、日、小時、分鐘、秒、utchour 和 utc 分鐘欄位。 utchour 和 utc 分鐘欄位具有 1/10 微秒精度。|  
|SQL_TYPE_UTCTIME|UTC 時間|小時、分鐘、秒、utchour 和 utc 分鐘欄位。 utchour 和 utc 分鐘欄位具有 1/10 微秒精度。|  
|SQL_INTERVAL_MONTH[7]|間隔月(*p*)|兩個日期之間的月數;*p*是間隔前導精度。|  
|SQL_INTERVAL_YEAR[7]|間隔年(*p*)|兩個日期之間的年數;*p*是間隔前導精度。|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|間隔年(*p*) 到月|兩個日期之間的年數和月數;*p*是間隔前導精度。|  
|SQL_INTERVAL_DAY[7]|間隔日(*p*)|兩個日期之間的天數;*p*是間隔前導精度。|  
|SQL_INTERVAL_HOUR[7]|間隔小時(*p*)|兩個日期/時間之間的小時數;*p*是間隔前導精度。|  
|SQL_INTERVAL_MINUTE[7]|間隔分鐘(*p*)|兩個日期/時間之間的分鐘數;*p*是間隔前導精度。|  
|SQL_INTERVAL_SECOND[7]|間隔秒(*p*,*q*)|兩個日期/時間之間的秒數;*p*是間隔前導精度 *,q*是間隔秒精度。|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|間隔日(*p*) 到 HOUR|兩個日期/時間之間的天數/小時數;*p*是間隔前導精度。|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|間隔日(*p*) 到分鐘|兩個日期/時間之間的天數/小時/分鐘數;*p*是間隔前導精度。|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|間隔日(*p*) 到 秒 (*q*)|兩個日期/時間之間的天數/小時/分鐘/秒數;*p*是間隔前導精度 *,q*是間隔秒精度。|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|間隔小時(*p*) 到分鐘|兩個日期/時間之間的小時/分鐘數;*p*是間隔前導精度。|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|間隔小時(*p*) 到 秒 (*q*)|兩個日期/時間之間的小時/分鐘/秒數;*p*是間隔前導精度 *,q*是間隔秒精度。|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|間隔分鐘(*p*) 到 秒 (*q*)|兩個日期/時間之間的分鐘/秒數;*p*是間隔前導精度 *,q*是間隔秒精度。|  
|SQL_GUID|GUID|固定長度 GUID。|  
  
 {1} 這是調用**SQLGetTypeInfo**在DATA_TYPE列中返回的值。  
  
 [2] 這是透過呼叫**SQLGetTypeInfo**在 NAME 和 CREATE PARAMS 列中傳回的值。 NAME 列傳回指定(例如,CHAR-而 CREATE PARAMS 列傳回建立參數(如精度、比例和長度)的逗號分隔清單。  
  
 [3] 應用程式使用**SQLGetTypeInfo**或**SQLColAttribute**來確定結果集中的特定數據類型或特定列是否未簽名。  
  
 [4] SQL_DECIMAL和SQL_NUMERIC數據類型的精度僅不同。 *DECIMAL(p**,s*) 的精度是實現定義的十進位精度,不低於*p,* 而*NUMERIC(p**)* 的精度完全等於*p*。  
  
 [5] 根據實現情況,SQL_FLOAT的精度可以是 24 或 53:如果是 24,則SQL_FLOAT數據類型與SQL_REAL相同;如果是 53,則SQL_FLOAT數據類型與SQL_DOUBLE相同。  
  
 [6] 在 ODBC *3.x*中,SQL 日期、時間和時間戳數據類型分別為SQL_TYPE_DATE、SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP;在 ODBC *2.x*中,數據類型為SQL_DATE、SQL_TIME和SQL_TIMESTAMP。  
  
 [7] 有關間隔 SQL 資料類型的詳細資訊,請參閱本附錄後面的[間隔數據類型](../../../odbc/reference/appendixes/interval-data-types.md)部分。  
  
 [8] SQL_BIT資料類型與 SQL-92 中的 BIT 類型具有不同的特徵。  
  
 [9] 此資料類型在 SQL-92 中沒有相應的數據類型。  
  
 本節提供以下示例。  
  
-   [範例 SQLGetTypeInfo 結果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
