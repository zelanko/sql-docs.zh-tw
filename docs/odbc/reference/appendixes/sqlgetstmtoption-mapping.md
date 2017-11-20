---
title: "SQLGetStmtOption 對應 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 503af3ea0dbac61cee506b932f79eccab5dedcf8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 對應
當應用程式呼叫**SQLGetStmtOption** ODBC 3*.x*不支援呼叫它的驅動程式  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 將會產生，如下所示：  
  
-   如果*fOption*指出傳回的字串，此驅動程式管理員會呼叫 ODBC 定義陳述式選項  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指出傳回 32 位元整數值，驅動程式管理員呼叫 ODBC 定義陳述式選項  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*表示驅動程式定義陳述式選項，驅動程式管理員呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前述三個情況下， *StatementHandle*引數設定中的值為*hstmt*、*屬性*引數設定中的值為*fOption*，而*ValuePtr*引數設定為相同的值做為*pvParam*。  
  
 針對 ODBC 定義的字串連接選項，設定驅動程式管理員*Columnsize*引數在呼叫**SQLGetConnectAttr**預先定義的最大長度 (SQL_MAX_OPTION_STRING_LENGTH);將非字串的連接選項，如*Columnsize*設為 0。  
  
 SQL_GET_BOOKMARK 陳述式選項已被取代，在 ODBC 3*.x*。 ODBC 3*.x*驅動程式，才能使用 ODBC 2。*x*使用 SQL_GET_BOOKMARK，應用程式，就必須支援 SQL_GET_BOOKMARK。 ODBC 3*.x*驅動程式，才能使用 ODBC 2。*x*應用程式，就必須支援 SQL_USE_BOOKMARKS 設 SQL_UB_ON 和應該公開 （expose） 的固定長度的書籤。 如果 ODBC 3*.x*驅動程式支援只可變長度的書籤，不會在固定長度的書籤，它必須傳回 SQLSTATE HYC00 （未實作的選擇性功能） 如果 ODBC 2。*x* SQL_USE_BOOKMARKS 設 SQL_UB_ON 嘗試應用程式。  
  
 ODBC 3*.x*驅動程式，驅動程式管理員不會再檢查以查看是否*選項*之間 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，或大於 SQL_CONNECT_OPT_DRVR_START。 驅動程式必須檢查。

