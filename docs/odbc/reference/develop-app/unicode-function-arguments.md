---
title: Unicode 函式引數 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0e67f437cd629411230daed17f6a39f24b7103d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669456"
---
# <a name="unicode-function-arguments"></a>Unicode 函式引數
ODBC 3.5 （或更新版本） 驅動程式管理員支援接受字元字串或 SQLPOINTER 指標，其引數中的所有函式的 ANSI 和 Unicode 版本。 Unicode 函式會實作為函式 (尾碼*W*)，而非巨集。 ANSI 函式 (使用或後置字元不可以呼叫它*A*) 與目前的 ODBC API 函式相同。  
  
## <a name="remarks"></a>備註  
 Unicode 函式一律傳回或接受字串或長度引數會傳遞為計算字元數。 針對傳回的伺服器資料的長度資訊的函式，顯示大小和精確度所述的字元數。 時的長度 （傳輸的資料大小） 無法參照字串或非字串資料，請將長度說明八位元長度。 例如， **SQLGetInfoW**仍會做為位元組計數的長度，但**SQLExecDirectW**將會使用計數的字元。  
  
 計算字元數是指 ANSI 函式的位元組數 （八位元） 的數目和 UNICODE 函式 WCHAR （16 位元單字） 的數目而定。 特別是，雙位元組字元序列 (DBCS) 或多位元組字元序列 (MBCS) 可以包含多個位元組。 可以包含多個 WCHARs utf-16 Unicode 字元序列。  
  
 以下是支援 Unicode (W) 和 ANSI (A) 版本的 ODBC API 函式的清單：  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
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
  
 以下是支援 Unicode (W) 和 ANSI (A) 版本的 ODBC 安裝程式和 ODBC 轉譯器函式的清單：  
  
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
>  已被取代的函式具有 Unicode-ANSI 對應支援，因為 ODBC 3 *.x*驅動程式管理員支援重新編譯 ODBC 2。*x*使用 UNICODE 應用程式 **#define**。  
  
 此章節包含下列主題。  
  
-   [Unicode 應用程式](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驅動程式管理員中的函式對應](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
