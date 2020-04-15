---
title: 接受字串參數的功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d0f143c72f57e946f7fe2bf52a50910d4e56aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286298"
---
# <a name="functions-accepting-string-parameters"></a>接受字串參數的函式
所有採用字串參數的函數都將轉換為 Unicode。 (將匯出函數的"W"形式。位元組計數將轉換為適用於 ODBC API 的字元計數。 這適用於以下功能:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **SQLColattributes**  
  
-   **SQLDescribeCol**  
  
-   **SQLError(** 取代為**SQLGetDiagField)**  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursor 名稱**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** (成為**SQLGetStmtAttr**)  
  
-   **SQLSetStmtOption** (成為**SQLSetStmtAttr**)  
  
-   **SQLGetConnectOption**  
  
-   **SQLSet 連線選項**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQLNativeSQL**  
  
-   **SQLSpecialColumns**  
  
-   **設定DSNEx**  
  
-   **設定DSN**
