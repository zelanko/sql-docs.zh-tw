---
title: SQLSetStmtOption Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc4ed430b301f2b191c0586c0a54af19a2d2d526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091673"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 對應
當應用程式呼叫**SQLSetStmtOption**透過 ODBC *3.x*驅動程式，會呼叫  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 會產生，如下所示：  
  
-   如果*fOption*表示為字串時，此驅動程式管理員會呼叫 ODBC 定義的陳述式屬性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指出傳回 32 位元整數值，此驅動程式管理員會呼叫 ODBC 定義的陳述式屬性  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*表示驅動程式定義的陳述式屬性，此驅動程式管理員會呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在上述三種情況下， **StatementHandle**引數設定中的值為*hstmt*，則*屬性*引數設定中的值為*fOption*，而*ValuePtr*引數設定為值*vParam*。  
  
 驅動程式管理員不知道驅動程式定義的陳述式屬性需要字串或 32 位元整數值，因為它有傳入的有效值*StringLength*引數**SQLSetStmtAttr**. 如果驅動程式已定義特殊的驅動程式定義的陳述式屬性的語意，而且必須使用呼叫**SQLSetStmtOption**，就必須支援**SQLSetStmtOption**。  
  
 如果應用程式呼叫**SQLSetStmtOption**來設定 ODBC 中的驅動程式特有的陳述式選項*3.x*驅動程式和選項定義在 ODBC *2.x*版本驅動程式，如 ODBC 中的選項，應該定義新的資訊清單常數*3.x*驅動程式。 如果在呼叫中使用舊的資訊清單常數**SQLSetStmtOption**，驅動程式管理員會呼叫**SQLSetStmtAttr**具有*StringLength*引數設定為 0。  
  
 當應用程式呼叫**SQLSetStmtAttr** SQL_ATTR_USE_BOOKMARKS 設在 ODBC 中的 SQL_UB_ON *3.x* SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_FIXED 驅動程式。 SQL_UB_ON 是 SQL_UB_FIXED 為相同的常數。 驅動程式管理員會透過 SQL_UB_FIXED 傳遞至驅動程式。 SQL_UB_FIXED 已被取代，在 ODBC *3.x*，但是 ODBC *3.x*驅動程式必須實作它以搭配 ODBC *2.x*使用固定長度書籤的應用程式。  
  
 適用於 ODBC *3.x*驅動程式，則驅動程式管理員不會再檢查，看看是否*選項*介於 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，或大於 SQL_CONNECT_OPT_DRVR_START。
