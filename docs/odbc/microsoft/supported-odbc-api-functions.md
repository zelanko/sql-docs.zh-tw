---
title: 支援 ODBC API 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 460b1cb00f68e9b1940a1680625a173bc92e6f84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633398"
---
# <a name="supported-odbc-api-functions"></a>支援的 ODBC API 函式
調節的目的是通知應用程式所提供功能給它的驅動程式。 Microsoft ODBC 桌面資料庫驅動程式支援所有的核心和層級 1 的函式。  
  
 如需一致性層級函式和文法的詳細資訊，請參閱[一致性層級](../../odbc/reference/develop-app/conformance-levels.md)中*ODBC 程式設計人員參考*。  
  
 支援的 ODBC API 函式可能相依於使用的驅動程式。 下表摘要說明函式的支援。 最左邊的資料行提供每個函式的一般參考頁面的連結。 這些參考頁面會在依字母順序列出[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下方區段[ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。 右邊提供連結來驅動程式專屬附註，每個支援的函式的相關資料行。 這些驅動程式特定主題所述每個驅動程式的 [其他程式設計詳細資料] 區段。 或者，如果函數的相關的相同 「 註解套用到所有 ODBC 桌面資料庫驅動程式，最右側資料行提供摘要說明桌面資料庫驅動程式的支援，該函式的主題連結。 這些主題會列出目前的區段 （「 支援 ODBC API 函式 」） 的結尾。  
  
|ODBC 函數|存取驅動程式專屬附註|dBASE 驅動程式專屬資訊|Paradox 驅動程式專屬附註|文字檔案的驅動程式專屬附註|Excel 驅動程式專屬附註|所有驅動程式的相關資訊|  
|-------------------|-----------------------------------|----------------------------------|------------------------------------|--------------------------------------|----------------------------------|-----------------------------------|  
|[SQLBindParameter](../../odbc/reference/syntax/sqlbindparameter-function.md)|||||[Excel](../../odbc/microsoft/sqlbindparameter-excel-driver.md)||  
|[SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md)|[存取](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLColumns](../../odbc/reference/syntax/sqlcolattributes-function.md)|[存取](../../odbc/microsoft/sqlcolattributes-access-driver.md)|[dBASE](../../odbc/microsoft/sqlcolattributes-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlcolattributes-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlcolattributes-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlcolattributes-excel-driver.md)||  
|[SQLConfigDataSource](../../odbc/reference/syntax/sqlconfigdatasource-function.md)|[存取](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)|[dBASE](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)|[Excel](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)||  
|[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)|[存取](../../odbc/microsoft/sqldriverconnect-access-driver.md)|[dBASE](../../odbc/microsoft/sqldriverconnect-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqldriverconnect-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqldriverconnect-text-file-driver.md)|[Excel](../../odbc/microsoft/sqldriverconnect-excel-driver.md)||  
|[SQLGetCursorName](../../odbc/reference/syntax/sqlgetcursorname-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetcursorname-desktop-database-drivers.md)|  
|[SQLGetData](../../odbc/reference/syntax/sqlgetdata-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)|  
|[SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md)|[存取](../../odbc/microsoft/sqlgetinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgetinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgetinfo-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlgetinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgetinfo-excel-driver.md)|
|[SQLGetStmtOption](../../odbc/reference/syntax/sqlgetstmtoption-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)|  
|[SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md)|[存取](../../odbc/microsoft/sqlgettypeinfo-access-driver.md)|[dBASE](../../odbc/microsoft/sqlgettypeinfo-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlgettypeinfo-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlgettypeinfo-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlgettypeinfo-excel-driver.md)||  
|[SQLMoreResults](../../odbc/reference/syntax/sqlmoreresults-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)|  
|[SQLPrepare](../../odbc/reference/syntax/sqlprepare-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)|  
|[SQLProcedureColumns](../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|[存取](../../odbc/microsoft/sqlprocedurecolumns-access-driver.md)||||||  
|[SQLProcedures](../../odbc/reference/syntax/sqlprocedures-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)|  
|[SQLSetConnectOption](../../odbc/reference/syntax/sqlsetconnectoption-function.md)|[存取](../../odbc/microsoft/sqlsetconnectoption-access-driver.md)|[dBASE](../../odbc/microsoft/sqlsetconnectoption-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlsetconnectoption-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlsetconnectoption-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlsetconnectoption-excel-driver.md)||  
|[SQLSetCursorName](../../odbc/reference/syntax/sqlsetcursorname-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)|  
|[SQLSetPos](../../odbc/reference/syntax/sqlsetpos-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)|  
|[SQLSetScrollOptions](../../odbc/reference/syntax/sqlsetscrolloptions-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)|  
|[SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)|  
|[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)||||||[所有驅動程式](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)|  
|[SQLStatistics](../../odbc/reference/syntax/sqlstatistics-function.md)|[存取](../../odbc/microsoft/sqlstatistics-access-driver.md)|[dBASE](../../odbc/microsoft/sqlstatistics-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqlstatistics-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqlstatistics-text-file-driver.md)|[Excel](../../odbc/microsoft/sqlstatistics-excel-driver.md)||  
|[SQLTables](../../odbc/reference/syntax/sqltables-function.md)|[存取](../../odbc/microsoft/sqltables-access-driver.md)|[dBASE](../../odbc/microsoft/sqltables-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltables-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqltables-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltables-excel-driver.md)|  
|[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)|[存取](../../odbc/microsoft/sqltransact-access-driver.md)|[dBASE](../../odbc/microsoft/sqltransact-dbase-driver.md)|[Paradox](../../odbc/microsoft/sqltransact-paradox-driver.md)|[文字檔](../../odbc/microsoft/sqltransact-text-file-driver.md)|[Excel](../../odbc/microsoft/sqltransact-excel-driver.md)||  
  
 下列主題提供有關 ODBC 函式的 < 備註 >。 這些註解套用到所有 ODBC 桌面資料庫驅動程式。  
  
-   [SQLGetData (桌面資料庫驅動程式)](../../odbc/microsoft/sqlgetdata-desktop-database-drivers.md)  
  
-   [SQLGetStmtOption(Desktop Database Drivers)](../../odbc/microsoft/sqlgetstmtoption-desktop-database-drivers.md)  
  
-   [SQLMoreResults (桌面資料庫驅動程式)](../../odbc/microsoft/sqlmoreresults-desktop-database-drivers.md)  
  
-   [SQLPrepare (桌面資料庫驅動程式)](../../odbc/microsoft/sqlprepare-desktop-database-drivers.md)  
  
-   [SQLProcedures (桌面資料庫驅動程式)](../../odbc/microsoft/sqlprocedures-desktop-database-drivers.md)  
  
-   [SQLSetCursorName (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetcursorname-desktop-database-drivers.md)  
  
-   [SQLSetPos (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetpos-desktop-database-drivers.md)  
  
-   [SQLSetScrollOptions (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetscrolloptions-desktop-database-drivers.md)  
  
-   [SQLSetStmtOption (桌面資料庫驅動程式)](../../odbc/microsoft/sqlsetstmtoption-desktop-database-drivers.md)  
  
-   [SQLSpecialColumns (桌面資料庫驅動程式)](../../odbc/microsoft/sqlspecialcolumns-desktop-database-drivers.md)
