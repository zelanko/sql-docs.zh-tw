---
title: "SQLGetInfo (dBASE 驅動程式) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetInfo
ms.assetid: 42ffdc9c-281b-4df5-ac6d-7b34f15ecd4c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d79bc7a4f83c3c5eccc69bebc1e8f5c29ffe6ac3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-dbase-driver"></a>SQLGetInfo (dBASE 驅動程式)
> [!NOTE]  
>  本主題提供 dBASE 驅動程式特定資訊。 如需此函式的一般資訊，請參閱底下的適當主題[ODBC 應用程式開發介面參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLGetInfo**支援 SQL_FILE_USAGE 資訊類型。 傳回的值是 16 位元的整數，表示驅動程式如何直接處理的資料來源中的檔案：  
  
-   SQL_FILE_NOT_SUPPORTED — 驅動程式不是單層驅動程式。  
  
-   SQL_FILE_TABLE — 單層驅動程式將資料來源中的檔案視為資料表。  
  
-   SQL_FILE_QUALIFIER — 單層驅動程式辨識符號視為資料來源中的檔案。  
  
 ODBC 驅動程式會傳回 SQL_FILE_TABLE，因為每個檔案是一個資料表。  
  
## <a name="sqlaltertable"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124;SQL_AT_DROP_COLUMN  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Version|版本號碼的格式|  
|----------|-------------|-------------------------------|  
|DBASE|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0|05.00.0000|  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124;SQL_QU_TABLE_DEFINITION &#124;SQL_QU_INDEX_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124;SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124;SQL_FN_TD_MINUTE &#124;SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124;SQL_FN_TD_WEEK &#124;SQL_FN_TD_YEAR

