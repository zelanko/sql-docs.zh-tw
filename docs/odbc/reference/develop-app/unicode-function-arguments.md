---
title: Unicode 函式引數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab660a9af95d6232f22c98a868da8fed9ebb0cae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917953"
---
# <a name="unicode-function-arguments"></a>Unicode 函式引數
ODBC 3.5 （或更新版本） 驅動程式管理員支援 ANSI 和 Unicode 版本的所有函式接受字元字串或 SQLPOINTER 在其引數的指標。 Unicode 函式會實作為函式 (且尾碼為*W*)，而不做巨集。 ANSI 函式 (或後置字元不可以呼叫的目標*A*) 等於目前的 ODBC API 函式。  
  
## <a name="remarks"></a>備註  
 Unicode 函式一律傳回或採用字串或長度引數會傳遞做為計算字元數。 對於傳回的伺服器資料的長度資訊的函式，顯示大小和有效位數所述的字元數。 長度 （傳輸的資料大小） 無法參照字串或非字串資料，當長度說明八位元長度。 例如， **SQLGetInfoW**仍會做為位元組計數的長度但**SQLExecDirectW**將會使用計數的字元。  
  
 計算字元數是指 ANSI 函式的位元組數 （八位元） 的數目和 WCHAR （16 位元字） 的 UNICODE 函式數目。 特別是，雙位元組字元序列 (DBCS) 或多位元組字元序列 (MBCS) 可以組合的多個位元組。 可以包括多個 WCHARs utf-16 Unicode 字元序列。  
  
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
>  已被取代的函式具有 Unicode-ANSI 對應支援，因為 ODBC 3 *.x*驅動程式管理員支援重新編譯 ODBC 2。*x*應用程式與 UNICODE **#define**。  
  
 此章節包含下列主題。  
  
-   [Unicode 應用程式](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驅動程式管理員中的函式對應](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
