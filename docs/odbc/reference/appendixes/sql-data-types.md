---
title: "SQL 資料類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9594ce3aa76af66cccc69936677cf2d9aa682a6f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sql-data-types"></a>SQL 資料類型
每個 DBMS 定義自己的 SQL 型別。 每個 ODBC 驅動程式會顯示只有這些 SQL 資料型別相關聯的 DBMS 所定義。 ODBC 定義的 SQL 類型識別項類型的資訊關於如何將驅動程式對應 DBMS SQL 和驅動程式將 DBMS SQL 類型對應至它自己的驅動程式專屬 SQL 類型識別項的方式透過呼叫傳回**SQLGetTypeInfo**。 驅動程式也會傳回 SQL 資料類型描述的資料行及透過呼叫參數的資料型別時**SQLColAttribute**， **SQLColumns**， **SQLDescribeCol**，**SQLDescribeParam**， **SQLProcedureColumns**，和**SQLSpecialColumns**。  
  
> [!NOTE]  
>  SQL 資料類型都包含在 SQL_DESC_ CONCISE_TYPE、 的 SQL_DESC_TYPE、 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的實作描述元。 SQL 資料類型的特性包含 SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH 和 SQL_DESC_OCTET_LENGTH 實作描述項欄位中。 如需詳細資訊，請參閱[資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)本附錄後面。  
  
 指定的驅動程式和資料來源不一定支援本附錄中所定義的所有 SQL 資料類型。 SQL 資料類型的驅動程式的支援取決於驅動程式符合 sql-92 的層級。 若要判斷驅動程式支援的 SQL 92 文法的層級，應用程式呼叫**SQLGetInfo** SQL_SQL_CONFORMANCE 資訊類型。 此外，指定驅動程式和資料來源可能支援其他的驅動程式特有的 SQL 資料類型。 若要判斷哪些資料類型的驅動程式支援，應用程式呼叫**SQLGetTypeInfo**。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。 特定資料來源的資料類型相關的資訊，請參閱該資料來源的文件。  
  
> [!IMPORTANT]  
>  此附錄在整個資料表是唯一的指導方針和常用的顯示名稱、 範圍和 SQL 資料類型的限制。 指定的資料來源可能只支援某些列出的資料類型，並不支援的資料類型的特性可以從所列出的一樣。  
  
 下表列出所有的 SQL 資料類型的有效 SQL 類型識別項。 這個表格也列出的名稱和描述的對應資料類型從 SQL 92 （如果有的話）。  
  
|SQL 類型識別碼 [1]|一般 SQL 資料<br /><br /> 類型 [2]|一般類型的描述|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|字元字串的固定的字串長度 *n* 。|  
|SQL_VARCHAR|VARCHAR (*n*)|最大字串長度與可變長度的字元字串 *n* 。|  
|SQL_LONGVARCHAR|LONG VARCHAR|可變長度的字元資料。 最大長度為資料來源而定。[9]|  
|SQL_WCHAR|WCHAR (*n*)|固定的字串長度的 Unicode 字元字串*n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Unicode 可變長度的字元字串的最大字串長度*n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Unicode 可變長度的字元資料。 最大長度是資料來源而定|  
|SQL_DECIMAL|十進位 (*p*，*s*)|帶正負號，完全、 數字值的有效位數最少*p*和小數位數*s。* （最大有效位數是驅動程式定義）。(1 < = *p* < = 15。*s* <= *p*)。 [4]|  
|SQL_NUMERIC|數值 (*p*，*s*)|帶正負號，完全、 數字的值，有效位數*p*和小數位數*s* (1 < = *p* < = 15。*s* <= *p*)。 [4]|  
|SQL_SMALLINT|SMALLINT|確切的數值有效位數 5、 小數點位數為 0 (帶正負號: – 32768 < =  *n*  < = 32767、 不帶正負號： 0 < =  *n*  < = 65535) [3]。|  
_INTEGER|INTEGER|確切的數值有效位數 10 和小數點位數為 0 (帶正負號: – 2 [31] < =  *n*  < = 2 [31] – 1，而不帶正負號： 0 < =  *n*  < = 2 [32] – 1) [3]。|  
|SQL_REAL|REAL|帶正負號，以二進位精確度 24 的近似、 數字值 （零或至 10[38]) 的絕對值 10 [–38]。|  
|SQL_FLOAT|FLOAT (*p*)|帶正負號，大約、 數字值具有二進位精確度至少*p*。 （最大有效位數是驅動程式定義）。[5]|  
|SQL_DOUBLE|DOUBLE PRECISION|帶正負號，以二進位精確度 53 的近似、 數字值 （零或至 10[308]) 的絕對值 10 [–308]。|  
|SQL_BIT|BIT|單一位元的二進位資料。[8]|  
|SQL_TINYINT|TINYINT|確切的數字位數為 3 的值、 小數點位數為 0 (帶正負號: – 128 < =  *n*  < = 127，不帶正負號： 0 < =  *n*  < = 255) [3]。|  
_BIGINT|bigint|確切的數值有效位數為 19 （如果帶正負號） 或 20 （如果不帶正負號）、 小數點位數為 0 (帶正負號: – 2 [63] < =  *n*  < = 2 [63] – 1，而不帶正負號： 0 < =  *n*  < = 2 [64] – 1) [3]，[9]。|  
|SQL_BINARY|二進位 (*n*)|固定長度的二進位資料 *n* 。 [9]|  
|SQL_VARBINARY|VARBINARY (*n*)|可變長度二進位資料的最大長度 *n* 。 最大值是由使用者設定。[9]|  
|SQL_LONGVARBINARY|LONG VARBINARY|可變長度二進位資料。 最大長度為資料來源而定。[9]|  
|SQL_TYPE_DATE [6]|DATE|年、 月和日等欄位，不符合西曆的規則。 (請參閱[西曆的條件約束](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md)稍後在本附錄中。)|  
|SQL_TYPE_TIME [6]|時間 (*p*)|小時、 分鐘和具有 00 到 59 分鐘的 00 到 23，有效的值時的有效值和有效的秒數 00 到 61 值的第二個欄位。 有效位數*p*表示秒數有效位數。|  
|SQL_TYPE_TIMESTAMP [6]|時間戳記 (*p*)|年、 月、 日、 小時、 分鐘和第二個欄位，以有效的值為日期和時間資料類型所定義。|  
_TYPE_UTCDATETIME|UTCDATETIME|年、 月、 日、 小時、 分鐘、 秒、 utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位具有 1/10 微秒有效位數。|  
|SQL_TYPE_UTCTIME|UTCTIME|小時、 分鐘、 秒、 utchour 和 utcminute 欄位。 Utchour 和 utcminute 欄位有 1/10 微秒的精確度...|  
|SQL_INTERVAL_MONTH [7]|INTERVAL MONTH (*p*)|兩個日期; 之間的月數*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_YEAR [7]|INTERVAL YEAR (*p*)|兩個日期; 之間的年數*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|INTERVAL YEAR (*p*) 到月份|年數和兩個日期; 之間的月數*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_DAY [7]|INTERVAL DAY (*p*)|兩個日期; 之間的天數*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_HOUR [7]|INTERVAL HOUR (*p*)|兩個小時數日期/時間。*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_MINUTE [7]|INTERVAL MINUTE (*p*)|兩個之間的分鐘數的日期/時間。*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_SECOND [7]|間隔第二個 (*p*，*q*)|兩個之間的秒數將日期/時間。*p*是間隔開頭有效位數和*q*的間隔秒數有效位數。|  
_INTERVAL_DAY_TO_HOUR [7]|INTERVAL DAY (*p*) 小時的時間|天/之間的小時數兩個日期/時間。*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|INTERVAL DAY (*p*) 為分鐘|天/小時/之間的分鐘數兩個日期/時間。*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|INTERVAL DAY (*p*) 第二個 (*q*)|數天/小時/分鐘/秒兩個日期/時間。*p*是間隔開頭有效位數和*q*的間隔秒數有效位數。|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|INTERVAL HOUR (*p*) 為分鐘|小時/之間的分鐘數兩個日期/時間。*p*是間隔開頭有效位數。|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|INTERVAL HOUR (*p*) 第二個 (*q*)|兩個小時/分鐘/秒數將日期/時間。*p*是間隔開頭有效位數和*q*的間隔秒數有效位數。|  
_INTERVAL_MINUTE_TO_SECOND [7]|INTERVAL MINUTE (*p*) 第二個 (*q*)|分鐘/之間的秒數兩個日期/時間。*p*是間隔開頭有效位數和*q*的間隔秒數有效位數。|  
|SQL_GUID|GUID|固定的長度的 GUID。|  
  
 [1] 這是在 DATA_TYPE 資料行呼叫所傳回的值**SQLGetTypeInfo**。  
  
 [2] 這是呼叫所傳回的名稱和建立參數的資料行中的值**SQLGetTypeInfo**。 名稱資料行傳回指定的 — 比方說，CHAR，而建立的參數資料行傳回的有效位數、 小數位數和長度等的建立參數以逗號分隔清單。  
  
 [3] 應用程式使用**SQLGetTypeInfo**或**SQLColAttribute**來判斷特定的資料類型或結果集內的特定資料行是否為不帶正負號。  
  
 [4] SQL_DECIMAL 和 SQL_NUMERIC 資料類型差異只在於其有效位數。 小數有效位數 (*p*，*s*) 會實作定義十進制有效位數的不少於*p*，而數值的有效位數 (*p*，*s*) 完全等於*p*。  
  
 [5] 取決於實作 SQL_FLOAT 的有效位數可以是 24 或 53： 如果它是 24，SQL_FLOAT 資料型別等同於 SQL_REAL;如果是 53，SQL_FLOAT 資料型別是 SQL_DOUBLE 相同。  
  
 [6] 在 ODBC 3*.x*，SQL 日期、 時間和時間戳記資料類型是 SQL_TYPE_DATE、 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，分別; 在 ODBC 2。*x*，資料類型為 SQL_DATE、 SQL_TIME 和 SQL_TIMESTAMP。  
  
 [7] 如需有關間隔 SQL 資料類型的詳細資訊，請參閱[間隔資料型別](../../../odbc/reference/appendixes/interval-data-types.md)稍後在本附錄 > 一節。  
  
 [8] SQL_BIT 資料類型以 sql-92 具有不同的特性與位元類型。  
  
 [9] 此資料類型以 sql-92 擁有任何對應的資料型別。  
  
 本節提供下列的範例。  
  
-   [範例 SQLGetTypeInfo 結果集](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)

