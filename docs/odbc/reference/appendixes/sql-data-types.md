---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4be0e017988670d740067011f775f8477037aa18
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057036"
---
# <a name="sql-data-types"></a>SQL 資料類型
每個 DBMS 都會定義自己的 SQL 類型。 每個 ODBC 驅動程式只會公開相關聯之 DBMS 定義的 SQL 資料類型。 驅動程式如何將 DBMS SQL 類型對應至 ODBC 定義的 SQL 類型識別碼，以及驅動程式如何將 DBMS SQL 類型對應到自己的驅動程式特定 SQL 類型識別碼的資訊，會透過呼叫**SQLGetTypeInfo**來傳回。 當透過呼叫**SQLColAttribute**、 **SQLColumns**、 **SQLDescribeCol**、 **SQLDescribeParam**、 **SQLProcedureColumns**和**SQLSpecialColumns**來描述資料行和參數的資料類型時，驅動程式也會傳回 SQL 資料類型。  
  
> [!NOTE]  
>  SQL 資料類型包含在執行描述項的 SQL_DESC_ CONCISE_TYPE、SQL_DESC_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位中。 SQL 資料類型的特性包含在執行描述項的 [SQL_DESC_PRECISION]、[SQL_DESC_SCALE]、[SQL_DESC_LENGTH] 和 [SQL_DESC_OCTET_LENGTH] 欄位中。 如需詳細資訊，請參閱本附錄稍後的[資料類型識別碼和描述](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)元。  
  
 給定的驅動程式和資料來源不一定支援本附錄中定義的所有 SQL 資料類型。 驅動程式對 SQL 資料類型的支援取決於驅動程式符合的 SQL-92 層級。 為了判斷驅動程式支援的 SQL-92 文法層級，應用程式會使用 SQL_SQL_CONFORMANCE 資訊類型來呼叫**SQLGetInfo** 。 此外，指定的驅動程式和資料來源可能支援其他驅動程式特定的 SQL 資料類型。 為了判斷驅動程式支援的資料類型，應用程式會呼叫**SQLGetTypeInfo**。 如需有關驅動程式特定 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。 如需特定資料來源中之資料類型的詳細資訊，請參閱該資料來源的檔集。  
  
> [!IMPORTANT]  
>  本附錄中的表格只是指導方針，並且會顯示 SQL 資料類型的一般使用名稱、範圍和限制。 給定的資料來源可能只支援部分列出的資料類型，而支援的資料類型的特性可能與列出的不同。  
  
 下表列出所有 SQL 資料類型的有效 SQL 類型識別碼。 資料表也會列出 SQL-92 （如果有的話）中對應資料類型的名稱和描述。  
  
|SQL 類型識別碼 [1]|一般 SQL 資料<br /><br /> 類型 [2]|一般類型描述|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR （*n*）|固定字串長度*n*的字元字串。|  
|SQL_VARCHAR|VARCHAR （*n*）|最大字串長度為*n*的可變長度字元字串。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可變長度的字元資料。 最大長度是與資料來源相關的。9|  
|SQL_WCHAR|WCHAR （*n*）|固定字串長度*n*的 Unicode 字元字串|  
|SQL_WVARCHAR|VARWCHAR （*n*）|Unicode 可變長度字元字串，最大字串長度為*n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 可變長度的字元資料。 最大長度是與資料來源相關|  
|SQL_DECIMAL|DECIMAL （*p*，*s*）|帶正負號的精確數值，有效位數為至少*p*和 scale *s。* （最大有效位數是驅動程式定義的）。（1 <= *p* <= 15;*s* <= *p*）。4gb|  
|SQL_NUMERIC|NUMERIC （*p*，*s*）|具有有效位數*p*和小數位數*s*的帶正負號、精確的數值（1 <= *p* <= 15;*s* <= *p*）。4gb|  
|SQL_SMALLINT|SMALLINT|有效位數5且小數位數為0的精確數值（帶正負號：-32768 <= *n* <= 32767，不帶正負號： 0 <= *n* <= 65535） [3]。|  
|SQL_INTEGER|INTEGER|精確度為10且小數位數為0的確切數值（帶正負號：-2 [31] <= *n* <= 2 [31]-1，不帶正負號： 0 <= *n* <= 2 [32]-1） [3]。|  
|SQL_REAL|real|帶正負號、近似的數值，其二進位有效位數為24（零或絕對值 10 [-38] 到 10 [38]）。|  
|SQL_FLOAT|FLOAT （*p*）|帶正負號、近似的數值，其二進位有效位數至少為*p*。 （最大有效位數是驅動程式定義的）。第|  
|SQL_DOUBLE|DOUBLE PRECISION|帶正負號、近似的數值，其二進位有效位數為53（零或絕對值 10 [-308] 到 10 [308]）。|  
|SQL_BIT|BIT|單一位的二進位資料。8|  
|SQL_TINYINT|TINYINT|有效位數3且小數位數為0的確切數值（帶正負號：-128 <= *n* <= 127，不帶正負號： 0 <= *n* <= 255） [3]。|  
|SQL_BIGINT|BIGINT|有效位數為19（如果帶正負號）或20（如果不帶正負號）且小數位數為0（帶正負號：-2 [63] <= *n* <= 2 [63]-1，不帶正負號： 0 <= *n* <= 2 [64]-1） [3]，[9] 的精確數值。|  
|SQL_BINARY|BINARY （*n*）|固定長度*n*的二進位資料。9|  
|SQL_VARBINARY|VARBINARY （*n*）|長度上限為*n*的可變長度二進位資料。 最大值是由使用者設定。9|  
|SQL_LONGVARBINARY|長 VARBINARY|可變長度的二進位資料。 最大長度是與資料來源相關的。9|  
|SQL_TYPE_DATE [6]|日期|[年]、[月] 和 [日] 欄位，符合西曆的規則。 （請參閱本附錄稍後[的西曆條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)）。|  
|SQL_TYPE_TIME [6]|時間（*p*）|[小時]、[分] 和 [第二個] 欄位，其中包含小時00到23的有效值、00到59分鐘的有效值，以及00到61的有效值。 精確度*p*表示秒數有效位數。|  
|SQL_TYPE_TIMESTAMP [6]|時間戳記（*p*）|Year、month、day、hour、minute 和 second 欄位，其有效值如日期和時間資料類型所定義。|  
|SQL_TYPE_UTCDATETIME|DATETIMEOFFSET.UTCDATETIME|Year、month、day、hour、minute、second、utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位具有1/10 微秒的精確度。|  
|SQL_TYPE_UTCTIME|UTCTIME|Hour、minute、second、utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位的精確度為1/10 微秒。|  
|SQL_INTERVAL_MONTH [7]|間隔月份（*p*）|兩個日期之間的月數;*p*是間隔的有效位數。|  
|SQL_INTERVAL_YEAR [7]|間隔年份（*p*）|兩個日期之間的年數。*p*是間隔的有效位數。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|間隔年份（*p*）至月|兩個日期之間的年份和月份數;*p*是間隔的有效位數。|  
|SQL_INTERVAL_DAY [7]|間隔日（*p*）|兩個日期之間的天數。*p*是間隔的有效位數。|  
|SQL_INTERVAL_HOUR [7]|間隔小時（*p*）|兩個日期/時間之間的時數*p*是間隔的有效位數。|  
|SQL_INTERVAL_MINUTE [7]|間隔分鐘數（*p*）|兩個日期/時間之間的分鐘數。*p*是間隔的有效位數。|  
|SQL_INTERVAL_SECOND [7]|間隔秒數（*p*、*q*）|兩個日期/時間之間的秒數。*p*是間隔的有效位數，而*q*是間隔秒數有效位數。|  
|SQL_INTERVAL_DAY_TO_HOUR [7]|間隔日（*p*）到小時|兩個日期/時間之間的天數/小時數;*p*是間隔的有效位數。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|間隔日（*p*）到分鐘|兩個日期/時間之間的天數/小時/分鐘數;*p*是間隔的有效位數。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|間隔日（*p*）到秒（*q*）|兩個日期/時間之間的天數/小時/分鐘數/秒;*p*是間隔的有效位數，而*q*是間隔秒數有效位數。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|間隔小時（*p*）到分鐘|兩個日期/時間之間的時數/分鐘;*p*是間隔的有效位數。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|間隔小時（*p*）到秒（*q*）|兩個日期/時間之間的小時/分鐘數/秒;*p*是間隔的有效位數，而*q*是間隔秒數有效位數。|  
|SQL_INTERVAL_MINUTE_TO_SECOND [7]|間隔分鐘數（*p*）到第二個（*q*）|兩個日期/時間之間的分鐘數/秒;*p*是間隔的有效位數，而*q*是間隔秒數有效位數。|  
|SQL_GUID|GUID|固定長度的 GUID。|  
  
 [1] 這是呼叫**SQLGetTypeInfo**時，在 DATA_TYPE 資料行中傳回的值。  
  
 [2] 這是在名稱中傳回的值，並藉由呼叫**SQLGetTypeInfo**來建立 PARAMS 資料行。 [名稱] 資料行會傳回指定-例如 CHAR，而 [建立 PARAMS] 資料行會傳回以逗號分隔的建立參數清單，例如有效位數、小數位數和長度。  
  
 [3] 應用程式會使用**SQLGetTypeInfo**或**SQLColAttribute**來判斷結果集內的特定資料類型或特定資料行是否不帶正負號。  
  
 [4] SQL_DECIMAL 和 SQL_NUMERIC 資料類型的差異只在於其精確度。 DECIMAL （*p*，*s*）的精確度是實值定義的十進位有效位數，其不小於*p*，而數值（*p*，*s*）的精確度則完全等於*p*。  
  
 [5] 根據執行而定，SQL_FLOAT 的有效位數可以是24或53：如果是24，則 SQL_FLOAT 資料類型與 SQL_REAL 相同。如果是53，SQL_FLOAT 資料類型與 SQL_DOUBLE 相同。  
  
 [6]*在 ODBC 3.x 中，SQL*日期、時間和時間戳記資料類型分別是 SQL_TYPE_DATE、SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP;在 ODBC *2.x 中，資料*類型是 SQL_DATE、SQL_TIME 和 SQL_TIMESTAMP。  
  
 [7] 如需間隔 SQL 資料類型的詳細資訊，請參閱本附錄稍後的[Interval 資料類型](../../../odbc/reference/appendixes/interval-data-types.md)一節。  
  
 [8] SQL_BIT 資料類型與 SQL-92 中的 BIT 類型具有不同的特性。  
  
 [9] 這個資料類型在 SQL-92 中沒有對應的資料類型。  
  
 本節提供下列範例。  
  
-   [SQLGetTypeInfo 結果集範例](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
