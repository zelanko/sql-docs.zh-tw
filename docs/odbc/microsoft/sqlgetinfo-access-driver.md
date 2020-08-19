---
description: SQLGetInfo (Access 驅動程式)
title: SQLGetInfo (Access 驅動程式) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Access Driver
- Access driver [ODBC], SQLGetInfo
ms.assetid: c226aba7-a2f4-4b32-b640-92654b40e5a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 11e725665171b85f994e45bc071b7cd2d9f01880
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421772"
---
# <a name="sqlgetinfo-access-driver"></a>SQLGetInfo (Access 驅動程式)
> [!NOTE]  
>  本主題提供存取驅動程式特定的資訊。 如需此函數的一般資訊，請參閱 [ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的適當主題。  
  
 **SQLGetInfo** 支援 SQL_FILE_USAGE 資訊類型。 傳回的值為16位整數，指出驅動程式如何直接處理資料來源中的檔案：  
  
-   SQL_FILE_NOT_SUPPORTED-驅動程式不是一層式驅動程式。  
  
-   SQL_FILE_TABLE-單一層驅動程式會將資料來源中的檔案視為資料表。  
  
-   SQL_FILE_QUALIFIER-單一層驅動程式會將資料來源中的檔案視為限定詞。  
  
 ODBC 驅動程式會傳回 SQL_FILE_QUALIFIER，因為每個檔案都是完整的資料庫。  
  
## <a name="sql_bookmark_persistence"></a>SQL_BOOKMARK_PERSISTENCE  
 SQL_BP_SCROLL &#124; SQL_BP_UPDATE [1]  
  
 [1] 書簽會在認可之後保存，但是在復原之後不會保存。  
  
## <a name="sql_convert_binary"></a>SQL_CONVERT_BINARY  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_char"></a>SQL_CONVERT_CHAR  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_date"></a>SQL_CONVERT_DATE  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_double"></a>SQL_CONVERT_DOUBLE  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_float"></a>SQL_CONVERT_FLOAT  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_integer"></a>SQL_CONVERT_INTEGER  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_longvarbinary"></a>SQL_CONVERT_LONGVARBINARY  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_longvarchar"></a>SQL_CONVERT_LONGVARCHAR  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_numeric"></a>SQL_CONVERT_NUMERIC  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_real"></a>SQL_CONVERT_REAL  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_smallint"></a>SQL_CONVERT_SMALLINT  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_time"></a>SQL_CONVERT_TIME  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_timestamp"></a>SQL_CONVERT_TIMESTAMP  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_tinyint"></a>SQL_CONVERT_TINYINT  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_varbinary"></a>SQL_CONVERT_VARBINARY  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_convert_varchar"></a>SQL_CONVERT_VARCHAR  
 SQL_CVT_DOUBLE &#124; SQL_CVT_FLOAT &#124; SQL_CVT_INTEGER &#124; SQL_CVT_NUMERIC &#124; SQL_CVT_REAL &#124; SQL_CVT_SMALLINT &#124; SQL_CVT_VARCHAR &#124; SQL_CVT_WVARCHAR  
  
## <a name="sql_union"></a>SQL_UNION  
 SQL_U_UNION_ALL &#124; SQL_U_UNION  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本號碼的格式|  
|----------|-------------|-------------------------------|  
|Microsoft Access|2.0|02.00.0000|  
||3.0|03.00.0000|  
||3.5|03.50.0000|  
||4.0|04.00.0000|  
  
> [!NOTE]  
>  不支援版本1.0 和1.1。 此外，Microsoft Access 版本3.0、7.0 和97中的資料格式沒有任何差異。  
  
## <a name="sql_ddl_index"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sql_getdata_extensions"></a>SQL_GETDATA_EXTENSIONS  
 SQL_GD_ANY_ORDER &#124; SQL_GD_ANY_COLUMN &#124; SQL_GD_BLOCK &#124; SQL_GD_BOUND  
  
## <a name="sql_keywords"></a>SQL_KEYWORDS  
 字母  
  
 AUTOINCREMENT  
  
 BINARY  
  
 BOOLEAN  
  
 BYTE  
  
 計數器  
  
 CURRENCY  
  
 DATABASE  
  
 DATABASE  
  
 DATETIME  
  
 禁止  
  
 DISTINCTROW  
  
 DOUBLEFLOAT  
  
 FLOAT4  
  
 FLOAT8  
  
 GENERAL  
  
 IEEEDOUBLE  
  
 IEEESINGLE  
  
 IGNORE  
  
 IMAGE  
  
 INTEGER1  
  
 INTEGER2  
  
 INTEGER4  
  
 邏輯  
  
 LOGICAL1  
  
 LONG  
  
 LONGBINARY  
  
 LONGCHAR  
  
 LONGTEXT  
  
 備忘錄  
  
 MONEY  
  
 注意  
  
 NUMBER  
  
 OLEOBJECT  
  
 OWNERACCESS  
  
 PARAMETERS  
  
 PERCENT  
  
 PIVOT  
  
 SHORT  
  
 單  
  
 SINGLEFLOAT  
  
 STDEV  
  
 STDEVP  
  
 STRING  
  
 TABLEID  
  
 TEXT  
  
 頂端  
  
 變換  
  
 UNSIGNEDBYTE  
  
 VAR  
  
 VARBINARY  
  
 VARP  
  
 YESNO  
  
## <a name="sql_numeric_functions"></a>SQL_NUMERIC_FUNCTIONS  
 SQL_FN_NUM_ABS &#124; SQL_FN_NUM_ATAN &#124; SQL_FN_NUM_CEILING &#124; SQL_FN_NUM_COS &#124; SQL_FN_NUM_EXP &#124; SQL_FN_NUM_FLOOR &#124; SQL_FN_NUM_LOG &#124; SQL_FN_NUM_MOD &#124; SQL_FN_NUM_POWER &#124; SQL_FN_NUM_RAND &#124; SQL_FN_NUM_SIGN &#124; SQL_FN_NUM_SIN &#124; SQL_FN_NUM_SQRT &#124; SQL_FN_NUM_TAN  
  
## <a name="sql_oj_capabilities"></a>SQL_OJ_CAPABILITIES  
 SQL_OJ_LEFT SQL_OJ_RIGHT SQL_OJ_NOT_ORDERED SQL_OJ_INNER SQL_OJ_ALL_COMPARISON_OPS  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION &#124; SQL_QU_PROCEDURE_INVOCATION  
  
## <a name="sql_scroll_options"></a>SQL_SCROLL_OPTIONS  
 SQL_SO_FORWARD_ONLY &#124; SQL_SO_STATIC &#124; SQL_SO_KEYSET_DRIVEN  
  
## <a name="sql_string_functions"></a>SQL_STRING_FUNCTIONS  
 SQL_FN_STR_ASCII &#124; SQL_FN_STR_CHAR &#124; SQL_FN_STR_CONCAT &#124; SQL_FN_STR_LCASE &#124; SQL_FN_STR_LEFT &#124; SQL_FN_STR_LENGTH &#124; SQL_FN_STR_LOCATE &#124; SQL_FN_STR_LOCATE_2 SQL_FN_STR_LTRIM &#124; SQL_FN_STR_RIGHT &#124; SQL_FN_STR_RTRIM &#124; SQL_FN_STR_SPACE &#124; SQL_FN_STR_SUBSTRING &#124; SQL_FN_STR_UCASE  
  
## <a name="sql_subqueries"></a>SQL_SUBQUERIES  
 SQL_SQ_COMPARISON &#124; SQL_SQ_EXISTS &#124; SQL_SQ_IN &#124; SQL_SQ_QUANTIFIED &#124; SQL_SQ_CORRELATED_SUBQUERIES  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
