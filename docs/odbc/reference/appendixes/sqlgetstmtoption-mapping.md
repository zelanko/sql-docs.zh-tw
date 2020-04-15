---
title: SQLGetStmtOption 映射 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300598"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 對應
當應用程式將**SQLGetStmtOption**呼叫不支援它的 ODBC *3.x*驅動程式時,呼叫  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 結果如下:  
  
-   如果*fOption*指示傳回字串的 ODBC 定義的敘述選項,驅動程式管理員將呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示一個 ODBC 定義的語句選項,該選項傳回 32 位元整數值,則驅動程式管理員將呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驅動程式定義的語句選項,則驅動程式管理員將呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面三種情況下,*語句句柄*參數設定為*hstmt*中的值,*屬性*參數設置為*fOption*中的值 *,ValuePtr*參數設定為與*pvParam*相同的值。  
  
 對於 ODBC 定義的字串連接選項,驅動程式管理器在調用**SQLGetConnectAttr**時將*緩衝區長度*參數設定為預定義的最大長度(SQL_MAX_OPTION_STRING_LENGTH);對於非字串連接選項,*緩衝區長度*設置為 0。  
  
 SQL_GET_BOOKMARK語句選項已在 ODBC *3.x*中棄用。 對於使用SQL_GET_BOOKMARK的 ODBC *3.x*驅動程式*2.x*,它必須支援SQL_GET_BOOKMARK。 對於 ODBC *3.x*驅動程式*2.x*,必須支援 將SQL_USE_BOOKMARKS設置為SQL_UB_ON,並且應公開固定長度的書籤。 如果 ODBC *3.x*驅動程式僅支援可變長度書籤,不支援固定長度書籤,則必須返回 SQLSTATE HYC00(未實現可選功能)(如果 ODBC *2.x*應用程式嘗試將SQL_USE_BOOKMARKS設置為SQL_UB_ON。  
  
 對於 ODBC *3.x*驅動程式,驅動程式管理器不再檢查*選項*是否介於SQL_STMT_OPT_MIN和SQL_STMT_OPT_MAX之間,還是大於SQL_CONNECT_OPT_DRVR_START。 驅動程序必須檢查此情況。
