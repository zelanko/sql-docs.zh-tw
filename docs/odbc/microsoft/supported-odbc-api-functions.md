---
title: 支援 ODBC API 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC, API functions
- ODBC SQL grammar, API functions mapped to driver (table) [ODBC]
ms.assetid: b28a8ed6-09b1-4acf-bf3e-f90bb32422de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec6ceaf57d8fe3c5325f85a9644cf4c8016663e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304099"
---
# <a name="supported-odbc-api-functions"></a>支援的 ODBC API 函式
平平的目的是通知應用程式驅動程式中可以使用哪些功能。 Microsoft ODBC 桌面資料庫驅動程式支援所有核心和 1 級功能。  
  
 有關函數和語法的符合性級別的詳細資訊,請參閱*ODBC 程式師參考中的*[「一致性級別](../../odbc/reference/develop-app/conformance-levels.md)」。。  
  
 對 ODBC API 功能的支援可以取決於所使用的驅動程式。 下表總結了對函數的支援。 最左側列提供指向每個函數的一般參考頁的連結。 這些參考頁按字母順序在[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)部分,在[ODBC 程式設計師的參考](../../odbc/reference/odbc-programmer-s-reference.md)下。 右側的列提供有關每個受支援函數的特定於驅動程序的說明的連結。 這些特定於驅動程式的主題列在每個驅動程式的「其他程式設計詳細資訊」 部分中。 或者,如果有關函數的相同註釋適用於所有 ODBC 桌面資料庫驅動程式,則最右側列提供指向一個主題的連結,該主題匯總了桌面資料庫驅動程式對該函數的支援。 這些主題列在當前部分的末尾("支援的ODBC API函數")。  
  
|ODBC 功能|存取特定於驅動程式的註解|dBASE 特定驅動程式的說明|悖論驅動程式指定註解|文字檔案驅動程式指定註解|Excel 特定於驅動程式的註解|與所有驅動程式相關的註解|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLColattributes](../../odbc/reference/syntax/sqlcolattributes-function.md)|[存取](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[存取](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[存取](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[dBASE](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[存取](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[dBASE](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[悖論](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[存取](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[存取](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[存取](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[SQLSet 連線選項](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[存取](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[dBASE](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursor 名稱](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[SQLSetScroll 選項](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[存取](../../odbc/microsoft/sqlstatistics-access-driver.md)|[dBASE](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[悖論](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[存取](../../odbc/microsoft/sqltables-access-driver.md)|[dBASE](../../odbc/microsoft/sqltables-dbase-driver.md)|[悖論](../../odbc/microsoft/sqltables-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)|[存取](../../odbc/microsoft/sqltransact-access-driver.md)|[dBASE](../../odbc/microsoft/sqltransact-dbase-driver.md)|[悖論](../../odbc/microsoft/sqltransact-paradox-driver.md)|[文字檔案](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 以下主題提供有關ODBC功能的註釋。 這些註釋適用於所有 ODBC 桌面資料庫驅動程式。  
  
-   [SQLGetData (桌面資料庫驅動程式)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption (桌面資料庫驅動程式)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (桌面資料庫驅動程式)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (桌面資料庫驅動程式)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (桌面資料庫驅動程式)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (桌面資料庫驅動程式)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
