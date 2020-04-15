---
title: SQLGetInfo (視覺福克斯Pro ODBC驅動程式) |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295188"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援: 完整  
  
 ODBC API 符合性:1 級  
  
 返回有關 Visual FoxPro ODBC 驅動程式和與連接句柄*hdbc*關聯的數據源的一般資訊。 下面的清單顯示了 Visual FoxPro ODBC 驅動程式為每個*fInfoType*參數返回的值,以及有關返回值的註釋。  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLGetInfo。](../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
## <a name="a"></a>A  
 SQL_ACCESSIBLE_PROCEDURES返回"N"。  
  
 SQL_ACCESSIBLE_TABLES返回"Y"。  
  
 SQL_ACTIVE_CONNECTIONS返回 0。  
  
 SQL_ACTIVE_STATEMENTS返回 0。  
  
 SQL_ALTER_TABLE返回SQL_AT_ADD_COLUMN或SQL_AT_DROP_COLUMN。  
  
## <a name="b"></a>B  
 SQL_BOOKMARK_PERSISTENCE返回SQL_BP_SCROLL。  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR返回SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINT返回 0。 視覺福克斯Pro ODBC驅動程式不支援*Bigint。*  
  
 SQL_CONVERT_BINARY返回 0。  
  
 SQL_CONVERT_BIT返回 0。  
  
 SQL_CONVERT_CHAR返回 0。  
  
 SQL_CONVERT_DATE返回 0。  
  
 SQL_CONVERT_DECIMAL返回 0。  
  
 SQL_CONVERT_DOUBLE返回 0。  
  
 SQL_CONVERT_FLOAT返回 0。  
  
 SQL_CONVERT_INTEGER返回 0。  
  
 SQL_CONVERT_LONGVARBINARY返回 0。  
  
 SQL_CONVERT_LONGVARCHAR返回 0。  
  
 SQL_CONVERT_NUMERIC返回 0。  
  
 SQL_CONVERT_REAL返回 0。  
  
 SQL_CONVERT_SMALLINT返回 0。  
  
 SQL_CONVERT_TIME返回 0。  
  
 SQL_CONVERT_TIMESTAMP返回 0。  
  
 SQL_CONVERT_TINYINT返回 0。  
  
 SQL_CONVERT_VARBINARY返回 0。  
  
 SQL_CONVERT_VARCHAR返回 0。  
  
 SQL_CONVERT_FUNCTIONS返回 0。  
  
 SQL_CORRELATION_NAME返回SQL_CN_ANY。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR返回SQL_CB_PRESERVE。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR返回SQL_CB_PRESERVE。  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME返回作為 DSN 傳遞到[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)的值 ,或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md);如果未指定 DSN,則返回空字串。  
  
 SQL_DATA_SOURCE_READ_ONLY返回"N"。  
  
 如果數據源是[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md),SQL_DATABASE_NAME將完整的 UNC 路徑傳回到當前資料庫。 如果數據源連接到[表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄,則函數將路徑返回到該目錄。  
  
 SQL_DBMS_NAME返回"視覺福克斯專業"。  
  
 SQL_DBMS_VER返回"03.00.0000"。  
  
 SQL_DEFAULT_TXN_ISOLATION返回SQL_TXN_READ_COMMITTED。 髒讀是不可能的,但不可重複讀取和幻象是可能的。  
  
 SQL_DRIVER_HDBC由驅動程式管理器實施。  
  
 SQL_DRIVER_HENV由驅動程式管理員實施。  
  
 SQL_DRIVER_HLIB由驅動程式管理員實現。  
  
 SQL_DRIVER_HSTMT由驅動程式管理員實施。  
  
 SQL_DRIVER_NAME返回「vfpodbc.dll」。。  
  
 SQL_DRIVER_ODBC_VER返回"02.50"(SQL_SPEC_MAJOR,SQL_SPEC_MINOR)。  
  
 SQL_DRIVER_VER返回"01.00.0000"。  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY返回"N"。  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION返回:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK  
  
 SQL_FILE_USAGE傳回資料庫 (.dbc 檔案) 和可用表格 (.dbf 檔案) 資料來源SQL_FILE_QUALIFIER。  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS返回:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY返回SQL_GB_NO_RELATION。  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE返回SQL_IC_MIXED。  
  
 SQL_IDENTIFIER_QUOTE_CHAR返回'  
  
## <a name="k"></a>K  
 SQL_KEYWORDS返回""。  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE返回"N"。  
  
 SQL_LOCK_TYPES返回SQL_LCK_NO_CHANGE。  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN返回 0。  
  
 SQL_MAX_CHAR_LITERAL_LEN返回 254。  
  
 SQL_MAX_COLUMN_NAME_LEN返回 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY返回 16。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY返回 16。  
  
 SQL_MAX_COLUMNS_IN_INDEX返回 0。  
  
 SQL_MAX_COLUMNS_IN_SELECT返回 254。  
  
 SQL_MAX_COLUMNS_IN_TABLE返回 254。  
  
 SQL_MAX_CURSOR_NAME_LEN返回 254。  
  
 SQL_MAX_INDEX_SIZE返回 0。  
  
 SQL_MAX_OWNER_NAME_LEN返回 0。  
  
 SQL_MAX_PROCEDURE_NAME_LEN返回 0。 Visual FoxPro ODBC 驅動程式不允許直接存取 Visual FoxPro 儲存過程。  
  
 SQL_MAX_QUALIFIER_NAME_LEN返回最大操作系統路徑長度。  
  
 SQL_MAX_ROW_SIZE返回 254......(2) 。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG返回"N"。  
  
 SQL_MAX_STATEMENT_LEN返回 8192。  
  
 SQL_MAX_TABLE_NAME_LEN返回 128。  
  
 SQL_MAX_TABLES_IN_SELECT返回 16。  
  
 SQL_MAX_USER_NAME_LEN返回 0。  
  
 SQL_MULT_RESULT_SETS返回"Y"。  
  
 SQL_MULTIPLE_ACTIVE_TXN返回"Y"。 多個連接可以同時打開多個事務。  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN返回"N"。  
  
 SQL_NON_NULLABLE_COLUMNS返回SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION返回SQL_NC_LOW。  
  
 SQL_NUMERIC_FUNCTIONS返回除 SQL_FN_NUM_POWER之外的所有功能,該功能不受 Visual FoxPro ODBC 驅動程式的支援。 支援以下功能:  
  
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
 SQL_ODBC_API_CONFORMANCE返回SQL_OAC_LEVEL1。  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE返回SQL_OSCC_COMPLIANT。  
  
 SQL_ODBC_SQL_CONFORMANCE返回SQL_OSC_MINIMUM。 支援最小 SQL 語法。  
  
 SQL_ODBC_SQL_OPT_IEF返回"N"。  
  
 SQL_ODBC_VER由驅動程式管理員實施。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT返回"N"。  
  
 SQL_OUTER_JOINS返回"N"。  
  
 SQL_OWNER_TERM返回"" Visual FoxPro ODBC 驅動程式不支援其物件的擁有者。  
  
 SQL_OWNER_USAGE返回 0。 Visual FoxPro ODBC 驅動程式不支援其物件的擁有者。  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS返回SQL_POS_POSITION。  
  
 SQL_POSITIONED_STATEMENTS返回 0。  
  
 SQL_PROCEDURE_TERM返回""。  
  
 SQL_PROCEDURES返回"N"。  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION返回SQL_QL_START。  
  
 SQL_QUALIFIER_NAME_SEPARATOR返回"!"或""。\\ 資料庫和表之間的分隔符是連接到[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的數據源的"!",對於作為[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)\\目錄的數據源 的"!"。  
  
 SQL_QUALIFIER_TERM返回"資料庫"或"目錄"。 限定符是連接到[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)的資料來源的資料庫,是[作為可用表](../../odbc/microsoft/visual-foxpro-terminology.md)目錄的資料來源的「目錄」。  
  
 SQL_QUALIFIER_USAGE不支援SQL_QU_PRIVILEGE_DEFINITION;它返回SQL_QU_DML_STATEMENT或SQL_QU_TABLE_DEFINITION。  
  
 SQL_QUOTED_IDENTIFIER_CASE返回SQL_IC_MIXED。  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES返回"N"。 可視化 FoxPro ODBC 驅動程式僅支援靜態和正向游標。  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY返回SQL_SCCO_READ_ONLY。  
  
 SQL_SCROLL_OPTIONS返回SQL_SO_STATIC或SQL_SO_READONLY。  
  
 SQL_SEARCH_PATTERN_ESCAPE返回"\\  
  
 SQL_SERVER_NAME返回""。  
  
 SQL_SPECIAL_CHARACTERS返回"[$%]"。  
  
 SQL_STATIC_SENSITIVITY返回 0。 可視化 FoxPro ODBC 驅動程式不支援位置更新。  
  
 SQL_STRING_FUNCTIONS不支援SQL_FN_STR_INSERT、SQL_FN_STR_LOCATE、SQL_FN_STR_LOCATE_2或SQL_FN_STR_SOUNDEX。  
  
 傳回的會是：  
  
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
  
-   SQL_FN_STR_SPACE  
  
 SQL_SUBQUERIES返回:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED  
  
 SQL_SYSTEM_FUNCTIONS返回:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 但不是:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM返回"表"。  
  
 SQL_TIMEDATE_ADD_INTERVALS返回:  
  
-   SQL_FN_TSI_秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 但不是:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS返回:  
  
-   SQL_FN_TSI_秒  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS不支援SQL_FN_TD_QUARTER、SQL_FN_TD_TIMESTAMPADD、SQL_FN_TD_DAYOFYEAR或SQL_FN_TD_WEEK。  
  
 傳回的會是：  
  
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
  
-   SQL_FN_TD_YEAR 。  
  
 SQL_TXN_CAPABLE返回SQL_TC_DML。  
  
 SQL_TXN_ISOLATION_OPTION返回SQL_TXN_READ_COMMITTED。  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION返回SQL_U_UNION或SQL_U_UNION_ALL。  
  
 SQL_USER_NAME返回\<空>。
