---
title: 單代碼函數參數 |微軟文件
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
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284288"
---
# <a name="unicode-function-arguments"></a>Unicode 函式引數
ODBC 3.5(或更高版本)驅動程式管理員支援所有函數的 ANSI 和 Unicode 版本,這些函數在其參數中接受指向字串或 SQLPOINTER 的指標。 Unicode 函數作為函數實現(後綴為*W),* 而不是宏。 ANSI 函數(可以使用或不使用*A*的後綴呼叫)與目前的 ODBC API 函數相同。  
  
## <a name="remarks"></a>備註  
 始終返回或獲取字串或長度參數的 Unicode 函數作為字元計數傳遞。 對於返回伺服器數據長度資訊的函數,顯示大小和精度以字元數表示。 當長度(資料的傳輸大小)可以引用字串或非字串數據時,長度以八點長度描述。 例如 **,SQLGetInfoW**仍將長度作為位元組數,但**SQLExecDirectW**將使用字元計數。  
  
 字元計數是指 ANSI 函數的位元組數(八位數)和 UNICODE 函數的 WCHAR(16 位元字數)。 特別是,雙位元組位元序列 (DBCS) 或多位元組位元序列 (MBCS) 可以由多個字節組成。 UTF-16 Unicode 字元序列可以由多個 WR 組成。  
  
 以下是支援 Unicode (W) 與 ANSI (A) 版本的 ODBC API 函數的清單:  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColattributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSQL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLData來源**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSet 連線選項**|  
|**SQLExecDirect**|**SQLSetCursor 名稱**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 以下是支援 Unicode (W) 與 ANSI (A) 版本的 ODBC 安裝程式與 ODBC 轉換器函數的清單:  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstall 驅動程式管理員**|  
|**SQLCreate資料來源**|**SQL 安裝程式錯誤**|  
|**SQLDataSourceto 驅動程式**|**SQLInstallODBC**|  
|**SQLDriverto 資料來源**|**SQLReadFileDSN**|  
|**SQLGet 可驅動程式**|**SQLremoveSnfromINININ**|  
|**SQLGet 安裝驅動程式**|**SQLValidDSN**|  
|**SQLGet 轉換器**|**SQLwriteSntoINI**|  
|**SQL安裝驅動程式**||  
  
> [!NOTE]
>  棄用函數具有 Unicode 到 ANSI 映射支援,因為 ODBC *3.x*驅動程式管理員支援使用 UNICODE **#define**重新編譯 ODBC *2.x*應用程式。  
  
 此章節包含下列主題。  
  
-   [Unicode 應用程式](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Unicode 驅動程式](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [驅動程式管理員中的函式對應](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
