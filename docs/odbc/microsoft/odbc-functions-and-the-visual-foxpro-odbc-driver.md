---
title: ODBC 函式和 Visual FoxPro ODBC Driver |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- ODBC level 1 API functions [ODBC]
- functions [ODBC], API
- ODBC API functions [ODBC]
- level 1 API functions [ODBC]
- API functions [ODBC]
- core level API functions [ODBC]
- level 2 API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 512f9cee-ffad-439b-b612-b49c34c32658
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 260630321825a695b4f1d701f18fff08551ff673
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363528"
---
# <a name="odbc-functions-and-the-visual-foxpro-odbc-driver"></a>ODBC 函式和 Visual FoxPro ODBC Driver
本節中的主題提供 ODBC API 函式及任何 Visual FoxPro 特定詳細資料的簡短摘要。  
  
> [!NOTE]  
>  如需 ODBC 函式的一般資訊，請參閱《 ODBC 程式設計人員指南》中的[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 ODBC API 函式已分成三個主要類別：核心層級 API 函式、層級 1 API 函式和層級 2 API 函式。  
  
> [!NOTE]  
>  有幾個函式的行為不同，端視資料來源是否定義為[可用資料表](../../odbc/microsoft/visual-foxpro-terminology.md)（.dbf 檔案）目錄的連接，或與 Visual FoxPro[資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)（dbc 檔案）的關係而定。 只有資料庫連接支援某些作業。  
  
## <a name="core-level-api-support"></a>核心層級 API 支援  
 下表列出 ODBC 核心層級 API 函數。 Visual FoxPro ODBC 驅動程式支援所有這些功能。  

:::row:::
    :::column:::
        [SQLAllocConnect](../../odbc/microsoft/sqlallocconnect-visual-foxpro-odbc-driver.md)  
        [SQLAllocEnv](../../odbc/microsoft/sqlallocenv-visual-foxpro-odbc-driver.md)  
        [SQLAllocStmt](../../odbc/microsoft/sqlallocstmt-visual-foxpro-odbc-driver.md)  
        [SQLBindCol](../../odbc/microsoft/sqlbindcol-visual-foxpro-odbc-driver.md)  
        [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)  
        [SQLColAttributes](../../odbc/microsoft/sqlcolattributes-visual-foxpro-odbc-driver.md)  
        [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)  
        [SQLDescribeCol](../../odbc/microsoft/sqldescribecol-visual-foxpro-odbc-driver.md)  
        [SQLDisconnect](../../odbc/microsoft/sqldisconnect-visual-foxpro-odbc-driver.md)  
        [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)  
        [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)  
    :::column-end:::
    :::column:::
        [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)  
        [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)  
        [SQLFreeConnect](../../odbc/microsoft/sqlfreeconnect-visual-foxpro-odbc-driver.md)  
        [SQLFreeEnv](../../odbc/microsoft/sqlfreeenv-visual-foxpro-odbc-driver.md)  
        [SQLFreeStmt](../../odbc/microsoft/sqlfreestmt-visual-foxpro-odbc-driver.md)  
        [SQLGetCursorName](../../odbc/microsoft/sqlgetcursorname-visual-foxpro-odbc-driver.md)  
        [SQLNumResultCols](../../odbc/microsoft/sqlnumresultcols-visual-foxpro-odbc-driver.md)  
        [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)  
        [SQLRowCount](../../odbc/microsoft/sql-row-count-visual-foxpro-odbc-driver.md)  
        [SQLSetCursorName](../../odbc/microsoft/sqlsetcursorname-visual-foxpro-odbc-driver.md)  
        [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)  
    :::column-end:::
:::row-end:::

## <a name="level-1-api-support"></a>層級 1 API 支援  
 下表列出 ODBC 層級 1 API 函數。 所有這些函式都是 Visual FoxPro ODBC 驅動程式的完整或部分支援的功能。  

:::row:::
    :::column:::
        [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)  
        [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)  
        [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)  
        [SQLGetConnectOption](../../odbc/microsoft/sqlgetconnectoption-visual-foxpro-odbc-driver.md)  
        [SQLGetData](../../odbc/microsoft/sqlgetdata-visual-foxpro-odbc-driver.md)  
        [SQLGetFunctions](../../odbc/microsoft/sqlgetfunctions-visual-foxpro-odbc-driver.md)  
        [SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md)  
        [SQLGetStmtOption](../../odbc/microsoft/sqlgetstmtoption-visual-foxpro-odbc-driver.md)  
    :::column-end:::
    :::column:::
        [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)  
        [SQLParamData](../../odbc/microsoft/sqlparamdata-visual-foxpro-odbc-driver.md)  
        [SQLPutData](../../odbc/microsoft/sqlputdata-visual-foxpro-odbc-driver.md)  
        [SQLSetConnectOption](../../odbc/microsoft/sqlsetconnectoption-visual-foxpro-odbc-driver.md)  
        [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
        [SQLSpecialColumns](../../odbc/microsoft/sqlspecialcolumns-visual-foxpro-odbc-driver.md)  
        [SQLStatistics](../../odbc/microsoft/sqlstatistics-visual-foxpro-odbc-driver.md)  
        [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)  
    :::column-end:::
:::row-end:::

## <a name="level-2-api-support"></a>層級 2 API 支援  
 以下是完整或部分支援的 ODBC 層級 2 API 函式：  
  
-   [SQLDataSources](../../odbc/microsoft/sqldatasources-visual-foxpro-odbc-driver.md)  
  
-   [SQLDrivers](../../odbc/microsoft/sqldrivers-visual-foxpro-odbc-driver.md)  
  
-   [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)  
  
-   [SQLMoreResults](../../odbc/microsoft/sqlmoreresults-visual-foxpro-odbc-driver.md)  
  
-   [SQLNumParams](../../odbc/microsoft/sqlnumparams-visual-foxpro-odbc-driver.md)  
  
-   [SQLParamOptions](../../odbc/microsoft/sqlparamoptions-visual-foxpro-odbc-driver.md)  
  
-   [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetPos](../../odbc/microsoft/sqlsetpos-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) （部分支援）  
  
 不支援下列層級 2 API 函式：  
  
-   SQLBrowseConnect  
  
-   SQLColumnPrivileges  
  
-   SQLDescribeParam  
  
-   SQLForeignKeys  
  
-   SQLNativeSql  
  
-   SQLProcedureColumns  
  
-   SQLProcedures  
  
-   SQLTablePrivileges
