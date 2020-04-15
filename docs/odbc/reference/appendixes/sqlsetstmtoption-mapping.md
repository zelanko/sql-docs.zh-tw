---
title: SQLSetStmtOption 映射 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91264cee0dfceeb7195e2bad40d1638a88e1e01a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304899"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption 對應
當應用程式透過 ODBC *3.x*驅動程式呼叫**SQLSetStmtOption**時,呼叫  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 結果如下:  
  
-   如果*fOption*指示為字串的 ODBC 定義的敘述屬性,驅動程式管理員將呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示傳回 32 位元整數值的 ODBC 定義的敘述屬性,則驅動程式管理員將呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驅動程式定義的語句屬性,則驅動程式管理員呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 在前面三種情況下,**語句句柄**參數設置為*hstmt*中的值,*屬性*參數設置為*fOption*中的值 *,ValuePtr*參數設置為*vParam*的值。  
  
 由於驅動程式管理員不知道驅動程式定義的語句屬性是否需要字串還是 32 位元整數值,因此必須為**SQLSetStmtAttr**的*StringLength*參數傳遞一個有效值。 如果驅動程式為驅動程式定義的語句屬性定義了特殊語義,並且需要使用**SQLSetStmtOption**呼叫 ,則必須支援**SQLSetStmtOption**。  
  
 如果應用程式呼叫**SQLSetStmtOption**在 ODBC *3.x*驅動程式中設定特定於驅動程式的語句選項,並且該選項在驅動程式的 ODBC *2.x*版本中定義,則應為 ODBC *3.x*驅動程式中的選項定義新的清單常量。 如果在調用**SQLSetStmtOption**時使用舊的清單常量,驅動程式管理器將調用**SQLSetStmtAttr,***字串長度*參數設置為 0。  
  
 當應用程式調用**SQLSetStmtAttr**將 SQL_ATTR_USE_BOOKMARKS設置為在 ODBC *3.x*驅動程式中SQL_UB_ON時,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_FIXED。 SQL_UB_ON與SQL_UB_FIXED的常量相同。 駕駛員管理員將SQL_UB_FIXED傳遞給駕駛員。 SQL_UB_FIXED已在 ODBC *3.x*中棄用,但 ODBC *3.x*驅動程式必須實現它才能與使用固定長度書籤的 ODBC *2.x*應用程式配合使用。  
  
 對於 ODBC *3.x*驅動程式,驅動程式管理器不再檢查*選項*是否位於SQL_STMT_OPT_MIN和SQL_STMT_OPT_MAX之間,還是大於SQL_CONNECT_OPT_DRVR_START。
