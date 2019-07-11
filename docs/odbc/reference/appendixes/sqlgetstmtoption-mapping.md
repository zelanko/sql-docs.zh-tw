---
title: SQLGetStmtOption Mapping | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98bbdcf66ed9ee8f2d716d8953fde8f4a888fca0
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792860"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 對應
當應用程式呼叫**SQLGetStmtOption** odbc *3.x*不支援它，若要呼叫的驅動程式  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 會產生，如下所示：  
  
-   如果*fOption*指出傳回的字串，此驅動程式管理員會呼叫 ODBC 定義的陳述式選項  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指出傳回 32 位元整數值，此驅動程式管理員會呼叫 ODBC 定義的陳述式選項  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*表示驅動程式定義的陳述式選項，此驅動程式管理員會呼叫  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在上述三種情況下， *StatementHandle*引數設定中的值為*hstmt*，則*屬性*引數設定中的值為*fOption*，而*ValuePtr*引數設定為相同的值*pvParam*。  
  
 如 ODBC 定義的字串連接選項，請設定驅動程式管理員*Columnsize*呼叫中的引數**SQLGetConnectAttr**預先定義的最大長度 (SQL_MAX_OPTION_STRING_LENGTH);非連線選項，如*Columnsize*設為 0。  
  
 SQL_GET_BOOKMARK 陳述式選項已被取代，在 ODBC *3.x*。 適用於 ODBC *3.x*驅動程式搭配使用 ODBC *2.x*使用 SQL_GET_BOOKMARK，應用程式，就必須支援 SQL_GET_BOOKMARK。 適用於 ODBC *3.x*驅動程式搭配使用 ODBC *2.x*應用程式，它必須支援 SQL_USE_BOOKMARKS 設 SQL_UB_ON 和應該公開 （expose） 的固定長度書籤。 如果 ODBC *3.x*驅動程式支援只可變長度的書籤，不會在固定長度書籤，它必須傳回 SQLSTATE HYC00 （未實作選擇性功能） 如果 ODBC *2.x*應用程式嘗試SQL_USE_BOOKMARKS 設 SQL_UB_ON。  
  
 適用於 ODBC *3.x*驅動程式，則驅動程式管理員不會再檢查以查看是否*選項*介於 SQL_STMT_OPT_MIN 和 SQL_STMT_OPT_MAX，或大於 SQL_CONNECT_OPT_DRVR_START。 此驅動程式必須檢查此。
