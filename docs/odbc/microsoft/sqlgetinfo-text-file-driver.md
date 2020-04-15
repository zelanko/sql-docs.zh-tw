---
title: SQLGetInfo(文字檔案驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09ca2e42e20a6f314de3b68fe5d5b143f41269c3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298499"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (文字檔驅動程式)
> [!NOTE]  
>  本主題提供特定於文本檔驅動程序的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 **SQLGetInfo**支援SQL_FILE_USAGE信息類型。 傳回的值是一個 16 位元整數,指示驅動程式如何處理資料來源中的檔案:  
  
-   SQL_FILE_NOT_SUPPORTED - 驅動程式不是單層驅動程式。  
  
-   SQL_FILE_TABLE - 單層驅動程式將資料來源中的檔案視為表。  
  
-   SQL_FILE_QUALIFIER - 單層驅動程式將資料來源中的檔案視為修飾詞。  
  
 ODBC 驅動程式返回文本驅動程式的SQL_FILE_TABLE,因為每個檔都是一個表。  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|版本|版本號的格式|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS&#124;SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE SQL_FN_TD_WEEK SQL_FN_TD_SECOND SQL_FN_TD_NOW SQL_FN_TD_MONTH &#124; SQL_FN_TD_MINUTE SQL_FN_TD_HOUR &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_DAYOFMONTH &#124;&#124;SQL_FN_TD_CURTIMESQL_FN_TD_DAYOFWEEKSQL_FN_TD_DAYOFWEEK&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124;&#124; &#124;SQL_FN_TD_YEAR
