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
ms.openlocfilehash: 88ce592ebbf5a1b44d55b1b3119ef96e713112bc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74833022"
---
# <a name="unicode-function-arguments"></a>Unicode 函式引數
ODBC 3.5 （或更新版本）驅動程式管理員同時支援 ANSI 和 Unicode 版本的所有函式，這些函式會接受其引數中的字元字串或 SQLPOINTER 的指標。 Unicode 函式會實作為函式（尾碼為*W*），而不是宏。 ANSI 函式（可以使用或不含*尾碼來呼叫）與*目前的 ODBC API 函式完全相同。  
  
## <a name="remarks"></a>備註  
 一律傳回或接受字串或長度引數的 Unicode 函式，會以字元數的形式傳遞。 針對傳回伺服器資料之長度資訊的函式，顯示大小和精確度會以字元數來描述。 當長度（資料的傳輸大小）可以參考字串或非字串資料時，長度會以八位長度描述。 例如， **SQLGetInfoW**仍然會將長度視為位元組計數，但是**SQLExecDirectW**會使用字元數的計數。  
  
 字元計數指的是 ANSI 函式的位元組數（八位）以及 UNICODE 函式的 WCHAR （16位字組）數目。 特別的是，雙位元組字元序列（DBCS）或多位元組字元序列（MBCS）可以由多個位元組組成。 UTF-16 Unicode 字元序列可以由多個 WCHARs 組成。  
  
 以下是支援 Unicode （W）和 ANSI （A）版本的 ODBC API 函數清單：  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
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
|**SQLGetDiagField**||  
  
 以下是 ODBC 安裝程式和 ODBC 轉譯器函式的清單，這些函數支援 Unicode （W）和 ANSI （A）版本：  
  
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
>  已取代的函式具有 Unicode 到 ANSI 的對應支援，因為 ODBC *3.X 驅動程式*管理員支援使用 unicode **#define**重新編譯 ODBC *2.x 應用程式。*  
  
 此章節包含下列主題。  
  
-   [Unicode 應用程式](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驅動程式管理員中的函式對應](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
