---
title: SQLGetInfo （Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14837bc5ba3368fbb0d33680ee1c54936ab0a224
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898852"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 支援：完整  
  
 ODBC API 一致性：層級1  
  
 傳回與連接控制碼（ *hdbc*）相關聯之 VISUAL FoxPro ODBC 驅動程式和資料來源的一般資訊。 下列清單顯示 Visual FoxPro ODBC Driver 針對每個*fInfoType*引數所傳回的值，以及有關傳回值的批註。  
  
 如需詳細資訊，請參閱 ODBC 程式設計*人員參考*中的[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) 。  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES 會傳回 ' N '。  
  
 SQL_ACCESSIBLE_TABLES 會傳回 ' Y '。  
  
 SQL_ACTIVE_CONNECTIONS 會傳回0。  
  
 SQL_ACTIVE_STATEMENTS 會傳回0。  
  
 SQL_ALTER_TABLE 會傳回 SQL_AT_ADD_COLUMN 或 SQL_AT_DROP_COLUMN。  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE 會傳回 SQL_BP_SCROLL。  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS 會傳回 ' Y '。  
  
 SQL_CONCAT_Null_BEHAVIOR 會傳回 SQL_CB_Null。  
  
 SQL_CONVERT_BIGINT 會傳回0。 Visual FoxPro ODBC 驅動程式不支援*BigInt*。  
  
 SQL_CONVERT_BINARY 會傳回0。  
  
 SQL_CONVERT_BIT 會傳回0。  
  
 SQL_CONVERT_CHAR 會傳回0。  
  
 SQL_CONVERT_DATE 會傳回0。  
  
 SQL_CONVERT_DECIMAL 會傳回0。  
  
 SQL_CONVERT_DOUBLE 會傳回0。  
  
 SQL_CONVERT_FLOAT 會傳回0。  
  
 SQL_CONVERT_INTEGER 會傳回0。  
  
 SQL_CONVERT_LONGVARBINARY 會傳回0。  
  
 SQL_CONVERT_LONGVARCHAR 會傳回0。  
  
 SQL_CONVERT_NUMERIC 會傳回0。  
  
 SQL_CONVERT_REAL 會傳回0。  
  
 SQL_CONVERT_SMALLINT 會傳回0。  
  
 SQL_CONVERT_TIME 會傳回0。  
  
 SQL_CONVERT_TIMESTAMP 會傳回0。  
  
 SQL_CONVERT_TINYINT 會傳回0。  
  
 SQL_CONVERT_VARBINARY 會傳回0。  
  
 SQL_CONVERT_VARCHAR 會傳回0。  
  
 SQL_CONVERT_FUNCTIONS 會傳回0。  
  
 SQL_CORRELATION_NAME 會傳回 SQL_CN_ANY。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR 會傳回 SQL_CB_PRESERVE。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR 會傳回 SQL_CB_PRESERVE。  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME 會傳回以 DSN 形式傳遞給[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)的值。如果未指定任何 DSN，則會傳回空字串。  
  
 SQL_DATA_SOURCE_READ_ONLY 會傳回 ' N '。  
  
 如果資料來源是[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)，SQL_DATABASE_NAME 會傳回目前資料庫的完整 UNC 路徑。 如果資料來源連接到[資料表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄，此函數會傳回目錄的路徑。  
  
 SQL_DBMS_NAME 會傳回 "Visual FoxPro"。  
  
 SQL_DBMS_VER 會傳回 "03.00.0000"。  
  
 SQL_DEFAULT_TXN_ISOLATION 會傳回 SQL_TXN_READ_COMMITTED。 不可能進行中途讀取，但不可重複讀取和幻像是可行的。  
  
 SQL_DRIVER_HDBC 是由驅動程式管理員所執行。  
  
 SQL_DRIVER_HENV 是由驅動程式管理員所執行。  
  
 SQL_DRIVER_HLIB 是由驅動程式管理員所執行。  
  
 SQL_DRIVER_HSTMT 是由驅動程式管理員所執行。  
  
 SQL_DRIVER_NAME 會傳回 "vfpodbc"。  
  
 SQL_DRIVER_ODBC_VER 會傳回 "02.50" （SQL_SPEC_MAJOR，SQL_SPEC_MINOR）。  
  
 SQL_DRIVER_VER 會傳回 "01.00.0000"。  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY 會傳回 ' N '。  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION 會傳回：  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK。  
  
 SQL_FILE_USAGE 會傳回資料庫（. dbc 檔案）和免費資料表（.dbf 檔案）資料來源的 SQL_FILE_QUALIFIER。  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS 會傳回：  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY 會傳回 SQL_GB_NO_RELATION。  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE 會傳回 SQL_IC_MIXED。  
  
 SQL_IDENTIFIER_QUOTE_CHAR 傳回 '。  
  
## <a name="k"></a>K  
 SQL_KEYWORDS 會傳回 ""。  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE 會傳回 ' N '。  
  
 SQL_LOCK_TYPES 會傳回 SQL_LCK_NO_CHANGE。  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN 會傳回0。  
  
 SQL_MAX_CHAR_LITERAL_LEN 傳回254。  
  
 SQL_MAX_COLUMN_NAME_LEN 傳回128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY 會傳回16。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY 會傳回16。  
  
 SQL_MAX_COLUMNS_IN_INDEX 會傳回0。  
  
 SQL_MAX_COLUMNS_IN_SELECT 傳回254。  
  
 SQL_MAX_COLUMNS_IN_TABLE 傳回254。  
  
 SQL_MAX_CURSOR_NAME_LEN 傳回254。  
  
 SQL_MAX_INDEX_SIZE 會傳回0。  
  
 SQL_MAX_OWNER_NAME_LEN 會傳回0。  
  
 SQL_MAX_PROCEDURE_NAME_LEN 會傳回0。 Visual FoxPro ODBC 驅動程式不允許直接存取 Visual FoxPro 預存程式。  
  
 SQL_MAX_QUALIFIER_NAME_LEN 會傳回最大的作業系統路徑長度。  
  
 SQL_MAX_ROW_SIZE 會傳回 254 ^ 2。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG 會傳回 ' N '。  
  
 SQL_MAX_STATEMENT_LEN 傳回8192。  
  
 SQL_MAX_TABLE_NAME_LEN 傳回128。  
  
 SQL_MAX_TABLES_IN_SELECT 會傳回16。  
  
 SQL_MAX_USER_NAME_LEN 會傳回0。  
  
 SQL_MULT_RESULT_SETS 會傳回 ' Y '。  
  
 SQL_MULTIPLE_ACTIVE_TXN 會傳回 ' Y '。 多個連接可以同時開啟數個交易。  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN 會傳回 ' N '。  
  
 SQL_NON_NullABLE_COLUMNS 會傳回 SQL_NNC_NON_Null。  
  
 SQL_Null_COLLATION 會傳回 SQL_NC_LOW。  
  
 SQL_NUMERIC_FUNCTIONS 會傳回 SQL_FN_NUM_POWER 以外的所有函式，但 Visual FoxPro ODBC 驅動程式不支援此功能。 支援下列功能：  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE 會傳回 SQL_OAC_LEVEL1。  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE 會傳回 SQL_OSCC_COMPLIANT。  
  
 SQL_ODBC_SQL_CONFORMANCE 會傳回 SQL_OSC_MINIMUM。 支援最小的 SQL 語法。  
  
 SQL_ODBC_SQL_OPT_IEF 會傳回 "N"。  
  
 SQL_ODBC_VER 是由驅動程式管理員所執行。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT 會傳回 "N"。  
  
 SQL_OUTER_JOINS 會傳回 "N"。  
  
 SQL_OWNER_TERM 會傳回 ""。 Visual FoxPro ODBC 驅動程式不支援其物件的擁有者。  
  
 SQL_OWNER_USAGE 會傳回0。 Visual FoxPro ODBC 驅動程式不支援其物件的擁有者。  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS 會傳回 SQL_POS_POSITION。  
  
 SQL_POSITIONED_STATEMENTS 會傳回0。  
  
 SQL_PROCEDURE_TERM 會傳回 ""。  
  
 SQL_PROCEDURES 會傳回 ' N '。  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION 會傳回 SQL_QL_START。  
  
 SQL_QUALIFIER_NAME_SEPARATOR 傳回 '！ ' 或 '\\'。 資料庫與資料表之間的分隔符號是連接到[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)之資料來源的 '！ '，而\\如果是[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)目錄的資料來源，則為 ' '。  
  
 SQL_QUALIFIER_TERM 會傳回 "database" 或 "directory"。 對於連接到[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源，限定詞是「資料庫」，而「目錄」則是[免費資料表](../../odbc/microsoft/visual-foxpro-terminology.md)目錄的資料來源。  
  
 SQL_QUALIFIER_USAGE 不支援 SQL_QU_PRIVILEGE_DEFINITION;它會傳回 SQL_QU_DML_STATEMENT 或 SQL_QU_TABLE_DEFINITION。  
  
 SQL_QUOTED_IDENTIFIER_CASE 會傳回 SQL_IC_MIXED。  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES 會傳回 "N"。 Visual FoxPro ODBC 驅動程式只支援靜態和轉送資料指標。  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY 會傳回 SQL_SCCO_READ_ONLY。  
  
 SQL_SCROLL_OPTIONS 會傳回 SQL_SO_STATIC 或 SQL_SO_READONLY。  
  
 SQL_SEARCH_PATTERN_ESCAPE 會傳回\\""。  
  
 SQL_SERVER_NAME 會傳回 ""。  
  
 SQL_SPECIAL_CHARACTERS 會傳回 "~ @ # $% ^"。  
  
 SQL_STATIC_SENSITIVITY 會傳回0。 Visual FoxPro ODBC 驅動程式不支援位置更新。  
  
 SQL_STRING_FUNCTIONS 不支援 SQL_FN_STR_INSERT、SQL_FN_STR_LOCATE、SQL_FN_STR_LOCATE_2 或 SQL_FN_STR_SOUNDEX。  
  
 它會傳回：  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE。  
  
 SQL_SUBQUERIES 會傳回：  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED。  
  
 SQL_SYSTEM_FUNCTIONS 會傳回：  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNull  
  
 但不是：  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM 會傳回 "TABLE"。  
  
 SQL_TIMEDATE_ADD_INTERVALS 會傳回：  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 但不是：  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS 會傳回：  
  
-   SQL_FN_TSI_ 秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS 不支援 SQL_FN_TD_QUARTER、SQL_FN_TD_TIMESTAMPADD、SQL_FN_TD_DAYOFYEAR 或 SQL_FN_TD_WEEK。  
  
 它會傳回：  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR。  
  
 SQL_TXN_CAPABLE 會傳回 SQL_TC_DML。  
  
 SQL_TXN_ISOLATION_OPTION 會傳回 SQL_TXN_READ_COMMITTED。  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION 會傳回 SQL_U_UNION 或 SQL_U_UNION_ALL。  
  
 SQL_USER_NAME 會\<傳回空白>。
