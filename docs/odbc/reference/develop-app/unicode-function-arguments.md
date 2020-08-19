---
description: Unicode 函式引數
title: Unicode 函數引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d2d59cad60855c670f7c7e2b189ad3c97a3027b9
ms.sourcegitcommit: 19ae05bc69edce1e3b3d621d7fdd45ea5f74969d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564036"
---
# <a name="unicode-function-arguments"></a>Unicode 函式引數
ODBC 3.5 (或更高版本的) 驅動程式管理員支援所有函式的 ANSI 和 Unicode 版本，這些函式會在其引數中接受字元字串或 SQLPOINTER 的指標。 Unicode 函數會實作為函式 (尾碼為 *W*) ，而不是宏。 ANSI 函式 (可以使用或不 *含) 的* 尾碼來呼叫，與目前的 ODBC API 函數相同。  
  
## <a name="remarks"></a>備註  
 對於一律傳回或採用字串或長度引數的 Unicode 函式，會將引數傳遞為字元數。 若為傳回伺服器資料長度資訊的函式，顯示大小和有效位數會以字元數來描述。 當資料) 的長度 (傳輸大小可能參考字串或非字串資料時，長度會以八位長度描述。 例如， **SQLGetInfoW** 的長度仍會以位元組數為單位，但 **SQLExecDirectW** 將會使用字元數。  
  
 字元數是指 ANSI 函式 (八位) 的位元組數，以及 UNICODE 函式) 的 WCHAR (16 位字組數目。 尤其是雙位元組字元序列 (DBCS) 或多位元組字元序列 (MBCS) 可以由多個位元組組成。 UTF-16 Unicode 字元序列可以由多個 WCHARs 組成。  
  
 以下是一份 ODBC API 函式清單，支援 Unicode (W) 和 ANSI () 版本：  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSql**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 以下是一份 ODBC 安裝程式和 ODBC 轉譯器函式的清單，這些函數支援 Unicode (W) 和 ANSI () 版本：  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  已淘汰的函式有 Unicode 至 ANSI 的對應支援，因為 ODBC *3.X 驅動程式*管理員支援使用 unicode **#define**重新*編譯 ODBC 2.x 應用程式。*  
  
 此章節包含下列主題。  
  
-   [Unicode 應用程式](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驅動程式管理員中的函式對應](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
