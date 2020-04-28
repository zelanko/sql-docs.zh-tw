---
title: SQLGetInfo （Excel 驅動程式） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Excel Driver
ms.assetid: fed4aea2-6d3d-4199-a5db-3d033eb63927
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0a96b135bbd8d44b82e645fac59ddea795666f3f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298578"
---
# <a name="sqlgetinfo-excel-driver"></a>SQLGetInfo (Excel 驅動程式)
> [!NOTE]  
>  本主題提供 Excel 驅動程式特有的資訊。 如需此函數的一般資訊，請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)底下的適當主題。  
  
 **SQLGetInfo**支援 SQL_FILE_USAGE 資訊類型。 傳回的值是16位整數，表示驅動程式如何直接處理資料來源中的檔案：  
  
-   SQL_FILE_NOT_SUPPORTED-驅動程式不是一層式驅動程式。  
  
-   SQL_FILE_TABLE-一層式驅動程式會將資料來源中的檔案視為資料表。  
  
-   SQL_FILE_QUALIFIER-一層式驅動程式會將資料來源中的檔案視為辨識符號。  
  
 ODBC 驅動程式會傳回 Microsoft Exceldriver 的 SQL_FILE_TABLE，因為每個檔案都是一個資料表。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本號碼的格式|  
|----------|-------------|-------------------------------|  
|Microsoft Excel|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0/7。0|05.00.0000|  
||97/2000|08.00.0000|  
  
## <a name="sql_file_usage"></a>SQL_FILE_USAGE  
 SQL_FILE_TABLE （Excel 3.0/4.0）  
  
 SQL_FILE_CATALOG （Excel 5.0/7.0）  
  
## <a name="sql_max_char_literal_len"></a>SQL_MAX_CHAR_LITERAL_LEN  
 255（Excel 3.0/4.0/5.0/7.0）  
  
 65535（Excel 97）  
  
## <a name="sql_max_column_name_len"></a>SQL_MAX_COLUMN_NAME_LEN  
 30（Excel 3.0/4.0）  
  
 64（Excel 5.0/7.0/97）  
  
## <a name="sql_max_table_name_len"></a>SQL_MAX_TABLE_NAME_LEN  
 12（Excel 3.0/4.0）  
  
 31（Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_name_separator"></a>SQL_CATALOG_NAME_SEPARATOR  
 "\\" （Excel 3.0/4.0）  
  
 "."（Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_term"></a>SQL_CATALOG_TERM  
 "Directory" （Excel 3.0/4.0）  
  
 「活頁簿」（Excel 5.0/7.0/97）  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
